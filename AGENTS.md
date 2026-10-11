# landit-assets — Agent context

> `CLAUDE.md` is a symlink to this file.

Dumb static file host for LANDIT's public assets at **https://asset.landit.com.au/** (GitHub Pages, `main` branch root). No CI, no build step — merging to `main` is the deploy. Repo path = URL path.

## The core invariant: published URLs are immutable

Assets are referenced from places that can't be updated — sent email signatures hotlink `email/*.png`, EDMs hotlink `brand/landit/logo/*`. **Never rename, move, or delete a published path.** Adding files is always safe; overwriting contents at the same path works, but delivered emails may keep a cached copy — when in doubt, publish a new path.

- Filenames: lowercase, hyphenated, no spaces.
- HTML referencing assets must use absolute `https://asset.landit.com.au/...` URLs, never relative paths.

## Knowledge lives in landit-brain

The brand guide and email-signature templates are private, in `landit-au/landit-brain`: `knowledge/guidelines/brand.md` and the `assets/` registry. Don't write guides or templates into this repo — it only holds the public binaries.

## Indexes and link integrity

`index.html` (humans) and `llms.txt` (agents) index the public areas; a new area updates both in the same PR. Before opening a PR, check every absolute URL still maps to a file (prints nothing when clean):

```bash
grep -ohE 'https://asset\.landit\.com\.au/[^]"'"'"'`)<> ]*' llms.txt index.html */index.html brand/*/index.html brand/*/fonts/fonts.css \
  | sed -E 's/[.,:;]+$//' | sort -u | sed 's|https://asset.landit.com.au/||' \
  | while read -r p; do [ -e "${p:-index.html}" ] || [ -e "${p}index.html" ] || echo "MISSING: $p"; done
```

## Conventions

- Branch + PR only — nobody commits to `main`. Branches: lowercase-hyphenated, ticket first (`gh-4-...`); no ticket → `chore-...`. Commits: `GH-4: ...` or `chore: ...`. Rebase-only merge; no CI, so draft PRs are optional.
- `robots.txt` in one line: `*.html` pages and `/email/` are closed to crawlers, images stay fetchable (mail clients render them); only `/brand/landit/` is open to search.
- Public repo — never commit secrets or private material. Keep it static: no frameworks, no `package.json`, no build tooling.
