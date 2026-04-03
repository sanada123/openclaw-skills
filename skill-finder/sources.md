# skill-finder — Source Documentation

Each source skill-finder searches, with working curl examples, auth requirements, rate limits, and what it's best for.

---

## Source Overview

| # | Source | Base URL | Auth | Rate Limit | Best For |
|---|---|---|---|---|---|
| 1 | **Local workspace** | filesystem | none | unlimited | Already-installed skills |
| 2 | **Our GitHub** | api.github.com | optional | 60–5000/hr | Your published skills |
| 3 | **ClawHub** | clawhub.ai/api/v1 | none | 60/min | Quality-curated skill search |
| 4 | **GitHub topics** | api.github.com | optional | 60–5000/hr | Community skills |
| 5 | **npm registry** | registry.npmjs.org | none | ~1000/hr | Versioned/packaged skills |
| 6 | **skillsmp.com** | skillsmp.com/api | none | unknown | Alternative marketplace |

---

## Source 1: Local Workspace

**No network call required.** Scans two directories.

### Paths scanned (detected automatically, cross-platform)

Local skill directories are detected at runtime — no hardcoded paths:

```
~/.openclaw/skills/                  (primary — all platforms)
~/.openclaw/workspace/skills/        (workspace install)
$OPENCLAW_SKILLS_DIR                 (custom override — set this env var to add paths)
./skills/                            (current working directory)
```

On Windows, `~` resolves to `%USERPROFILE%` (e.g. `C:\Users\YourName`).
Alternatively, set `OPENCLAW_SKILLS_DIR=%APPDATA%\OpenClaw\skills` on Windows.

### Curl equivalent (filesystem scan)

```bash
# Detect skill directories dynamically
LOCAL_DIRS=""
[ -d "$HOME/.openclaw/skills" ] && LOCAL_DIRS="$HOME/.openclaw/skills"
[ -d "$HOME/.openclaw/workspace/skills" ] && LOCAL_DIRS="$LOCAL_DIRS $HOME/.openclaw/workspace/skills"
[ -n "$OPENCLAW_SKILLS_DIR" ] && LOCAL_DIRS="$LOCAL_DIRS $OPENCLAW_SKILLS_DIR"
[ -d "./skills" ] && LOCAL_DIRS="$LOCAL_DIRS ./skills"

# List all detected skills with their descriptions
for dir in $LOCAL_DIRS; do
  for skill_dir in "$dir"/*/; do
    [ -d "$skill_dir" ] || continue
    skill_name=$(basename "$skill_dir")
    skill_md="$skill_dir/SKILL.md"
    if [ -f "$skill_md" ]; then
      description=$(grep -m1 '^description:' "$skill_md" 2>/dev/null \
        | sed 's/^description: *//' | tr -d '"')
      echo "name=$skill_name | description=$description"
    fi
  done
done
```

### Response shape

```
name=telegram-bot | description=Use when sending Telegram notifications...
name=n8n-workflow | description=Use when building n8n automation flows...
```

### Notes

- Skills here are already installed — no install action needed
- These always appear first in FIND results (rank 1)
- `STATUS` command primarily uses this source

---

## Source 2: Our GitHub (`sanada123/openclaw-skills`)

**Our own published skill library.** Highest trust after local.

### List all skills

```bash
curl -s \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer ${GITHUB_TOKEN}" \
  "https://api.github.com/repos/sanada123/openclaw-skills/contents/" \
  | jq '.[] | select(.type == "dir") | {name: .name, url: .html_url, path: .path}'
```

### Fetch a specific skill's SKILL.md

```bash
curl -s \
  -H "Accept: application/vnd.github.raw+json" \
  -H "Authorization: Bearer ${GITHUB_TOKEN}" \
  "https://api.github.com/repos/sanada123/openclaw-skills/contents/telegram-bot/SKILL.md"
```

### Search within repo (filename match)

```bash
curl -s \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer ${GITHUB_TOKEN}" \
  "https://api.github.com/search/code?q=${QUERY}+repo:sanada123/openclaw-skills+filename:SKILL.md" \
  | jq '.items[] | {name: .repository.name, path: .path, url: .html_url}'
```

### Download and install a skill

