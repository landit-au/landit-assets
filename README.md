# landit-assets

Dumb static file host for LANDIT's public assets, served by GitHub Pages at **https://asset.landit.com.au/**. A repo path is the public URL path: `email/jack.png` → `https://asset.landit.com.au/email/jack.png`. No CI, no build step — merging to `main` redeploys within a minute.

- **Humans:** https://asset.landit.com.au/ · **AI agents:** https://asset.landit.com.au/llms.txt
- **Guidelines and templates are private:** the brand guide and email-signature templates live in [landit-brain](https://github.com/landit-au/landit-brain) (`knowledge/guidelines/brand.md`, `assets/`).

## The one rule: published URLs are immutable

Sent email signatures hotlink the portraits; EDM templates hotlink the logo PNGs. Those URLs can never be updated — **never rename, move, or delete a published path.** Adding files is always safe; when in doubt, publish a new path rather than overwrite.

## Layout

- `brand/landit/` — logos, icons, fonts, favicons, social banners, `tokens.css`/`tokens.json`, guideline PDF, deck template, browsable `index.html`
- `email/` — signature portraits only
- `index.html` / `llms.txt` — the human and agent indexes
- `robots.txt` — `*.html` pages closed to crawlers, images open; `/email/` fully closed to AI crawlers

## Adding an asset

Filenames lowercase, hyphenated, no spaces — the name becomes a permanent URL. Branch + PR only (conventions in `AGENTS.md`); update `llms.txt` and `index.html` for new areas in the same PR. This repo is public by design — never commit anything private.
