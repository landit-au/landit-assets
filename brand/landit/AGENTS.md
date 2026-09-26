# brand/landit/ — LANDIT brand guide for agents

> `CLAUDE.md` is a symlink to `AGENTS.md`. Read alongside the root `AGENTS.md` (URL immutability, link integrity, naming, git flow).

The agent-readable LANDIT brand guide, plus the map of every published brand asset. Follow it when building anything on-brand: landing pages, EDMs, the web app, decks, social posts.

- **This file:** `https://asset.landit.com.au/brand/landit/AGENTS.md`. The human-browsable version is `https://asset.landit.com.au/brand/landit/`.
- **Index of all brands and assets:** `https://asset.landit.com.au/llms.txt`
- **Source of truth for artwork:** the designer's master files and the guideline PDF, kept in LANDIT's internal Google Drive (`Marketing/LANDIT/`). Everything here is exported from there with `_export/export_brand.py`; never hand-edit exported files.
- **Precedence:** the guideline PDF > this file > any other LANDIT repo. Other LANDIT repos may predate this guide; don't copy their styling.
- Items marked **(proposed)** fill gaps the PDF doesn't cover. Use them, but they may change.

## Using this brand in a project

Add one line to the consuming project's `AGENTS.md`:

```md
Brand: follow https://asset.landit.com.au/brand/landit/AGENTS.md. Use the published asset URLs and tokens.css; don't redraw logos or icons.
```

- Hotlink or download assets from the URLs below; never recreate the logo or icons from scratch.
- Load `tokens.css` and `fonts/fonts.css`, or copy the token values into the project's theme.

## Brand at a glance

- **LANDIT** is a Sydney real-estate business: property solutions across **House · Land · Investment**.
- **Tagline:** "Land your dream house"
- **Name:** always `LANDIT` in copy. Never "Landit", "LandIt" or "Land it" (a legacy concept name). Use lowercase `landit` only in URLs, slugs and handles.
- **Domain:** `https://landit.com.au`

## Which format to use

| Medium | Logos | Icons | Notes |
| ------ | ----- | ----- | ----- |
| Web app (React, Next.js) | SVG | Inline SVG: `icons/svg/<name>.svg`, imported as components (e.g. SVGR) and coloured with CSS `color` | `currentColor` only recolours when the SVG is inlined or used as a CSS mask |
| Landing pages (HTML) | SVG | Inline SVG, or `icons/svg/<name>-<colour>.svg` in an `<img>` | An `<img>` can't inherit `color`: `<name>.svg` would render black, so use a fixed-colour file |
| EDM (email) | `logo/<variant>@2x.png`, shown at half its pixel width | `icons/png/<name>-<colour>.png` | Gmail and Outlook don't render SVG reliably. Absolute URLs only, inline styles |
| Print | SVG (vector, any size), or the PDF/EPS masters in Drive | SVG | Never the web PNGs; they're screen resolution |
| Docs and slides | PNG @2x, or SVG where supported | PNG or SVG | Start decks from `templates/landit-deck-template.pptx` |
| Favicons and app icons | `favicon/` set | — | See the Asset map |

## Colour

| Token | Hex | RGB | CMYK | Role |
| ----- | --- | --- | ---- | ---- |
| `--landit-red` | `#D31E31` | 211 30 49 | 11 100 89 2 | Brand accent: logo mark, icons, primary CTA, highlights |
| `--landit-navy` | `#1A1B26` | 26 27 38 | 80 74 56 71 | Brand "black": all text, impact surfaces |
| `--landit-white` | `#FFFFFF` | — | — | Default surface |

The PDF's red swatch label says `#021D42`. That is a typo; `#D31E31` is correct and matches the logo files.

**Tints** (from the PDF: 10–50% mixes with white):

| Step | Red | Navy |
| ---- | --- | ---- |
| 90 | `#D73446` | `#31323C` |
| 80 | `#DB4B5A` | `#474851` |
| 70 | `#E0616F` | `#5F5F67` |
| 60 | `#E47883` | `#75767C` |
| 50 | `#E88E97` | `#8C8C92` |

(proposed) Use `--landit-surface-alt: #F4F4F5` (navy at 5%) for alternating sections and cards on white. Don't use pure black (`#000`), extra hues, or gradients.

### Two surface modes

**Default (light): most places.** EDM body, web and app UI, navigation, forms, documents, print body.
White background · navy text · red for the mark, icons, links and primary CTA. Rough balance: 60% white, 30% navy, 10% red.

