# landit-assets

Static asset host for the LANDIT platform — email-signature images, logo files, and (planned) a static version of the brand guidelines. Served publicly at **https://asset.landit.com.au/**.

## Purpose

- Host static assets whose public URL must stay stable forever (a sent email signature can never be updated).
- Keep asset management simple: files in the repo map 1:1 to public URLs.

## Deployment

GitHub Pages serves the `main` branch root directly — no build step. Merging to `main` redeploys automatically, usually within a minute.

- `CNAME` pins the `asset.landit.com.au` custom domain.
- `.nojekyll` keeps Pages serving files verbatim (no Jekyll processing, so dotfiles and `_`-prefixed paths deploy).
- `index.html` is a landing page that redirects to https://landit.com.au/ — not an asset index.
- `robots.txt` keeps HTML pages unindexed while allowing image files to be crawled.

## Repository structure

- `email/` — email-signature HTML templates + images (`email/realtisan/` for Realtisan-brand signatures)

Example:

- `email/jack.png` → `https://asset.landit.com.au/email/jack.png`

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

After merging, verify the asset loads at `https://asset.landit.com.au/<path>` before referencing it.

## Notes

- This repo is for static assets only, not source code, and is **public by design** — never commit secrets or unreleased material.
- Broken images in email signatures almost always mean the filename or path changed.
