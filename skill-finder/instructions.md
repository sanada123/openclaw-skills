# skill-finder — Technical Reference

Full API reference, curl examples, deduplication algorithm, and security scoring details.

---

## API Endpoints

### 1. ClawHub Search

```bash
# Semantic search — returns skills ranked by relevance
curl -s "https://clawhub.ai/api/v1/search?q=telegram&limit=10" \
  | jq '.results[] | {name: .slug, description: .description, score: .relevance_score, install: .slug}'
```

**Response shape:**
```json
{
  "results": [
    {
      "slug": "telegram-bot",
      "name": "Telegram Bot",
      "description": "Send messages via Telegram Bot API",
      "relevance_score": 0.92,
      "author": "sanada123",
      "downloads": 1847,
      "updated_at": "2026-03-15T10:00:00Z"
    }
  ],
  "total": 47
}
```

**Parse to normalized format:**
```bash
curl -s "https://clawhub.ai/api/v1/search?q=${QUERY}" | jq '[
  .results[] | {
    name: .slug,
    source: "clawhub",
    description: .description,
    score: .relevance_score,
    stars: .downloads,
    install_cmd: ("skill-finder: install " + .slug),
    url: ("https://clawhub.ai/skills/" + .slug)
  }
]'
```

---

### 2. GitHub Topics Search

```bash
# Search repos tagged with openclaw-skill topic
curl -s \
  -H "Accept: application/vnd.github+json" \
  ${GITHUB_TOKEN:+-H "Authorization: Bearer $GITHUB_TOKEN"} \
  "https://api.github.com/search/repositories?q=topic:openclaw-skill+${QUERY}&sort=stars&order=desc&per_page=10" \
  | jq '.items[] | {
      name: .name,
      source: "github-community",
      description: .description,
      stars: .stargazers_count,
      owner: .owner.login,
      install_cmd: ("skill-finder: install github:" + .owner.login + "/" + .name),
      url: .html_url
    }'
```

**Rate limit check:**
```bash
curl -s -I \
  ${GITHUB_TOKEN:+-H "Authorization: Bearer $GITHUB_TOKEN"} \
  "https://api.github.com/rate_limit" | grep -E "x-ratelimit"
```

**Set token for 5000 req/hour:**
```bash
export GITHUB_TOKEN=ghp_yourpersonalaccesstoken
```

---

### 3. Our GitHub Skills Repo

```bash
# List all skills in sanada123/openclaw-skills
curl -s \
  -H "Accept: application/vnd.github+json" \
  ${GITHUB_TOKEN:+-H "Authorization: Bearer $GITHUB_TOKEN"} \
  "https://api.github.com/repos/sanada123/openclaw-skills/contents/" \
  | jq '[
      .[] | select(.type == "dir") | {
        name: .name,
        source: "our-github",
        install_cmd: ("skill-finder: install github:sanada123/openclaw-skills/" + .name),
        url: .html_url
      }
    ]'

# Fetch SKILL.md for a specific skill to get description
curl -s \
  -H "Accept: application/vnd.github.raw+json" \
  "https://api.github.com/repos/sanada123/openclaw-skills/contents/${SKILL_NAME}/SKILL.md" \
  | head -10
```

---

### 4. Local Skills Scan

```bash
# Workspace skills
ls -1d /home/node/.openclaw/workspace/skills/*/  2>/dev/null \
  | xargs -I{} basename {} \
  | while read skill; do
      desc=$(grep -m1 "^description:" \
        "/home/node/.openclaw/workspace/skills/$skill/SKILL.md" 2>/dev/null \
        | sed 's/description: *//' | tr -d '"')
      echo "{\"name\":\"$skill\",\"source\":\"local\",\"description\":\"$desc\",\"install_cmd\":\"(installed)\"}"
    done | jq -s '.'

# User skills
ls -1d ~/.openclaw/skills/*/  2>/dev/null \
  | xargs -I{} basename {} \
  | while read skill; do
      echo "{\"name\":\"$skill\",\"source\":\"local-user\",\"install_cmd\":\"(installed)\"}"
    done | jq -s '.'
```

---

### 5. skillsmp.com (Graceful Fallback)

