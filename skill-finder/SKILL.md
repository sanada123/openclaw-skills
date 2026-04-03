---
name: skill-finder
description: "Use when searching for, vetting, or installing OpenClaw skills from any source — ClawHub, GitHub, npm, or local. Replaces skill-hunter with multi-source discovery, security vetting, and one-command installs."
license: MIT
metadata:
  version: "1.0"
  category: utility
  author: "Atlas / ASD-AI"
  sources:
    - https://clawhub.ai
    - https://github.com
    - https://npmjs.com
---

# skill-finder

**Find skills everywhere. Not just ClawHub.**

Multi-source skill discovery: search ClawHub, GitHub, npm, and local skills in one command. Find, vet, and install from anywhere.

---

## Overview

`skill-hunter` only searches ClawHub. **skill-finder** searches 6 sources simultaneously, deduplicates results, ranks by trust, and lets you vet security before installing anything.

| | skill-hunter | skill-finder |
|---|---|---|
| Sources | 1 (ClawHub) | 6 (ClawHub + GitHub + npm + local + more) |
| Security vetting | None | Built-in VET command |
| Install from GitHub | No | Yes |
| Shows local skills | No | Yes |
| Deduplication | No | Yes |

---

## Quick Start

```bash
# Find skills about Telegram
skill-finder: find telegram

# See what's trending on ClawHub this week
skill-finder: scout trending

# Vet a skill before installing
skill-finder: vet telegram-bot

# Install from GitHub instead of ClawHub
skill-finder: install github:sanada123/openclaw-skills/telegram-bot
```

---

## Commands

### FIND — Search everywhere, ranked by trust

```bash
skill-finder: find <query>
```

Searches all 6 sources concurrently, deduplicates by name/slug, and returns ranked results.

**Output columns:**
```
RANK  NAME                SOURCE      DESCRIPTION                    INSTALL
 1    telegram-bot        local       Send Telegram messages         (already installed)
 2    telegram-notifier   our-github  Notify via Telegram            install github:sanada123/openclaw-skills/telegram-notifier
 3    telegram-claude     clawhub     Full Telegram + Claude bot     install telegram-claude
 4    telegram-webhook    npm         Webhook handler for Telegram   install npm:openclaw-skill-telegram-webhook
```

**Ranking logic:**
1. Local installed skills (already have them)
2. Our GitHub (`sanada123/openclaw-skills`) — trusted source
3. ClawHub (ranked by semantic relevance score)
4. GitHub community skills (ranked by stars)
5. npm packages (ranked by weekly downloads)
6. skillsmp.com (if available)

**Options:**
```bash
skill-finder: find telegram --source clawhub     # Single source only
skill-finder: find telegram --top 5              # Limit results
skill-finder: find telegram --safe               # Only SAFE-vetted skills
```

---

### SCOUT — Browse trending and new skills

```bash
skill-finder: scout trending    # Top skills this week across sources
skill-finder: scout newest      # Most recently published
skill-finder: scout popular     # All-time most installed
```

Sources checked: ClawHub trending endpoint + GitHub topic stars + npm weekly downloads.

**Example output:**
```
TRENDING THIS WEEK
  1. n8n-workflow-builder    clawhub    ★ 847   "Build n8n workflows with AI"
  2. mcp-server-builder      clawhub    ★ 623   "Create MCP servers"
  3. openclaw-skill-slack    npm        ↓ 2.1k  "Slack integration toolkit"
```

---

### VET — Security analysis before install

```bash
skill-finder: vet <slug>
skill-finder: vet github:user/repo/path
skill-finder: vet https://raw.githubusercontent.com/...
```

Pulls the SKILL.md and runs a 10-point security checklist.

**Security scorecard:**

| Check | Flag | Points |
|---|---|---|
| Reads env vars (API keys, tokens) | REVIEW | -1 |
| Executes shell commands | REVIEW | -1 |
| Makes outbound network calls | INFO | 0 |
| Calls known-safe APIs only | SAFE | +1 |
| Installs packages at runtime | RISKY | -2 |
| Accesses filesystem outside workspace | RISKY | -2 |
| Contains obfuscated code | RISKY | -3 |
| Has pinned dependency versions | SAFE | +1 |
| Published author has other trusted skills | SAFE | +1 |
| SKILL.md has explicit permissions section | SAFE | +1 |

