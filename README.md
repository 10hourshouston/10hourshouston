# 10 Hours Houston — Witnesses

Event site for **10 Hours Houston**, a 10-hour gathering of worship, prayer,
consecration, and commissioning, with emphasis on science, technology, and media.

- **Theme:** Witnesses — Bearing Witness to Christ in Every Sphere
- **Tagline:** Ancient Wells. New Frontiers.
- **When:** Saturday, October 31, 2026, 10:00 AM – 8:00 PM CDT
- **Where:** Dominion Chapel Houston (DCH), 1203 Cravens Rd, Stafford, TX 77477
- **Register:** https://luma.com/oe8cgk9v
- **Contact:** 10hourshouston@gmail.com
- **YouTube:** https://www.youtube.com/channel/UCXyM-O4j0v1ThGibPrwTo5A
- **Instagram:** https://www.instagram.com/10hourshouston
- **TikTok:** https://www.tiktok.com/@10hourshouston

---

## ⚠️ One open decision: which tagline is canonical?

The Witnesses logo package reads **"New Wells. New Frontiers"**. The site's
existing body copy reads **"Ancient Wells. New Frontiers."** Both cannot be right.

- The hero now shows the lockup exactly as supplied, so it says *New Wells*.
- One line of body copy still says *Ancient Wells* — in the Burden section,
  marked with a `⚠ TAGLINE CONFLICT` comment in `index.html`. It is the only
  place the wording still lives; the decorative footer repeat was removed.

Change that one line, or send a corrected lockup. **Do not retype the tagline
inside the SVG** — the package warns that the +136/1000 em tracking is calculated
so the tagline's width matches the wordmark exactly, flush on both edges. New
wording means the tracking must be recalculated.

## Domain

Set to **https://10hourshouston.com** in `index.html`, `robots.txt`,
`sitemap.xml`, and `10-hours-houston.ics`.

After deploying, check the preview renders correctly:
- Facebook / Instagram — https://developers.facebook.com/tools/debug/
- X — https://cards-dev.twitter.com/validator
- Google event listing — https://search.google.com/test/rich-results

---

## Still open

1. **Is the event free?** If so, add `"price": "0", "priceCurrency": "USD"` inside
   the `"offers"` block of the JSON-LD in `index.html` (there's a comment marking
   the spot). Google needs a price to show the richest event result. It was left
   out rather than guessed.

2. **Parking, childcare, livestream?** These are the questions people ask before
   showing up, and none of it exists anywhere in the source material. There is no
   longer a section for it — the "Plan Your Day" cards were removed as a duplicate
   of the footer — so this would need a new block, or extra footer columns.

---

## What's on the page

| Section | Anchor | Notes |
|---|---|---|
| Hero | `#top` | Torch mark, Witnesses lockup, countdown, register |
| Scripture | — | Acts 1:8 |
| The Burden | `#burden` | |
| About | `#about` | |
| The Day | `#arc` | The ten-hour arc |
| Speakers | `#speakers` | Announced soon + sliding rail |
| Register | `#register` | **Commented out** |

### About "The Day"

The four movements — worship, prayer & the Word, consecration, commissioning —
come from the gathering's own description, in the order it names them. **No clock
times are assigned to them**, because the running order isn't set yet. Only the
10:00 AM and 8:00 PM endpoints are shown, since those are confirmed. When the
schedule is finalised, add times inside each `.arc-item`.

---

## Design notes

- **Type:** Instrument Sans for headings and body, JetBrains Mono for technical
  labels, nav, and metadata. Both are subset to Latin and served from `/assets/`.
- **Palette unchanged:** the site keeps its own colours — ink `#0c101c`, orange
  `#f73301`, soft `#ff8a5c` — and the cityscape photo background. The Witnesses
  package ships its own palette (Ink/Ember/Paper); only the Knockout artwork's
  paper white is used, so the brand's Ember `#9E3B14` never competes with the
  site's orange.
- **Two marks, on purpose:** the *10 Hours Houston* torch is the organisation;
  the *Witnesses* lockup is Season One. The torch sits in the nav and footer, the
  Witnesses lockup is the hero.
- **Colour:** the brand orange `#f73301` is taken from the logo's flame. Note that
  the primary button uses **dark ink `#0c101c` on orange**, not white — white on
  this orange is only 3.87:1 and fails WCAG AA. Dark ink gives 4.91:1. If you
  restyle the button, keep it above 4.5:1.
- **Background:** the cityscape is a fixed layer under a gradient veil. Swap it by
  replacing the `city-*.webp` / `city-*.jpg` files (three widths: 800, 1280, 1920).

### The Witnesses lockup

The hero uses the **Knockout** variant (paper artwork), per the brand spec's rule
that Knockout is for dark backgrounds and photography. Two deliberate choices:

- **The supplied ink panel was dropped.** The spec forbids placing the lockup on a
  busy image "without a solid or scrimmed panel behind it" — the page's existing
  gradient veil is that scrim, so a second opaque rectangle would have sat as a
  visible box over the skyline. The artwork colour is untouched.
- **No shadow or glow.** The old `Witnesses` text had a `text-shadow`; the spec
  forbids shadows, outlines, bevels, gradients and glows on the mark, so it was
  removed. Don't add one back.

Clear space (half the cap height, all four sides) is baked into the SVG's viewBox
padding, so it's preserved automatically at any size.

