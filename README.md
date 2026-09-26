# landit-assets

Static asset host for LANDIT — brand assets (logos, icons, fonts, colour tokens, templates) and email-signature files. Served publicly at **https://asset.landit.com.au/**.

- **Humans:** start at https://asset.landit.com.au/ (index of every brand and asset area).
- **AI agents:** start at https://asset.landit.com.au/llms.txt, or point them at the brand guide https://asset.landit.com.au/brand/landit/AGENTS.md.

## Purpose

- Host static assets whose public URL must stay stable forever (a sent email signature can never be updated).
- Keep asset management simple: files in the repo map 1:1 to public URLs.

## Deployment

GitHub Pages serves the `main` branch root directly — no build step. Merging to `main` redeploys automatically, usually within a minute.

- `CNAME` pins the `asset.landit.com.au` custom domain.
- `.nojekyll` keeps Pages serving files verbatim (no Jekyll processing, so dotfiles and `_`-prefixed paths deploy).
- `index.html` is the human index of every brand and asset area. `llms.txt` is the agent index for every brand. It's closed to search engines because it names non-LANDIT brands. Email signatures are deliberately excluded from it because they contain personal contact details.
- `robots.txt` keeps HTML pages unindexed and LANDIT brand files crawlable, and closes signature pages to every crawler and AI agent (images stay fetchable so mail clients render them). Only the LANDIT brand is open to search; other brands, `llms.txt` and the repo docs are closed to search but open to agents a person points at the site.

## Repository structure

- `brand/landit/` — LANDIT brand: `logo/`, `icons/`, `fonts/`, `favicon/`, `social/`, `templates/`, `guideline/`, `tokens.css`/`tokens.json`, a browsable `index.html` and the agent-readable `AGENTS.md`. Other brands get sibling folders (`brand/<brand>/`). These are hidden from search but listed in `llms.txt` and the human index, so people and agents can still use them.
- `email/` — email-signature HTML templates + images (`email/realtisan/` for Realtisan-brand signatures). `email/index.html` is the human-only list of signatures.

Example:

- `email/jack.png` → `https://asset.landit.com.au/email/jack.png`
- `brand/landit/logo/landit-logo-color.svg` → `https://asset.landit.com.au/brand/landit/logo/landit-logo-color.svg`

## Usage

Reference assets by absolute URL — the repo path becomes the URL path:

```html
<img src="https://asset.landit.com.au/email/jack.png" alt="Jack" />
```

## File naming and path rules

- **Never rename, move, or delete a published asset** — its URL is embedded in places that can't be updated (sent emails, third-party sites).
- Keep names lowercase and hyphenated, no spaces — the filename becomes a permanent public URL.
- New asset categories get their own top-level folder (e.g. `brand/`); new brands inside a category get a subfolder.
- If you add an asset, place it in the correct folder and use a clear, stable filename.

## Adding or updating assets

Work happens on a branch, merged via PR (see `AGENTS.md` for the conventions agents follow):

```bash
git checkout -b chore-add-email-signature
git add email/new-image.png
git commit -m "chore: Add email signature asset email/new-image.png"
```

Every change that adds a file must also update the relevant indexes in the same PR: the brand `AGENTS.md` and `index.html` for brand files, plus `llms.txt` and the root `index.html` for new brands or areas. A new signature goes on `email/index.html` only, **never** `llms.txt`. See the link-integrity rule in `AGENTS.md`. After merging, verify the asset loads at `https://asset.landit.com.au/<path>` before referencing it.

## Notes

- This repo is for static assets only, not source code, and is **public by design** — never commit secrets or unreleased material.
- Broken images in email signatures almost always mean the filename or path changed.