**Verdicts:**
- **SAFE** (8–10): Install with confidence
- **REVIEW** (5–7): Read the skill carefully before installing
- **RISKY** (0–4): Do not install without understanding exactly what it does

**Example output:**
```
VET REPORT: telegram-bot (clawhub)
Score: 7/10 — REVIEW

Flags:
  [REVIEW] Reads env vars: TELEGRAM_BOT_TOKEN, TELEGRAM_CHAT_ID
  [INFO]   Makes outbound calls: api.telegram.org
  [SAFE]   Author sanada123 has 12 published skills
  [SAFE]   Has explicit permissions section in SKILL.md

Recommendation: Safe to install if you intend to use Telegram. The env vars
it reads are expected for this skill type. Review lines 23-31 of SKILL.md.
```

---

### INSTALL — Install from any source

```bash
# From ClawHub (default)
skill-finder: install <slug>

# From our GitHub skills repo
skill-finder: install github:sanada123/openclaw-skills/<skill-name>

# From any GitHub repo (org/repo/path/to/skill)
skill-finder: install github:<user>/<repo>/<path>

# Copy from local path
skill-finder: install local:</path/to/skill>

# From npm
skill-finder: install npm:<package-name>
```

**Install flow:**
1. Fetch SKILL.md from source
2. Auto-run VET (warn if RISKY, require `--force` to override)
3. Copy to `~/.openclaw/skills/<skill-name>/`
4. Confirm: "Installed skill-name → ~/.openclaw/skills/skill-name/"

**Skip vet (not recommended):**
```bash
skill-finder: install telegram-bot --no-vet
```

---

### STATUS — Inventory of all installed skills

```bash
skill-finder: status
```

Detects and lists all skills from local skill directories (see sources.md for detection logic) with source metadata.

**Example output:**
```
INSTALLED SKILLS (47 total)

LOCAL (workspace):
  telegram-bot        v1.2   clawhub     updated 3 days ago
  n8n-workflow        v2.0   clawhub     updated 1 week ago
  skill-finder        v1.0   local       updated today

USER (~/.openclaw/skills/):
  my-custom-tool      v1.0   local       updated 2 weeks ago

Options:
  skill-finder: status --outdated    # Show skills with updates available
  skill-finder: status --source github   # Filter by source
```

---

## Source Priority Table

| # | Source | Trust Level | Best For |
|---|---|---|---|
| 1 | Local workspace | Highest — you own it | Already installed skills |
| 2 | Our GitHub (`sanada123/openclaw-skills`) | High — your own published skills | Tested, personal skills |
| 3 | ClawHub semantic search | High — curated platform | Discovering quality skills |
| 4 | GitHub topic: `openclaw-skill` | Medium — community | Niche/experimental skills |
| 5 | npm registry | Medium — versioned packages | Skills with dependencies |
| 6 | skillsmp.com | Variable — try, fail gracefully | Alternative marketplace |

---

## Security Framework

**Always vet before installing skills you didn't write.**

The VET command is automatic on INSTALL. To force-install a RISKY skill you've reviewed:
```bash
skill-finder: install <slug> --force --i-reviewed-it
```

**What VET cannot catch:**
- Skills that behave differently based on environment
- Logic that only activates under certain conditions
- Social engineering (skill that tells you to do something harmful)

**Golden rule:** If a skill asks you to run commands outside the workspace, pipe to shell, or export credentials — stop and re-read it.

---

## Rate Limits & Best Practices

| Source | Limit | Notes |
|---|---|---|
| ClawHub | 60 req/min | No auth needed for search |
| GitHub API | 60 req/hour (unauthenticated) | Set `GITHUB_TOKEN` for 5000/hour |
| npm registry | ~1000 req/hour | No auth needed |
| skillsmp.com | Unknown | Fail gracefully if unavailable |

**Set GitHub token for better rate limits:**
```bash
export GITHUB_TOKEN=ghp_yourtoken
# skill-finder automatically uses it if set
```

**Concurrent search:** FIND runs all sources in parallel. Total search time ≈ slowest source response time (~1-2s), not sum of all.

---

## See Also

- `instructions.md` — Full API reference, curl examples, dedup algorithm, security scoring details
- `sources.md` — Per-source documentation with working curl commands