```bash
SKILL_NAME="telegram-bot"
TARGET_DIR="${OPENCLAW_SKILLS_DIR:-$HOME/.openclaw/skills}/$SKILL_NAME"
mkdir -p "$TARGET_DIR"

# Get all files in the skill directory
curl -s \
  -H "Accept: application/vnd.github+json" \
  "https://api.github.com/repos/sanada123/openclaw-skills/contents/$SKILL_NAME" \
  | jq -r '.[] | .download_url' \
  | while read url; do
      filename=$(basename "$url")
      curl -s -L "$url" -o "$TARGET_DIR/$filename"
      echo "Downloaded: $filename"
    done
```

### Rate limits

- Unauthenticated: 60 req/hour (shared with GitHub topics source)
- With `GITHUB_TOKEN`: 5000 req/hour
- Search API: 30 req/min (unauthenticated), 30 req/min (authenticated)

---

## Source 3: ClawHub

**The primary OpenClaw skill marketplace.** 10,000+ skills, semantic search, curated quality.

### Search

```bash
curl -s "https://clawhub.ai/api/v1/search?q=telegram&limit=10" \
  | jq '.results[] | {
      name: .slug,
      title: .name,
      description: .description,
      score: .relevance_score,
      author: .author,
      downloads: .downloads,
      updated: .updated_at
    }'
```

### Trending skills

```bash
# Trending this week
curl -s "https://clawhub.ai/api/v1/trending?period=week&limit=20" \
  | jq '.[] | {name: .slug, description: .description, downloads: .weekly_downloads}'

# Newest published
curl -s "https://clawhub.ai/api/v1/skills?sort=newest&limit=20" \
  | jq '.skills[] | {name: .slug, published: .created_at}'

# Most popular all-time
curl -s "https://clawhub.ai/api/v1/skills?sort=downloads&limit=20" \
  | jq '.skills[] | {name: .slug, downloads: .downloads}'
```

### Fetch raw SKILL.md (for VET command)

```bash
curl -s "https://clawhub.ai/api/v1/skills/telegram-bot/raw"
```

### Fetch skill metadata

```bash
curl -s "https://clawhub.ai/api/v1/skills/telegram-bot" \
  | jq '{
      slug: .slug,
      description: .description,
      author: .author,
      version: .version,
      downloads: .downloads,
      tags: .tags
    }'
```

### Rate limits

- 60 requests/minute, no authentication required
- No token needed for public skill search

---

## Source 4: GitHub Topics (`openclaw-skill`)

**Community-published skills** in standalone repositories tagged with the `openclaw-skill` topic.

### Search by query + topic

```bash
curl -s \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer ${GITHUB_TOKEN}" \
  "https://api.github.com/search/repositories?q=topic:openclaw-skill+${QUERY}&sort=stars&order=desc&per_page=10" \
  | jq '.items[] | {
      name: .name,
      owner: .owner.login,
      description: .description,
      stars: .stargazers_count,
      updated: .updated_at,
      install_cmd: ("skill-finder: install github:" + .owner.login + "/" + .name)
    }'
```

### Browse all skills with this topic (no query filter)

```bash
curl -s \
  -H "Accept: application/vnd.github+json" \
  "https://api.github.com/search/repositories?q=topic:openclaw-skill&sort=stars&order=desc&per_page=30" \
  | jq '.total_count, [.items[] | {name: .name, owner: .owner.login, stars: .stargazers_count}]'
```

### Check if a repo has a SKILL.md

```bash
OWNER="some-user"
REPO="some-skill"
STATUS=$(curl -s -o /dev/null -w "%{http_code}" \
  -H "Accept: application/vnd.github+json" \
  "https://api.github.com/repos/${OWNER}/${REPO}/contents/SKILL.md")
echo "SKILL.md status: $STATUS"   # 200 = found, 404 = missing
```

### Notes

- Community skills vary in quality — always VET before installing
- Repos without a SKILL.md are still listed but VET will warn
- Sort by stars for quality signal

---

## Source 5: npm Registry

Skills published as npm packages with the `openclaw-skill` prefix convention.

### Search