```bash
# Try the search endpoint — continue if it fails
SMPRESULT=$(curl -s --max-time 3 \
  "https://skillsmp.com/api/search?q=${QUERY}" 2>/dev/null) || SMPRESULT=""

if [ -n "$SMPRESULT" ] && echo "$SMPRESULT" | jq -e '.results' >/dev/null 2>&1; then
  echo "$SMPRESULT" | jq '[
    .results[] | {
      name: .slug,
      source: "skillsmp",
      description: .description,
      install_cmd: ("skill-finder: install skillsmp:" + .slug)
    }
  ]'
else
  echo "[]"  # Return empty array — do not fail the overall search
fi
```

---

### 6. npm Registry

```bash
# Search npm for openclaw-skill packages
curl -s \
  "https://registry.npmjs.org/-/v1/search?text=openclaw-skill+${QUERY}&size=5" \
  | jq '[
      .objects[] | {
        name: .package.name,
        source: "npm",
        description: .package.description,
        stars: (.score.detail.popularity * 100 | floor),
        weekly_downloads: .package.links.npm,
        version: .package.version,
        install_cmd: ("skill-finder: install npm:" + .package.name)
      }
    ]'
```

---

## Deduplication Algorithm

When FIND runs all sources concurrently, results from different sources may refer to the same skill.

**Step 1: Normalize names**
```bash
normalize() {
  echo "$1" \
    | tr '[:upper:]' '[:lower:]' \
    | sed 's/[^a-z0-9]/-/g' \
    | sed 's/--*/-/g' \
    | sed 's/^-//;s/-$//'
}
# Examples:
# "Telegram Bot"        → "telegram-bot"
# "telegram_bot"        → "telegram-bot"
# "openclaw-skill-telegram-bot" → "openclaw-skill-telegram-bot"
# Strip "openclaw-skill-" prefix for comparison:
# "openclaw-skill-telegram-bot" → "telegram-bot"
```

**Step 2: Merge by normalized name**

When the same normalized name appears across sources, keep the highest-trust entry but attach all sources as metadata:
```json
{
  "name": "telegram-bot",
  "canonical_source": "clawhub",
  "also_available": ["our-github", "npm"],
  "description": "...",
  "install_cmd": "skill-finder: install telegram-bot"
}
```

**Step 3: Trust ranking for dedup winner**

```
Priority (highest wins for canonical):
  1. local           — already installed, no action needed
  2. our-github      — sanada123/openclaw-skills
  3. clawhub         — platform-curated, relevance-scored
  4. github-community — community, ranked by stars
  5. npm             — versioned but indirect
  6. skillsmp        — unknown quality
```

**Step 4: Filter near-matches (fuzzy)**

Skills whose names share 80%+ of tokens are shown as "related":
```
telegram-bot          (exact match across clawhub + npm)
telegram-notifier     (related — shares "telegram")
telegram-webhook      (related — shares "telegram")
```

---

## Security Scoring System (0–10)

Each check runs against the raw text of `SKILL.md`. Claude evaluates meaning, not just keywords.

### Positive signals (+points)

| Signal | Points | Detection |
|---|---|---|
| Explicit permissions section in SKILL.md | +1 | Grep for `## Permissions` or `## Required Access` |
| All API calls go to known-safe domains | +1 | Parse domains from curl/fetch calls, check against allowlist |
| Author has 5+ published skills | +1 | Check author's skill count via ClawHub or GitHub |
| Dependencies pinned to specific versions | +1 | `@1.2.3` not `@latest` or `@*` |

### Negative signals (−points)

| Signal | Points | Detection |
|---|---|---|
| Reads env vars that look like credentials | -1 | Regex: `\$[A-Z_]*(TOKEN|KEY|SECRET|PASSWORD|API)` |
| Executes shell commands via exec/subprocess | -1 | `exec(`, `subprocess`, `os.system`, backtick syntax |
| Installs packages at runtime | -2 | `npm install`, `pip install`, `brew install` in skill body |
| Accesses filesystem paths outside workspace | -2 | Absolute paths like `/etc/`, `/root/`, `~/.ssh/` |
| Contains base64-encoded or obfuscated content | -3 | Long base64 strings, eval of encoded data |
| Calls unknown external endpoints | -1 | Domains not in a recognized allowlist |

### Known-safe domain allowlist

```
api.telegram.org
api.openai.com
api.anthropic.com
api.github.com
registry.npmjs.org
clawhub.ai
api.slack.com
hooks.slack.com
api.notion.com
api.linear.app
discord.com/api
```

Add your own to `~/.openclaw/skill-finder/safe-domains.txt`.

### Verdict thresholds

