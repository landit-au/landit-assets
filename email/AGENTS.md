# email/ — signature assets

Read alongside the root `AGENTS.md`; the published-URL immutability rule applies hardest here — once a signature is sent, its image URL is frozen forever.

**Live files — never rename, move, or delete:** `jack.png` and `elaine.png` at this folder's root are hard-coded into `generic/signature.html` and `generic/signature-elaine.html`, which are already pasted into third-party email systems. Every open of those emails fetches `https://asset.landit.com.au/email/jack.png` / `https://asset.landit.com.au/email/elaine.png` — those paths must keep serving.

Signature HTML files are copy-paste templates rendered by recipients' mail clients: table layout, fully inline styles only — no external CSS, no `<link>`, no `<style>` reliance, no scripts. Every `img src` must be an absolute `https://asset.landit.com.au/...` URL.

Layout:

- `generic/signature.html` / `generic/signature-elaine.html` — LANDIT-brand signatures, each pairing with a portrait at this folder's root (`jack.png`, `elaine.png`)
- `realtisan/` — Realtisan-brand signatures (`jack.html`); one subfolder per brand
- `signature.html` / `signature-elaine.html` at this folder's root — redirect stubs (meta-refresh → `generic/…`) preserving the pre-`generic/` URLs; not templates to copy

Adding a signature:

1. Add the portrait/logo image here (or the brand subfolder) — the filename becomes a permanent public URL, so pick it carefully.
2. Copy an existing signature HTML as the template and edit the details; don't restructure the tables.
3. After merge, verify the image loads at `https://asset.landit.com.au/<path>` before pasting the signature into a mail client.
