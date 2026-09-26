# email/ — signature assets

Read alongside the root `AGENTS.md`; the published-URL immutability rule applies hardest here — once a signature is sent, its image URL is frozen forever.

**Live files — never rename, move, or delete:** `jack.png` and `elaine.png` at this folder's root are hard-coded into `generic/signature.html` and `generic/signature-elaine.html`, which are already pasted into third-party email systems. Every open of those emails fetches `https://asset.landit.com.au/email/jack.png` / `https://asset.landit.com.au/email/elaine.png` — those paths must keep serving.

**Privacy: signatures are human-only.** They contain personal contact details. Link them only from `email/index.html` (with `rel="nofollow"`). The root `index.html` links to that page but never to individual signatures, and `email/index.html` carries a `noindex` meta tag. Never list them in `llms.txt`, brand guides or other agent-facing indexes. `robots.txt` blocks AI crawlers from this folder, and all crawlers from `*.html`. Don't add `<meta>` robots tags to the signature files: they're fragments pasted into mail clients, so the tag would end up inside people's signatures.

Signature HTML files are copy-paste templates rendered by recipients' mail clients: table layout, fully inline styles only — no external CSS, no `<link>`, no `<style>` reliance, no scripts. Every `img src` must be an absolute `https://asset.landit.com.au/...` URL.

Layout:

- `generic/signature.html` / `generic/signature-elaine.html` — LANDIT-brand signatures, each pairing with a portrait at this folder's root (`jack.png`, `elaine.png`)
- `realtisan/` — Realtisan-brand signatures (`jack.html`); one subfolder per brand
- `index.html` — human-only list of every signature. Add each new signature here.

Adding a signature:

1. Add the portrait/logo image here (or the brand subfolder) — the filename becomes a permanent public URL, so pick it carefully.
2. Copy an existing signature HTML as the template and edit the details; don't restructure the tables.
3. Add a link to it on `email/index.html` (`rel="nofollow"`). Don't add it to `llms.txt` or the root index.
4. After merge, verify the image loads at `https://asset.landit.com.au/<path>` before pasting the signature into a mail client.
