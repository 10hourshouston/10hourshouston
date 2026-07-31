# 10 Hours Houston — Witnesses

Event site for **10 Hours Houston**, a ten-hour gathering of worship, prayer,
consecration, and commissioning, with emphasis on science, technology, and media.

- **Theme:** Witnesses — Bearing Witness to Christ in Every Sphere
- **Tagline:** Ancient Wells. New Frontiers.
- **When:** Saturday, October 31, 2026, 10:00 AM – 8:00 PM
- **Where:** Houston, Texas (venue announced soon)
- **Contact:** 10hourshouston@gmail.com

## Design notes

- Type: Instrument Sans for headings and body, JetBrains Mono for the technical
  labels, nav, and metadata. Both are embedded in `index.html` (works offline).
- The hero uses a constant cityscape background, embedded directly in the page.
  To swap it for a different photo, replace the `background-image` data URI on
  the `.hero-bg` rule in `index.html`, or point it at `city-bg.jpg`.

## Files

- `index.html` — the entire site (fonts, logo, and city background embedded)
- `city-bg.jpg` — optimized hero background (swap this to change the skyline)
- `logo-light.svg` / `logo-dark.svg` — logo source files
- `Instrument_Sans-OFL.txt` — Instrument Sans license (JetBrains Mono is also OFL)

## Deploy

Static site, any host works.

- **Vercel:** import the repo, no build step. Every push auto-deploys.
- **Netlify / Cloudflare Pages:** drag the folder in, or connect the repo.
- **Local preview:** open `index.html` in a browser.
