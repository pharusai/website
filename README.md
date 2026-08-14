# pharus.ai — marketing site

Static landing page for Pharus. **No build step.** Every file here is served as-is
from the repo root.

## Layout

```
index.html            the whole page — inline CSS, zero JavaScript
fonts/*.woff2         Inter + JetBrains Mono, self-hosted (subset by unicode-range)
favicon.svg           Pharus beam mark
apple-touch-icon.png  180×180
og.png                1200×630 social card
robots.txt sitemap.xml
_headers              cache + security headers (Cloudflare Pages / Netlify)
.nojekyll             stops GitHub Pages from stripping _headers
CNAME                 custom domain for GitHub Pages
```

## Editing

`index.html` is a flattened export of the Claude Design source (`Pharus Landing.html`).
It was rendered once and snapshotted, so the markup is plain HTML with inline styles —
edit it directly. Two additions live in `<style>` blocks in `<head>`:

- smooth scrolling + `scroll-margin-top` for the `#why` / `#day` / `#pricing` / `#faq` anchors
- a responsive block (`@media max-width: 700px`) — the design source ships **no**
  media queries, so the header and the "a day with Pharus" timeline rows are
  corrected for phones here. Classes `.ph-hdr`, `.ph-nav`, `.ph-hdr-cta`,
  `.ph-day-row` exist only for those overrides.

If you re-export from Claude Design, re-apply both blocks.

## Local preview

```sh
python3 -m http.server 8000
```

## Links used on the page

| Target | Where |
|---|---|
| `https://app.pharus.ai/new-organization` | self-serve: header "Start free trial", hero, Foundation, Multichannel, closing CTA (5) |
| Google Calendar appointment schedule | sales-assisted: Wholesale "Talk to us", Full operator "Talk to us", "Book a working session" (3) |
| `https://app.pharus.ai` | "Log in" only — header and footer |
| `mailto:marshall@pharus.ai` | footer Contact |
| `#why` `#day` `#pricing` `#top` | nav + footer |

`#faq` exists as a section but nothing links to it yet.

## Mobile

The design source has **no media queries at all**. Three `<style>` blocks in
`<head>` supply them — do not drop these if you re-export:

1. smooth scrolling + `scroll-margin-top` for anchors
2. header/timeline fixes (`.ph-hdr`, `.ph-nav`, `.ph-hdr-cta`, `.ph-day-row`)
3. layout fixes (`.ph-hero-grid`, `.ph-kpi`, `.ph-price-grid`, `.ph-why-grid`,
   `.ph-sec`, `.ph-wrap`)

Without #3 the hero stays a two-column grid on phones and the "Pharus operating
view" card is pushed off-canvas and clipped by the hero's `overflow:hidden` —
invisible to every mobile visitor. Pricing likewise collapses four tiers into
81px columns.
