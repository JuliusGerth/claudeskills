---
name: speed-craft
description: 'Make pages genuinely fast - images, fonts, JavaScript weight, and Core Web Vitals (LCP, CLS, INP) via a measured optimization pass with concrete budgets. Use this skill whenever a page or app feels slow ("traag", "laadt lang", "duurt even"), before launching anything public (pair with ship-it), when Lighthouse or PageSpeed scores matter, or whenever images, embeds, fonts, or heavy libraries are added to a page. Goes deeper than the performance basics in frontend-quality-gates - this is the dedicated speed pass.'
---

# Speed Craft

Speed is UX: slow pages feel broken and lose visitors before showing anything. Almost all web slowness comes from four sources — images, fonts, JavaScript, and layout shift — in that order of likelihood. Fix by measurement, not vibes.

## Step 0 — Measure first

Optimizing without measuring is guessing. Establish the baseline: Lighthouse (in devtools or PageSpeed Insights) on the LIVE or built page, throttled to mobile — that is the real audience condition. Note LCP, CLS, INP/TBT and total transferred bytes. Re-measure after each pass; keep changes that move numbers, revert ones that do not.

Targets: LCP < 2.5s · CLS < 0.1 · INP < 200ms.

## Pass 1 — Images (usually 80% of the win)

- Modern format: WebP/AVIF instead of PNG/JPEG (photos as AVIF/WebP ~80% quality is visually lossless at a fraction of the bytes).
- Sized to display: no 4000px originals in a 400px slot. Provide `srcset` for large hero images.
- `width`/`height` (or `aspect-ratio`) attributes on EVERY image — without them the page jumps as images load (CLS).
- `loading="lazy"` on everything below the fold; NEVER on the hero/LCP image — that one gets `fetchpriority="high"`.
- Iconography as inline SVG, not icon-font or PNG.

## Pass 2 — Fonts

- Maximum 2 font families, ~4 files total (regular/bold per family). Every weight is a download.
- `font-display: swap` so text is readable during font load; preload the primary font file.
- Self-host with `woff2` and subset to the characters actually needed (latin) — often 70% smaller.
- No font needed at all? The system font stack costs 0 bytes and looks native.

## Pass 3 — JavaScript

- Biggest question first: is the heavy dependency pulling its weight? A 300KB library for one date-format or one carousel is the classic mistake — replace with a few lines of vanilla or a micro-library.
- `defer` all non-critical scripts; third-party embeds (maps, video, chat widgets) load on interaction (click-to-load facade) — they are routinely the heaviest thing on the page.
- Long tasks block clicks (INP): debounce input handlers, chunk heavy loops, move real number-crunching off the main thread.
- Animations: only `transform` and `opacity` (see motion-craft) — animating layout properties forces reflow jank.

## Pass 4 — CSS & layout stability

- Reserve space for EVERYTHING that arrives async: images (pass 1), ads, embeds, web fonts, skeletons in the real dimensions. CLS is almost always "iets laadde en duwde de pagina omlaag".
- Ship one CSS file, minified; cut dead rules. Critical-CSS inlining only when measurement says CSS blocks first paint.
- `content-visibility: auto` on long below-fold sections defers their render cost.

## Budget (enforce at build time)

| Item | Budget |
|---|---|
| Total page weight (first load) | < 1 MB (target 500 KB) |
| JS (compressed) | < 200 KB |
| Hero image | < 200 KB |
| Fonts total | < 100 KB |
| Requests | < 50 |

Over budget? Something must leave — the budget is the argument that wins feature-creep debates.

## Verify

Re-run Lighthouse mobile on the built page. Compare against Step 0 numbers in the delivery note ("LCP 4.1s → 1.9s"). Test once on a real phone over cellular if possible — the emulator flatters. Then hand off to ship-it.
