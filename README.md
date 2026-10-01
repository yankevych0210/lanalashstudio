# Lana Studio

Marketing website for **Lana Studio** — lash extensions, lash and brow lamination, brows and sugaring in Walnut Creek and San Francisco, CA.

**Live:** https://lanalashstudio.com

## Overview

A single-page static site with no build step and no dependencies. Everything — markup, styles and scripts — lives in `index.html`; photos live in `images/`.

**Sections:** hero, about, services, recent work (filterable gallery with lightbox), before/after slider, prices (per studio and category), reviews, booking, FAQ.

**Booking** goes through Square Appointments (one booking page per studio). Visitors can also send a pre-filled request by SMS or WhatsApp; the message is built from the options they pick on the page.

## Project structure

```
.
├── index.html            # the whole site: HTML, CSS (<style>) and JS (<script>)
├── 404.html              # "page not found" page (served by Vercel automatically)
├── images/
│   ├── og-cover.jpg      # social sharing preview (1200×630)
│   └── photo-XX.jpg      # logo, portrait, gallery and before/after photos
├── favicon.ico           # browser tab icon (legacy browsers)
├── favicon-32.png        # browser tab icon
├── apple-touch-icon.png  # iOS home-screen icon
├── icon-192.png          # Android / web app icon
├── icon-512.png          # web app icon, logo in structured data
├── site.webmanifest      # web app manifest (name, colors, icons)
├── robots.txt
├── sitemap.xml
├── vercel.json           # clean URLs, security headers, image caching
└── docs/
    └── CONTENT.md        # how to update prices, hours, photos and links
```

## Running locally

Any static file server works. From the project root:

```bash
python3 -m http.server 8000
# or
npx serve .
```

Then open http://localhost:8000.

Opening `index.html` directly from disk also works, except for the root-relative favicon paths.

## Deployment

The site is hosted on [Vercel](https://vercel.com) and deploys automatically:

- A push to `main` publishes to production.
- A push to any other branch, or a pull request, gets its own preview URL.

Vercel project settings: **Framework preset** Other, **Root directory** `./`, no build command, no output directory, no environment variables.

The domain `lanalashstudio.com` (and `www`) is attached under **Settings → Domains** in the Vercel project.

## Updating content

Prices, working hours, contacts, booking links, photos and reviews are all edited directly in `index.html`. See **[docs/CONTENT.md](docs/CONTENT.md)** for where each piece lives and what else needs updating alongside it.

After a content change, check it at both phone width and desktop width before pushing to `main`.

## SEO

- `<title>`, meta description, canonical URL and Open Graph / Twitter tags in `<head>`
- `BeautySalon` structured data (JSON-LD) with both locations, phone and opening hours
- `sitemap.xml` and `robots.txt`

Structured data can be checked with Google's [Rich Results Test](https://search.google.com/test/rich-results).

## Browser support

Current versions of Safari (iOS and macOS), Chrome, Edge and Firefox. The layout is mobile-first and respects `prefers-reduced-motion`.

## License

Copyright © 2026 Lana Studio. All rights reserved. The code, photos and branding are not licensed for reuse — see [LICENSE](LICENSE).
