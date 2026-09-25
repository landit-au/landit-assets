# email/ — signature assets

Read alongside the root `AGENTS.md`; the published-URL immutability rule applies hardest here — once a signature is sent, its image URL is frozen forever.

Signature HTML files are copy-paste templates rendered by recipients' mail clients: table layout, fully inline styles only — no external CSS, no `<link>`, no `<style>` reliance, no scripts. Every `img src` must be an absolute `https://asset.landit.com.au/...` URL.

Layout:

- `signature.html` / `signature-elaine.html` — LANDIT-brand signatures, each pairing with a same-named portrait (`jack.png`, `elaine.png`)
- `realtisan/` — Realtisan-brand signatures (`jack.html`); one subfolder per brand

Adding a signature:

1. Add the portrait/logo image here (or the brand subfolder) — the filename becomes a permanent public URL, so pick it carefully.
2. Copy an existing signature HTML as the template and edit the details; don't restructure the tables.
3. After merge, verify the image loads at `https://asset.landit.com.au/<path>` before pasting the signature into a mail client.
