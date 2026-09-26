# landit-assets — Project Context

> **Note:** `CLAUDE.md` is a symlink to `AGENTS.md`. They are the same file.

Static asset host for the LANDIT platform — email-signature images, logo files, and (planned) a static version of the brand guidelines. Plain HTML + media files, no dependencies, no build step.

## Where to look

This file holds only cross-cutting guidance. Area-specific rules live in a nested `AGENTS.md` next to the content they describe (each with its own `CLAUDE.md` symlink) — the nearest file to what you're editing applies on top of this one:

| Area | File |
| ---- | ---- |
| Email signatures (HTML templates + hotlinked images, per-brand folders) | `email/AGENTS.md` |

## Deployment

GitHub Pages serves this repo at **https://asset.landit.com.au/** (public repo `github.com/landit-au/landit-assets`, Pages source = `main` branch root, legacy build). There is no CI or build step: **merging to `main` is the deploy** — GitHub republishes automatically, usually within a minute. Files are served verbatim, so a repo path is the public URL path: `email/jack.png` → `https://asset.landit.com.au/email/jack.png`.

- `CNAME` pins the custom domain. `index.html` is a landing page that meta-refreshes to `https://landit.com.au/` — it is not an asset index.
- `robots.txt` disallows `*.html` but allows image extensions — pages stay unindexed, asset URLs keep resolving. Keep that split if new file types are added.
- `.nojekyll` disables Pages' Jekyll processing so every file (including dotfiles and `_`-prefixed paths) deploys verbatim — keep it.

## The core invariant: published URLs are immutable

Assets are referenced by absolute URL from places that can never be updated afterwards — email signatures already sent, third-party sites, documents. **Never rename, move, or delete a published asset.** Adding files is always safe. Overwriting a file's *contents* at the same path updates future fetches, but already-delivered emails may keep showing a cached copy — when in doubt, publish a new path instead.

- New asset categories get their own top-level folder (e.g. `brand/` for the brand guidelines); new brands inside a category get a subfolder (`email/realtisan/`).
- Filenames: lowercase, hyphenated, no spaces — the filename becomes a permanent public URL.
- HTML that references assets (signatures, future pages) must use absolute `https://asset.landit.com.au/...` URLs, never relative paths — the HTML gets copied into contexts where relative paths break.

## Git Conventions

Same trunk-based flow as `landit-digital`:

- **Branch + PR only** — nobody commits directly to `main`, including agent sessions.
- Branch names: lowercase, hyphenated, ticket key first (`road-xxx-short-description`); no ticket → `chore-short-description`.
- Commit messages: `ROAD-XXX: Short description` or `chore: Short description`.
- No CI runs here, so draft PRs are optional. Repo settings restrict merging to **rebase only** (squash and merge-commit disabled, same as `landit-digital`) — `gh pr merge --rebase`, then spot-check the asset URL over HTTPS.

## Conventions

- This repo is **public by design** — email clients must fetch images without auth. Never commit anything private: no secrets, no unreleased material.
- Keep it static: no frameworks, no `package.json`, no build tooling. Pages needing styles use inline/embedded CSS.
- **Placement rule:** cross-cutting → this file; folder-specific → the nearest nested `AGENTS.md` (create one with a sibling `CLAUDE.md -> AGENTS.md` symlink if missing); multi-step workflow → a skill in `.agents/skills/<name>/SKILL.md` with a `.claude/skills -> ../.agents/skills` symlink — same pattern as `landit-digital`.
