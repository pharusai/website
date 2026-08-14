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
| `https://app.pharus.ai/new-organization` | every "Start free trial" / "Start 14-day trial" CTA (6 of them) |
| `https://app.pharus.ai` | "Log in" only — header and footer |
| Google Calendar appointment schedule | "Book a working session" — 30 min, auto-generates a Meet link |
| `mailto:marshall@pharus.ai` | "Talk to us", footer Contact |
| `#why` `#day` `#pricing` `#top` | nav + footer |

`#faq` exists as a section but nothing links to it yet.