**Impact (navy): where it needs to land.** Hero and header bands, EDM header, social banners and tiles, print covers, business-card back, deck title slides.
Navy background · white text · red mark and iconography. Use `landit-logo-color-reversed`.

**Red surfaces are allowed but rare.** Use them for a single CTA band, a "Sold / Just listed" badge, or a small icon tile. Only white goes on red: use the white logo and white text.

This follows the PDF's compatibility matrix (page 06): white takes navy and red; navy takes white and red; red takes white only.

### Contrast rules (WCAG AA)

| Pair | Ratio | Allowed for |
| ---- | ----- | ----------- |
| Navy on white | 17.1:1 | everything |
| White on navy | 17.1:1 | everything |
| Red on white | 5.3:1 | body text, links, buttons |
| White on red | 5.3:1 | button labels, badges |
| Red on navy | 3.3:1 | **large text (≥ 24 px) and graphics only**; never body copy |
| Navy 70 `#5F5F67` on white | 6.4:1 | secondary / muted text (the lightest tint allowed for text) |
| Navy 50 `#8C8C92` on white | 3.4:1 | borders, disabled states, never text |

### Components (proposed)

- **Primary button:** red background, white label. Hover: red 90.
- **Secondary button:** navy 1.5 px outline, navy label (white outline and label on navy).
- **Links:** red; underline on hover.
- **Headings:** navy by default. Red only for a single highlighted word or short line.

## Logo

| Variant | Mark / wordmark | Use on |
| ------- | --------------- | ------ |
| `landit-logo-color` (**primary**) | red / navy | white and light surfaces |
| `landit-logo-color-reversed` | red / white | navy |
| `landit-logo-white` | white / white | red, or busy photography |
| `landit-logo-navy` | navy / navy | single-colour light applications |
| `landit-mark-red` | red roof-"LA" symbol | avatars, small spaces, on white or navy |
| `landit-mark-white` | white | red or navy |
| `landit-mark-navy` | navy | single-colour light applications |

- **Files:** `logo/<variant>.svg`, `logo/<variant>.png` (lockups 400 px wide, marks 256 px) and `logo/<variant>@2x.png` (800 px / 512 px). Lockup files are cropped tight to the artwork. Mark files are square with built-in padding.
- **Clear space:** at least 24 px on every side. Nothing enters that zone.
- **Minimum size:** full lockup at least **120 px wide on screen** and **30 mm wide in print**. Below that, use the mark alone, at least **16 px**. The PDF's "100 px / 75 px height" figure refers to its 1920 px slide canvas and is superseded by this rule.
- **Don'ts (PDF page 09):** don't stretch or squeeze it; don't rearrange it; don't rotate it; don't recolour it outside the variants above; don't place it where it's hard to read; don't add effects (shadow, glow, outline, gradient).

## Typography

Two families, **five weights**. Poppins is the voice of headings; Montserrat is everything you read. The guideline PDF (page 07) sets the roles. The weights come from the designer's own applications: stationery, email signature and letterhead use Montserrat Regular + SemiBold, and guideline headings use Poppins Medium.

| Weight | Font | Use for |
| ------ | ---- | ------- |
| **500 Medium** | Poppins | Headings H2–H4, card and section titles |
| **700 Bold** | Poppins | Display / H1, hero lines, social and cover titles, key figures (prices, stats) |
| **400 Regular** | Montserrat | Body copy, descriptions, form input text, captions and legal text |
| **500 Medium** | Montserrat | Nav links, form labels, tags, metadata |
| **600 SemiBold** | Montserrat | Buttons, emphasis in body (`<strong>`), names in signatures, eyebrows |

These five are the only weights published in `fonts/fonts.css`. The Drive has the full families for designers, but no other weight is on-brand.

### Web and app scale

