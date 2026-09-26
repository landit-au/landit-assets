# landit-assets — Project Context

> **Note:** `CLAUDE.md` is a symlink to `AGENTS.md`. They are the same file.

Static asset host for LANDIT — brand assets (logos, icons, fonts, tokens, templates) and email-signature files. Plain HTML + media files, no dependencies, no build step.

## Where to look

This file holds only cross-cutting guidance. Area-specific rules live in a nested `AGENTS.md` next to the content they describe (each with its own `CLAUDE.md` symlink) — the nearest file to what you're editing applies on top of this one:

| Area | File |
| ---- | ---- |
| Email signatures (HTML templates + hotlinked images, per-brand folders) | `email/AGENTS.md` |
| LANDIT brand guide — colours, logo, type, icons, voice, brand asset map | `brand/landit/AGENTS.md` |

Brand assets live in `brand/<brand>/` (`brand/landit/` primary; other brands get sibling folders with the same layout: `AGENTS.md`, `index.html`, `logo/`, `icons/`, `fonts/`, …). **Only LANDIT shows up in search.** Other brands are hidden from search but fully usable by people and agents:
- List them in `llms.txt` (under *Other brands*) and on the root `index.html` (with `rel="nofollow"`).
- `robots.txt` closes `/brand/*` (except `/brand/landit/`) and `llms.txt` itself to search engines and AI crawlers. New brand folders are covered automatically.
- Assistants a person points at the site can still read everything except `/email/`. Brand files are exported from the masters in LANDIT's Google Drive, never hand-drawn here.

## Deployment

GitHub Pages serves this repo at **https://asset.landit.com.au/** (public repo `github.com/landit-au/landit-assets`, Pages source = `main` branch root, legacy build). There is no CI or build step: **merging to `main` is the deploy** — GitHub republishes automatically, usually within a minute. Files are served verbatim, so a repo path is the public URL path: `email/jack.png` → `https://asset.landit.com.au/email/jack.png`.

