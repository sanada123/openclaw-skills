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

## Source 1: Local Workspace (All Platforms)

**No network call required.** Scans skill/rules directories for every detected AI platform.

### Paths scanned (detected automatically, all platforms)

Skill directories are detected at runtime across all installed platforms:

```
# OpenClaw
~/.openclaw/skills/                  (primary OpenClaw install)
~/.openclaw/workspace/skills/        (workspace install)
$OPENCLAW_SKILLS_DIR                 (custom override)

# Claude Code
~/.claude/skills/                    (global Claude Code skills)
./.claude/skills/                    (project-local Claude Code skills)

# Codex (OpenAI)
~/.codex/skills/                     (Codex global skills)

# Cursor
~/.cursor/rules/                     (global Cursor rules)
./.cursor/rules/                     (project-local Cursor rules)

# Windsurf
~/.windsurf/rules/                   (global Windsurf rules)
./.windsurf/rules/                   (project-local Windsurf rules)

# Continue
~/.continue/rules/                   (Continue dev rules)

# Generic
./skills/                            (current working directory)
./.agents/skills/                    (local agents directory)
~/.agents/skills/                    (global agents directory)
```

On Windows, `~` resolves to `%USERPROFILE%` (e.g. `C:\Users\YourName`).
Alternatively, set `OPENCLAW_SKILLS_DIR=%APPDATA%\OpenClaw\skills` on Windows.

### Filesystem scan (all platforms)

```bash
# Detect all platform skill directories
detect_skill_dirs() {
  local dirs=()
  [[ -d "$HOME/.openclaw/skills" ]] && dirs+=("$HOME/.openclaw/skills [openclaw]")
  [[ -d "$HOME/.openclaw/workspace/skills" ]] && dirs+=("$HOME/.openclaw/workspace/skills [openclaw]")
  [[ -n "$OPENCLAW_SKILLS_DIR" && -d "$OPENCLAW_SKILLS_DIR" ]] && dirs+=("$OPENCLAW_SKILLS_DIR [openclaw-custom]")
  [[ -d "$HOME/.claude/skills" ]] && dirs+=("$HOME/.claude/skills [claude-code]")
  [[ -d "./.claude/skills" ]] && dirs+=("./.claude/skills [claude-code-local]")
  [[ -d "$HOME/.codex/skills" ]] && dirs+=("$HOME/.codex/skills [codex]")
  [[ -d "$HOME/.cursor/rules" ]] && dirs+=("$HOME/.cursor/rules [cursor]")
  [[ -d "./.cursor/rules" ]] && dirs+=("./.cursor/rules [cursor-local]")
  [[ -d "$HOME/.windsurf/rules" ]] && dirs+=("$HOME/.windsurf/rules [windsurf]")
  [[ -d "./.windsurf/rules" ]] && dirs+=("./.windsurf/rules [windsurf-local]")
  [[ -d "$HOME/.continue/rules" ]] && dirs+=("$HOME/.continue/rules [continue]")
  [[ -d "./skills" ]] && dirs+=("./skills [local]")
  [[ -d "./.agents/skills" ]] && dirs+=("./.agents/skills [agents]")
  [[ -d "$HOME/.agents/skills" ]] && dirs+=("$HOME/.agents/skills [agents-global]")
  printf "%s\n" "${dirs[@]}"
}

# List all skills across all platforms
detect_skill_dirs | while IFS=' ' read -r dir platform; do
  platform="${platform//[\[\]]/}"
  for skill_dir in "$dir"/*/; do
    [ -d "$skill_dir" ] || continue
    skill_name=$(basename "$skill_dir")
    skill_md="$skill_dir/SKILL.md"
    [ ! -f "$skill_md" ] && skill_md="$skill_dir/README.md"
    description=""
    [ -f "$skill_md" ] && description=$(grep -m1 '^description:' "$skill_md" 2>/dev/null \
      | sed 's/^description: *//' | tr -d '"')
    echo "platform=$platform | name=$skill_name | description=$description"
  done
done
```