```bash
curl -s \
  "https://registry.npmjs.org/-/v1/search?text=openclaw-skill+telegram&size=5" \
  | jq '.objects[] | {
      name: .package.name,
      description: .package.description,
      version: .package.version,
      author: .package.author.name,
      weekly_downloads: .package.links.npm,
      popularity: .score.detail.popularity,
      install_cmd: ("skill-finder: install npm:" + .package.name)
    }'
```

### Fetch package metadata directly

```bash
curl -s "https://registry.npmjs.org/openclaw-skill-telegram-bot" \
  | jq '{
      name: .name,
      version: .["dist-tags"].latest,
      description: .description,
      keywords: .keywords,
      homepage: .homepage
    }'
```

### Fetch SKILL.md from npm package (via unpkg CDN)

```bash
PACKAGE="openclaw-skill-telegram-bot"
curl -s "https://unpkg.com/${PACKAGE}/SKILL.md"
# Returns 404 if SKILL.md not in package root
```

### Check weekly download stats

```bash
curl -s "https://api.npmjs.org/downloads/point/last-week/openclaw-skill-telegram-bot" \
  | jq '{package: .package, downloads: .downloads}'
```

### Notes

- Package naming convention: `openclaw-skill-<name>`
- Check for SKILL.md at package root before listing in results
- VET reads the SKILL.md fetched from unpkg
- npm packages may include node_modules — extra scrutiny warranted

---

## Source 6: skillsmp.com

**Alternative marketplace.** Treated as best-effort: skill-finder tries it and moves on if unavailable.

### Search

```bash
curl -s --max-time 3 \
  "https://skillsmp.com/api/search?q=telegram" \
  | jq '.results[] | {
      name: .slug,
      description: .description,
      install_cmd: ("skill-finder: install skillsmp:" + .slug)
    }' 2>/dev/null || echo "skillsmp.com unavailable"
```

### Graceful failure pattern

```bash
RESULT=$(curl -s --max-time 3 "https://skillsmp.com/api/search?q=${QUERY}" 2>/dev/null)
EXIT_CODE=$?

if [ $EXIT_CODE -ne 0 ] || [ -z "$RESULT" ]; then
  echo '[skillsmp.com: unavailable, skipped]'
  SKILLSMP_RESULTS="[]"
else
  SKILLSMP_RESULTS=$(echo "$RESULT" | jq '.results // []' 2>/dev/null || echo "[]")
fi
```

### Notes

- API availability not guaranteed — always wrap in `--max-time 3` + error handling
- If API returns non-JSON (e.g., HTML error page), treat as unavailable
- Quality is unknown — VET any skills from this source before installing

---

## Parallel Search Pattern

All sources run concurrently via background jobs:

```bash
#!/bin/bash
QUERY="${1:-telegram}"
GH_AUTH="${GITHUB_TOKEN:+-H \"Authorization: Bearer $GITHUB_TOKEN\"}"
TMPDIR=$(mktemp -d)
trap "rm -rf $TMPDIR" EXIT

# Launch all source searches in background
curl -s "https://clawhub.ai/api/v1/search?q=${QUERY}&limit=10" \
  > "$TMPDIR/clawhub.json" &

curl -s -H "Accept: application/vnd.github+json" \
  ${GITHUB_TOKEN:+-H "Authorization: Bearer $GITHUB_TOKEN"} \
  "https://api.github.com/repos/sanada123/openclaw-skills/contents/" \
  > "$TMPDIR/our-github.json" &

curl -s -H "Accept: application/vnd.github+json" \
  ${GITHUB_TOKEN:+-H "Authorization: Bearer $GITHUB_TOKEN"} \
  "https://api.github.com/search/repositories?q=topic:openclaw-skill+${QUERY}&sort=stars&per_page=10" \
  > "$TMPDIR/github-topics.json" &

curl -s "https://registry.npmjs.org/-/v1/search?text=openclaw-skill+${QUERY}&size=5" \
  > "$TMPDIR/npm.json" &

curl -s --max-time 3 "https://skillsmp.com/api/search?q=${QUERY}" \
  > "$TMPDIR/skillsmp.json" 2>/dev/null &

# Wait for all concurrent calls to complete
wait

echo "All sources responded. Results in $TMPDIR/"
ls -la "$TMPDIR/"
```

Expected total time: **~1.5 seconds** (limited by slowest responding source, not sum).
