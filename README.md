# landit-assets

This repository stores static media assets used across email signatures and other places where the asset file name and path must remain stable.

## Purpose

- Host static assets such as signature images.
- Preserve file names and paths so external references do not break.
- Keep asset management simple and predictable.

## Repository structure

- `email/` – email-specific assets

Example:

- `email/jack.png`

## Usage

Use the exact path and filename when embedding assets.

Example HTML for an email signature:

```html
<img src="https://your-cdn.example.com/email/jack.png" alt="Jack" />
```

If the asset is referenced from a local copy or in documentation, keep the same path:

```text
email/jack.png
```

## File naming and path rules

- Do not rename or move files unless you also update every reference.
- Keep names lowercase and avoid spaces when possible.
- Preserve the directory structure.
- If you add a new asset, place it in the correct folder and use a clear, stable filename.

## Adding or updating assets

1. Add the file under the appropriate folder (for example, `email/`).
2. Keep the filename stable and descriptive.
3. Update any references wherever the asset is used.
4. Commit the change with a clear message, such as:

```bash
git add email/new-image.png
git commit -m "Add email signature asset email/new-image.png"
```

## GitHub Pages

This repository is published as a GitHub Pages site. The site uses `index.html` to describe the repository and redirect visitors to `https://landit.com.au/`.

- `index.html` contains a short page explanation and a timed redirect.
- `robots.txt` is configured to discourage indexing of the homepage while allowing access to asset subfolders like `email/`.
- The asset URLs should still resolve normally from their static paths.

## Notes

- This repo is meant for static assets only, not source code.
- Broken images typically mean the filename or path has changed.
- Preserve file paths exactly to avoid rendering issues in email clients.