### Response shape

```
platform=openclaw    | name=telegram-bot | description=Use when sending Telegram notifications...
platform=claude-code | name=skill-finder | description=Multi-source skill discovery...
platform=cursor      | name=my-rule      | description=Project coding conventions
```

### Notes

- Skills here are already installed — no install action needed
- These always appear first in FIND results (rank 1)
- `STATUS` command primarily uses this source
- Cursor/Windsurf may use `.md` or `.mdc` files directly in rules directories instead of subdirectories

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

---

## Platform Compatibility

skill-finder supports installing skills to all major AI coding platforms. Each platform has its own convention for where skills/rules live.

### Supported Platforms

| Platform | Slug | Global Skills Dir | Local (project) Skills Dir | Skill Format |
|----------|------|-------------------|----------------------------|--------------|
| **OpenClaw** | `openclaw` | `~/.openclaw/skills/` | `./skills/` (or `$OPENCLAW_SKILLS_DIR`) | `SKILL.md` + scripts |
| **Claude Code** | `claude-code` | `~/.claude/skills/` | `./.claude/skills/` | `SKILL.md` + scripts |
| **Codex (OpenAI)** | `codex` | `~/.codex/skills/` | `AGENTS.md` in project root | `SKILL.md` or `AGENTS.md` |
| **Cursor** | `cursor` | `~/.cursor/rules/` | `./.cursor/rules/` | `.md` or `.mdc` rule files |
| **Windsurf** | `windsurf` | `~/.windsurf/rules/` | `./.windsurf/rules/` | `.md` rule files |
| **Continue** | `continue` | `~/.continue/rules/` | — | `.md` rule files |
| **Aider** | `aider` | — | `.aider.conf.yml` conventions | Config-driven |
| **Generic** | `local` | `~/.agents/skills/` | `./.agents/skills/` or `./skills/` | `SKILL.md` |

### Detection Logic

A platform is considered "installed" (and therefore a valid install target) when its skill/rules directory exists on the filesystem. Detection runs left-to-right on these conditions:

```
OpenClaw     → ~/.openclaw/skills/ exists
Claude Code  → ~/.claude/skills/ OR ./.claude/skills/ exists
Codex        → ~/.codex/skills/ exists OR AGENTS.md exists in project root
Cursor       → ~/.cursor/rules/ OR ./.cursor/rules/ exists
Windsurf     → ~/.windsurf/rules/ OR ./.windsurf/rules/ exists
Continue     → ~/.continue/rules/ exists
Local        → ./skills/ OR ./.agents/skills/ OR ~/.agents/skills/ exists
```

### Per-Platform Install Notes

**Claude Code**: Skills installed to `~/.claude/skills/<name>/` work identically to OpenClaw. `SKILL.md` format is shared.

**Codex**: Uses `AGENTS.md` convention at project root. When installing to Codex, skill-finder appends the skill's description and trigger conditions to `AGENTS.md` if it exists, or creates a skill directory at `~/.codex/skills/<name>/`.

**Cursor**: Rules live as individual `.md` or `.mdc` files in the rules directory (not subdirectories). skill-finder maps `SKILL.md` → `~/.cursor/rules/<skill-name>.md`.

**Windsurf**: Same convention as Cursor. Maps `SKILL.md` → `~/.windsurf/rules/<skill-name>.md`.

**Continue**: Rules are `.md` files in `~/.continue/rules/`. Maps `SKILL.md` → `~/.continue/rules/<skill-name>.md`.

**Aider**: Skill conventions are appended to `.aider.conf.yml` in the project directory. skill-finder reads the SKILL.md and generates a compatible config block.

### Adding a custom platform path

Set environment variables to extend detection:

```bash
export OPENCLAW_SKILLS_DIR="/custom/path/to/skills"   # Extra OpenClaw path
# skill-finder will include this path in all detection and install operations
```