- `CNAME` pins the custom domain.
- **Entry points** — the only URLs external docs (Drive README, other repos) should hard-code, so they survive reorganisation:
  - `index.html` — human index of every brand and asset area.
  - `llms.txt` — machine-readable index for AI agents ([llmstxt.org](https://llmstxt.org) format).
- `robots.txt` has three groups. Test any change against them, and keep new file types and AI user agents in the right group. The rules are longest-match, and on a tie `Allow` wins.
  - **All crawlers (`*`):** `*.html` pages and everything under `/email/` are closed. `Disallow: /email/*` is one character longer than `Allow: /*.png$`, so it wins. Brand images stay crawlable. Email clients aren't crawlers and ignore `robots.txt`, so signatures still render. Other brands (`/brand/*` except `/brand/landit/`), `llms.txt` (it names them) and the repo docs (`/AGENTS.md`, `/README.md`, `/CLAUDE.md`) are closed too.
  - **AI crawlers and AI search** (GPTBot, ClaudeBot, PerplexityBot, …): the same, plus all of `/email/`. This group has no image `Allow` lines, because `Allow: /*.png$` would tie with `Disallow: /email/` and re-open signature images.
  - **User-triggered AI assistants** (Claude-User, ChatGPT-User, Perplexity-User), which only fetch because a person asked: may read `llms.txt` and every brand, never `/email/`.
- `.nojekyll` disables Pages' Jekyll processing so every file (including dotfiles and `_`-prefixed paths) deploys verbatim — keep it.

## The core invariant: published URLs are immutable

Assets are referenced by absolute URL from places that can never be updated afterwards — email signatures already sent, third-party sites, documents. **Never rename, move, or delete a published asset.** Adding files is always safe. Overwriting a file's *contents* at the same path updates future fetches, but already-delivered emails may keep showing a cached copy — when in doubt, publish a new path instead.

- New asset categories get their own top-level folder (e.g. `brand/` for the brand guidelines); new brands inside a category get a subfolder (`email/realtisan/`).
- Filenames: lowercase, hyphenated, no spaces — the filename becomes a permanent public URL.
- HTML that references assets (signatures, future pages) must use absolute `https://asset.landit.com.au/...` URLs, never relative paths — the HTML gets copied into contexts where relative paths break.

## Link integrity: no broken links for humans or AI

Several files index the others, so every add, rename or removal must update them **in the same PR**:

| When you change… | Also update |
| ---------------- | ----------- |
| Any file or path under `brand/<brand>/` | That brand's `AGENTS.md` (Asset map) and `index.html` |
| A signature under `email/` | `email/index.html` only (human-only; see the exception below) |
| LANDIT or a new asset area, or a file linked from the indexes | `llms.txt` and root `index.html` |
| A new non-LANDIT brand | `llms.txt` (*Other brands* section) and root `index.html` (`rel="nofollow"`) |
| A top-level folder or convention | This file's "Where to look" table and `README.md` |
| An exported asset's name or layout | The export script in Drive (`_export/export_brand.py`) and the Drive `AGENTS.md`, so the next export matches |

`llms.txt` and the root `index.html` must cover the same **areas** (every brand and asset area): one index for agents, one for humans. Neither needs every file: per-file links live in each brand's `AGENTS.md` asset map and `index.html`. `llms.txt` may also deep-link a few key files (tokens, primary logo) for agents.

**Exception: email signatures are human-only.** They contain personal contact details (names, mobile numbers, emails). List them only on `email/index.html` (the root `index.html` links to that page, not to individual signatures), with `rel="nofollow"`. **Never** add them to `llms.txt`, a brand `AGENTS.md`, or anything written for agents or search. `robots.txt` closes `/email/` to every crawler and AI agent; keep it that way.

Renames and removals of published paths are still forbidden (see above). When a new path supersedes an old one, keep the old file and point the indexes at the new one.

Before opening the PR, check that every absolute URL in the indexes, pages and `fonts.css` maps to a file in the repo (prints nothing when clean). If you add a new index page or stylesheet, add it to this command:

```bash
grep -ohE 'https://asset\.landit\.com\.au/[^]"'"'"'`)<> ]*' llms.txt index.html */index.html */AGENTS.md brand/*/AGENTS.md brand/*/index.html brand/*/fonts/fonts.css \
  | sed -E 's/[.,:;]+$//' | sort -u | sed 's|https://asset.landit.com.au/||' \
  | while read -r p; do [ -e "${p:-index.html}" ] || [ -e "${p}index.html" ] || echo "MISSING: $p"; done
```

After merging, re-run it against the live site by swapping the test for `curl -s -o /dev/null -w '%{http_code}' "https://asset.landit.com.au/$p"`, and expect `200`.

## Git Conventions

Same trunk-based flow as `landit-digital`:

- **Branch + PR only** — nobody commits directly to `main`, including agent sessions.
- Branch names: lowercase, hyphenated, ticket key first (`road-xxx-short-description`); no ticket → `chore-short-description`.
- Commit messages: `ROAD-XXX: Short description` or `chore: Short description`.
- No CI runs here, so draft PRs are optional. Repo settings restrict merging to **rebase only** (squash and merge-commit disabled, same as `landit-digital`) — `gh pr merge --rebase`, then spot-check the asset URL over HTTPS.

## Conventions

- This repo is **public by design** — email clients must fetch images without auth. Never commit anything private: no secrets, no unreleased material.
- Keep it static: no frameworks, no `package.json`, no build tooling. Pages use embedded CSS; they may link this site's own `tokens.css` / `fonts.css` (email signatures stay fully inline — see `email/AGENTS.md`).
- **Placement rule:** cross-cutting → this file; folder-specific → the nearest nested `AGENTS.md` (create one with a sibling `CLAUDE.md -> AGENTS.md` symlink if missing); multi-step workflow → a skill in `.agents/skills/<name>/SKILL.md` with a `.claude/skills -> ../.agents/skills` symlink — same pattern as `landit-digital`.