| Style | Font / weight | Desktop | Mobile | Line height | Notes |
| ----- | ------------- | ------- | ------ | ----------- | ----- |
| Display | Poppins 700 | 56 px | 36 px | 1.1 | One per page, hero only; may tighten to `-0.01em` |
| H1 | Poppins 700 | 40 px | 32 px | 1.15 | Page title |
| H2 | Poppins 500 | 32 px | 26 px | 1.2 | Section heading |
| H3 | Poppins 500 | 24 px | 20 px | 1.3 | Sub-section / card title |
| H4 | Poppins 500 | 20 px | 18 px | 1.3 | Small heading |
| Figure | Poppins 700 | 24–32 px | 20–24 px | 1.2 | Prices, stats, bed/bath counts |
| Lead | Montserrat 400 | 20 px | 18 px | 1.6 | Intro paragraph under a heading |
| Body | Montserrat 400 | 16–18 px | 16 px | 1.6 | Default text; never below 16 px on mobile |
| Label / nav | Montserrat 500 | 14–16 px | 14–16 px | 1.4 | Form labels, nav, tags |
| Button | Montserrat 600 | 16 px | 16 px | 1 | 14 px for small buttons |
| Eyebrow | Montserrat 600 | 13 px | 12 px | 1.4 | Uppercase, `0.08em` tracking, red, above a heading |
| Caption / legal | Montserrat 400 | 13–14 px | 12–13 px | 1.5 | Disclaimers ("Exclusions" in the PDF), image credits; 12 px minimum |

Set the CSS explicitly: browsers default `h2`–`h6` and `<strong>` to 700. Use `--landit-weight-*` from `tokens.css`: headings 500, `strong` 600.

### EDM (email)

- **Headline:** Poppins 700, 28–32 px.
- **Sub-heading:** Poppins 500, 20–22 px.
- **Body:** Montserrat 400, 16 px on a 24 px line height.
- **Button:** Montserrat 600, 16 px.
- **Footer / legal:** Montserrat 400, 12–13 px.
- **Font loading:** Outlook and Gmail ignore web fonts, so always declare the fallback stack. Check the layout in Arial.
- **Headlines stay live text:** never bake text into images just to keep the font.

### Print and decks

- **Decks** (1920 × 1080, from the PDF):
  - Heading: Poppins 700, 70–80 pt.
  - Sub-heading: Poppins 500, 36–50 pt.
  - Body: Montserrat 400, 16–20 pt.
  - Buttons and captions: Montserrat 500/600, 12–20 pt.
- **A4 print:**
  - Headings: Poppins 700, 24–36 pt.
  - Sub-headings: Poppins 500, 14–18 pt.
  - Body: Montserrat 400, 9–11 pt.
  - Captions and legal: Montserrat 400, 7–8 pt (7 pt minimum).
- **Stationery** follows the designer's files: Montserrat 400, with names in 600.

### Do

- Use Poppins for headings and figures, and Montserrat for everything else.
- Stick to the five weights. Make hierarchy with size and weight, not new fonts or colours.
- Use sentence case for headings and buttons ("Book an inspection", not "Book An Inspection").
- Left-align body copy. Centre only short display lines and single CTAs.
- Keep lines to 60–75 characters, and keep text navy. Red is for eyebrows or one highlighted word (≥ 24 px when on navy; see Contrast rules).
- For emphasis in body, use Montserrat 600 or a red link, not italics.
- Load fonts with `fonts/fonts.css` and always include the fallback stack.

### Don't

- Don't set body copy in Poppins, or headings in Montserrat. The guideline slides and the deck template both do this; it's a known inconsistency, and page 07's roles win.
- Don't use other weights (Thin, ExtraLight, Light, SemiBold Poppins, Bold/ExtraBold/Black Montserrat), and don't let the browser fake bold or italic. Italics aren't part of the system.
- Don't use other fonts. LEMONMILK (social templates), Calibri/Arial (deck theme) and Myriad (PDF labels) are off-system. Arial and Helvetica are only fallbacks.
- Don't type "LANDIT" in Poppins in place of the logo: the wordmark is artwork. Use the logo files.
- Don't set whole sentences or headings over four words in capitals, and don't letter-space lowercase text.
- Don't stretch, condense, outline, shadow or gradient-fill text.
- Don't go below 16 px for body text or 12 px for any text on screen, or 7 pt in print.

**Fallback stacks:** `'Poppins', 'Helvetica Neue', Arial, sans-serif` and `'Montserrat', 'Helvetica Neue', Arial, sans-serif`. Both families are SIL OFL 1.1 (free for commercial use); the licences are at `fonts/OFL-*.txt`.

## Iconography

- Custom line icons: 2 pt stroke on a 24 px grid. All share one scale, so stroke weights match at any size.
- **Colour:** navy on light, white on navy, red for emphasis. A red rounded-square tile with a white glyph is also allowed, as on the stationery.
- **18 icons:** `bath` `bed` `car` `garage` `globe` `handshake` `location` `mail` `map-pin` `megaphone` `phone` `settings` `shield-check` `shower` `toilet` `toilet-paper` `user` `wardrobe`
- **Files per icon:**
  - `icons/svg/<name>.svg` (`fill="currentColor"`, recolourable)
  - `icons/svg/<name>-navy.svg`, `-red.svg`, `-white.svg` (fixed colour)
  - `icons/png/<name>-navy.png`, `-red.png`, `-white.png` (96 px, transparent; display at ≤ 48 px)