**Sizing.** `width: min(92vw, 820px)` — edge-to-edge on phones, capped on desktop.
The artwork is 88.8% of that box (the remainder is the spec's clear space), so the
spec's 180px minimum holds everywhere. Measured:

| Viewport | Artwork width |
|---|---|
| 320 × 568 (iPhone SE) | 261 px |
| 390 × 844 (iPhone 14) | 318 px |
| 768 × 1024 (iPad) | 627 px |
| 1440 × 900 (desktop) | 728 px |
| 844 × 390 (landscape) | 461 px |

Short viewports get their own rules: below 760px tall the lockup and spacing pull
in, and below 560px tall the torch mark is dropped so the hero doesn't overflow.

Source artwork, the specification PDF, and the Chakra Petch TTFs are kept in
`brand/`. Chakra Petch is **not** loaded as a webfont — the lockup's type is
outlined, so it renders without it. Load it only if you want the page's headings
to match the mark's typeface.

### Changing the hero photo

```bash
# from a new 1920px-wide source image
python3 - <<'EOF'
from PIL import Image
im = Image.open('new-city.jpg').convert('RGB')
for w in (1920, 1280, 800):
    r = im.resize((w, round(w*im.height/im.width)), Image.LANCZOS)
    r.save(f'assets/city-{w}.webp', 'WEBP', quality=76, method=6)
    r.save(f'assets/city-{w}.jpg', 'JPEG', quality=78, optimize=True, progressive=True)
EOF
```

---

## Pages

- `index.html` — the event page
- `sponsors.html` — the partnership page

Shared CSS now lives in `assets/site.css` rather than inline, so the two pages
share one cached stylesheet instead of duplicating ~25 KB of rules.

### Speakers rail

`#speakers` has a sliding rail of six placeholder cards, duplicated once so the
loop is seamless. To add real speakers:

1. Drop photos in `assets/speakers/` (square, ~400×400, cropped to the face).
2. In each `.sp-card`, swap the placeholder `<svg>` for
   `<img src="/assets/speakers/name.jpg" alt="" width="96" height="96">`.
3. Replace "Announced soon" with the name and "Speaker 0N" with their role.
4. **Update both copies** — the second set is marked with a comment. If the two
   halves differ, the rail visibly jumps when it loops.

The rail pauses on hover and on keyboard focus, and under
`prefers-reduced-motion` it stops animating and becomes a normal scrollable row.

### Sponsors page

Content comes from the partnership PDF. It deliberately does **not** repeat The
Burden, which already has its own section on the home page — the letter links the
two instead. Because there are no sponsor logos yet, the proof section is the
prayer track record (Shift 90, Shift 120, the 24- and 48-hour retreats) rather
than a logo wall. Swap in a logo grid once partners sign.

Prices, tiers, and the benefit matrix are transcribed from the PDF. Three typos
in the source were corrected here: "Exhibit Boot" → "Exhibit booth", "hear
witness" → "bear witness", "in an invitation" → "is an invitation".

## Files

```
index.html               the event page
sponsors.html            the partnership page
assets/site.css          shared stylesheet for both pages
10-hours-houston.ics     calendar file, correct America/Chicago DST rules
site.webmanifest         icons + theme for "add to home screen"
robots.txt, sitemap.xml  search engines
logo-light.svg           torch logo source (unused by the page)
logo-dark.svg            torch logo source (embedded inline in index.html)
brand/                   Witnesses logo package: SVG variants, spec PDF,
                         Chakra Petch TTFs + OFL licence
Instrument_Sans-OFL.txt  font licence (JetBrains Mono is also OFL)
assets/
  instrument-sans.woff2  subset to Latin
  jetbrains-mono.woff2   subset to Latin
  city-{800,1280,1920}.{webp,jpg}
  og.jpg                 1200×630 social share card
  favicon.svg .ico icon-16/32/192/512 apple-touch-icon.png
```

### Regenerating the share card and favicons

`og.jpg` and the icons were generated from `logo-dark.svg` + the city photo. If
the branding changes, they need regenerating — there's no build step that does it
automatically.

---

## Performance

The previous version inlined both fonts and the hero photo as base64 inside a
render-blocking `<style>` block: the browser had to download and parse 215 KB
before it could paint anything. Those are now external files with `preload` hints.

| | before | after |
|---|---|---|
| Render-blocking HTML | 215.6 KB | 43.8 KB |
| Mobile first load | ~215.6 KB | ~122.8 KB |
| Hero image (mobile) | 60 KB base64 | 5.8 KB WebP |

**Trade-off:** the page no longer works by double-clicking `index.html` off a USB
stick, because assets load from absolute paths (`/assets/…`). This was a
deliberate swap of offline-portability for first-paint speed on phones. Preview
locally with a server instead:

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

---

## Accessibility

Register stays visible in the nav bar on phones, because the hero is taller than a
small screen and the CTA otherwise falls below the fold.

Built to and verified against: skip link as first tab stop, visible focus rings,
h1→h2→h3 with no skipped levels, labelled controls, `prefers-reduced-motion`
honoured, no horizontal overflow from 320px up, AA contrast on all text.

The countdown is `aria-hidden` — a clock ticking once per second is unusable
read aloud — and a quiet day count is exposed to screen readers instead.

---

## Deploy

Static site, no build step.

- **Vercel:** import the repo. Every push auto-deploys.
- **Netlify / Cloudflare Pages:** drag the folder in, or connect the repo.

Optional: serve `/assets/*` with a long cache header
(`Cache-Control: public, max-age=31536000, immutable`) — the filenames are stable,
so returning visitors skip re-downloading the fonts and photo.