```
Score  Verdict   Action
8–10   SAFE      Install freely
5–7    REVIEW    Read SKILL.md carefully, especially flagged sections
3–4    RISKY     Only install if you fully understand the skill
0–2    DANGER    Do not install. Escalate for manual review.
```

### Full vet example

```bash
# Fetch SKILL.md from ClawHub
SKILL_CONTENT=$(curl -s "https://clawhub.ai/api/v1/skills/telegram-bot/raw")

# Check for credential env vars
echo "$SKILL_CONTENT" | grep -oE '\$[A-Z_]*(TOKEN|KEY|SECRET|PASSWORD|API)[A-Z_]*'

# Check for shell execution
echo "$SKILL_CONTENT" | grep -E 'exec\(|subprocess|os\.system|`[^`]+`'

# Check for runtime installs
echo "$SKILL_CONTENT" | grep -E 'npm install|pip install|brew install'

# Check for suspicious paths
echo "$SKILL_CONTENT" | grep -E '/etc/|/root/|~/.ssh/|/proc/'

# Check for base64
echo "$SKILL_CONTENT" | grep -E '[A-Za-z0-9+/]{50,}={0,2}'
```

---

## Concurrent Search Implementation

FIND runs all sources in parallel using background processes:

```bash
QUERY="$1"
TMPDIR=$(mktemp -d)

# Launch all searches concurrently
curl -s "https://clawhub.ai/api/v1/search?q=${QUERY}" > "$TMPDIR/clawhub.json" &
curl -s -H "${GH_AUTH}" "https://api.github.com/search/repositories?q=topic:openclaw-skill+${QUERY}" > "$TMPDIR/github.json" &
curl -s -H "${GH_AUTH}" "https://api.github.com/repos/sanada123/openclaw-skills/contents/" > "$TMPDIR/our-github.json" &
curl -s --max-time 3 "https://skillsmp.com/api/search?q=${QUERY}" > "$TMPDIR/skillsmp.json" 2>/dev/null &
curl -s "https://registry.npmjs.org/-/v1/search?text=openclaw-skill+${QUERY}&size=5" > "$TMPDIR/npm.json" &

# Wait for all to complete
wait

# Parse each source, normalize, then merge
# (implemented in Claude's response context — not a shell-only operation)
```

Total latency ≈ max(individual response times), typically 1–2 seconds.

---

## Edge Cases

### GitHub 403 / Rate Limited
```bash
# Check remaining rate limit
curl -s -H "Accept: application/vnd.github+json" \
  "https://api.github.com/rate_limit" | jq '.rate'
# {"limit": 60, "remaining": 0, "reset": 1743800000}

# Solution: set GITHUB_TOKEN or wait until reset
date -d @1743800000   # Convert reset timestamp to human-readable
```

### ClawHub returns 404 or empty
- Fall through to GitHub sources
- Note in output: `[ClawHub: no results for "query"]`
- Don't fail the whole search

### SKILL.md not found in GitHub repo
```bash
# Try common paths
for path in "SKILL.md" "skill.md" "README.md"; do
  result=$(curl -s -o /dev/null -w "%{http_code}" \
    "https://api.github.com/repos/${REPO}/contents/${path}")
  [ "$result" = "200" ] && echo "Found: $path" && break
done
```

### Private GitHub repo
```bash
# Requires token with repo scope
curl -s \
  -H "Authorization: Bearer $GITHUB_TOKEN" \
  -H "Accept: application/vnd.github.raw+json" \
  "https://api.github.com/repos/PRIVATE_ORG/PRIVATE_REPO/contents/SKILL.md"
# Returns 404 without auth — handle gracefully
```

### npm package has no SKILL.md
- npm skills are `openclaw-skill-*` packages
- SKILL.md is expected at package root
- If missing, mark source as `npm-no-skill-md` and skip VET
- Install still works — just no description to show

### skillsmp.com unreachable
- `--max-time 3` on curl ensures we don't block
- Treat empty/error response as `[]`
- Log: `[skillsmp.com: unavailable, skipped]`

---

## clawhub CLI Integration

If `clawhub` CLI is installed, use it directly for better performance:

```bash
# Check if clawhub CLI is available
command -v clawhub >/dev/null 2>&1 && HAVE_CLAWHUB=true

# Use CLI if available, fall back to API
if [ "$HAVE_CLAWHUB" = true ]; then
  clawhub search "$QUERY" --json
else
  curl -s "https://clawhub.ai/api/v1/search?q=${QUERY}"
fi

# Install via CLI
clawhub install <slug>

# Check installed version
clawhub info <slug>
```