- **Recolour on the web:** inline the SVG and set `color`, or use it as a mask: `background: var(--landit-navy); mask: url(<name>.svg) center / contain no-repeat;`
- (proposed) When the set lacks an icon, use **Lucide** at `stroke-width="2"`: its style is the closest match. Don't mix in filled or duotone libraries. If an icon is used often, request it from the designer so it joins the set.

## Voice

This covers the public-facing brand register. **Lead-nurture SMS and email** (enquiry follow-ups, callbacks, no-shows) follow the internal *Tone of Voice – Lead Nurture* playbook on Confluence (General space). That playbook is not reproduced here.

1. **Confident, not eager.** State what's on offer plainly. No oversell, no over-thanking, no "happy to help however I can!".
2. **Advisory, not transactional.** Lead with guidance and local expertise, not price pushes or scarcity.
3. **Concise and direct.** Get to the point. Don't pad with filler empathy.
4. **Show, don't claim.** Build credibility through demonstrated experience and specifics, not empty titles ("property consultant") or superlatives ("Sydney's #1").
5. **Professional, not casual.** Plain Australian English (e.g. *neighbourhood*, *enquiry*, *organise*). No slang ("flicking the details through"), no emoji in brand copy.

- **Links:** bare original domain (`landit.com.au/...`), no URL shorteners.
- **Headlines:** plain and specific. No clickbait and no false urgency.
- **Compliance:** don't promise returns or capital growth on investment content, and don't make unverifiable claims ("guaranteed", "best"). Price guides must be genuine (NSW underquoting rules). When unsure, leave the claim out and flag it for review.

## Tokens

`tokens.css` (CSS custom properties) and `tokens.json` (W3C design-tokens format) hold every value above, plus semantic roles (`--landit-text`, `--landit-cta-bg`, etc.). Prefer the semantic roles in components.

## Asset map

Every path below is relative to `https://asset.landit.com.au/brand/landit/`.

| Path | Contents |
| ---- | -------- |
| `index.html` | Human-browsable brand page: swatches, logo downloads, icon grid |
| `AGENTS.md` | This guide |
| `tokens.css`, `tokens.json` | Design tokens |
| `logo/landit-{logo-color,logo-color-reversed,logo-white,logo-navy,mark-red,mark-white,mark-navy}.svg` | Vector logos |
| `logo/<variant>.png`, `logo/<variant>@2x.png` | Transparent raster logos |
| `icons/svg/<name>.svg`, `icons/svg/<name>-{navy,red,white}.svg` | Icons (recolourable / fixed colour) |
| `icons/png/<name>-{navy,red,white}.png` | Icons, 96 px transparent |
| `fonts/fonts.css`, `fonts/poppins-{500,700}.woff2`, `fonts/montserrat-{400,500,600}.woff2`, `fonts/OFL-*.txt` | The five brand weights (WOFF2, Latin) and licences |
| `favicon/favicon.svg`, `favicon.ico`, `favicon-96x96.png`, `apple-touch-icon.png`, `web-app-manifest-{192x192,512x512}.png` | Favicon and app icons (red mark; app icons on navy) |
| `social/{facebook-cover,linkedin-banner,x-header,youtube-banner,instagram-story,profile-picture}-{white,navy,red}.jpg` | Social banners at each platform's upload size |
| `templates/landit-deck-template.pptx` | Branded deck template (18 layouts) |
| `guideline/landit-brand-guideline.pdf` | The brand guideline, compressed for web (the master is 130 MB) |

## Maintaining this folder

- Export from the Drive masters with `_export/export_brand.py` (documented in the Drive folder's `AGENTS.md`). Never hand-edit artwork here.
- Keep filenames lowercase and hyphenated. Never rename or delete a published path; add a new one instead.
- Publish web formats only (SVG, PNG, JPG, WOFF2, compressed PDF, PPTX). Leave `.ai` and `.eps` masters in Drive.
- Keep personal items (portraits, personal QR codes, vCards) out of `brand/`; they belong with their channel (e.g. `email/`).
- Any added, renamed or removed file must be reflected in this file's Asset map, `index.html` and the root `llms.txt` in the same PR (see the root `AGENTS.md` link-integrity rule).
