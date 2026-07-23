# CLAUDE.md

Slidev deck for "Developing with Unity AI: Practical Use Cases" (Keijiro
Takahashi). Japanese content, ~86 slides. Originally built for Unite Seoul
2026 (already presented); `slides.md` is now being reworked for an upcoming
Japanese-audience presentation. `pnpm run dev` to serve at
http://localhost:3030/.

## slides-kr.md — the Seoul deck (frozen archive)

`slides-kr.md` is the deck as presented at Unite Seoul 2026. The session is
over: do NOT mirror `slides.md` edits into it anymore — the two decks have
intentionally diverged (as of July 2026, `slides.md` dropped the review
warning slide and gained new roadmap/CLI-demo slides) and will not be
re-synced. Only touch `slides-kr.md` if explicitly asked.

For reference, it was a translation of the then-identical `slides.md` with
a three-layer language split: speaker notes (HTML comments) in Japanese,
on-slide text in English, `<blockquote>` prompt/response examples in
Korean. Serve it with `pnpm exec slidev slides-kr.md --port 3030`
(`pnpm run dev` serves the Japanese deck; both default to port 3030, so
only one runs at a time).

## The design mimics the official Unite template

The visual theme replicates Unity's official "Unite 2026 Seoul - General
Template" PPTX (not in this repo; the user has the file, e.g. in
`~/Downloads/[External] Unite 2026 Seoul - General Template.pptx`). Design
values were extracted from that PPTX's XML, so they look arbitrary but are
not — don't "clean them up":

- Colors: pure black background, accent `#39AAFF`, secondary gray `#B7B7B7`.
- Fonts: Inter (+ Noto Sans JP for Japanese). Headings are ExtraBold (800).
- Base geometry in `styles/index.css` comes from the template's 10×5.625in
  slide mapped at 98px/in to Slidev's 980×551 canvas: side margins 69px
  (0.70in), title top 88px (0.90in), body top 147px (1.50in), h1 24.5px
  (18pt), body 16.3px (12pt).
- Bullets: level 1 is an SVG-mask chevron arrow, level 2 a dash (the Google
  Fonts Inter subset lacks U+2192, so the arrow is drawn, not a glyph).
  Blockquotes use plain "•" instead.
- `global-top.vue` draws the brand marks on every slide: Unity icon
  (top-left), "UNITE/" (bottom-left, white at 35% opacity per the template),
  "U/" (bottom-right). The SVG paths were machine-converted from the
  template's vector shapes. It must stay `global-top` (not `global-bottom`),
  otherwise the opaque slide background covers it. A slide can opt out with
  `hideBrand: true` in its frontmatter (used by slide 3, the full-bleed
  "UNITE/2026 SEOUL" cover image — `public/unite-cover.png`, the template's
  page 1 — whose artwork already contains the branding); global-top reads
  the current slide's frontmatter via the `$$slidev-context` injection,
  which works in both play and print/export modes.
- `public/unite-*.png|jpg` are backgrounds extracted from the template. The
  thank-you background is intentionally flipped (`scaleY(-1)`) because the
  template places that image with flipH + 180° rotation.
- The deck is dark-only (`colorSchema: dark` in the headmatter). Styles
  assume this; there is no light-mode support anywhere.

To extract more template details, unzip the PPTX and read the XML under
`ppt/slideLayouts/` (positions are EMU; 914400 EMU = 1 inch).

## Layouts

- Slide 1 has no `layout:` — Slidev implicitly gives the first slide
  `cover`, which is overridden locally by `layouts/cover.vue` (template
  title-page look). Use `cover` ONLY for the deck title slide.
- `layouts/chapter.vue` — project title pages with `<BgVideo>` backgrounds.
  The root has `isolate`: BgVideo renders at `z-index: -1`, and without an
  own stacking context the layout's black background paints over the video.
- `layouts/section.vue` — template section-divider background + 36pt title.
- `layouts/image-right.vue` / `two-cols-video.vue` — local customizations
  (black behind the image pane; column gap).

## Video and print/export

Slidev exports (PDF/PNG/PPTX) rasterize each slide in headless Chromium,
which does NOT paint seeked video frames — `print-timestamp` alone yields
black rectangles. Therefore:

- Every `<SlidevVideo>` carries `print-poster="/<video>-print.jpg"`.
- `BgVideo.vue` derives its poster from `src` (`foo.mp4` → `foo-print.jpg`)
  and uses `preload="none"` in print contexts so the poster always shows.
- When adding a video, generate its poster (3s frame; use the midpoint for
  clips shorter than that):
  `ffmpeg -ss 3 -i public/foo.mp4 -frames:v 1 public/foo-print.jpg`
- Export needs `--wait-until load` (default networkidle times out on video
  loading):
  `npx slidev export --format pptx --wait 1500 --wait-until load --timeout 90000`
- `playwright-chromium` is a devDependency for exactly this purpose.

Slide 3's full-bleed video uses `:muted="$renderContext !== 'slide'"` so
audio plays only in the play-mode window, not in presenter view.

## Editing gotchas

- Inline HTML blocks in `slides.md`: avoid blank lines between indented
  (4+ space) HTML lines — markdown reinterprets them as code blocks and the
  slide renders as literal text.
- SVG `<text>` font sizes must be inline styles (`style="font-size:..px"`);
  presentation attributes (`font-size=".."`) get overridden by slide CSS
  and render huge.
- SVG marker/def ids must be unique across the whole deck (all slides share
  one DOM); duplicated ids break arrowheads.
- `public/` assets are not HMR'd; reload the browser after replacing them.
  Headmatter, layout files, and slide-count changes need a dev-server
  restart.
- Slidev base CSS sets a fixed line-height on `p`/`li`, so line-height set
  on a container (e.g. blockquote) does not cascade into them — set it on
  `p`/`li` directly.

## Verifying visual changes

Headless screenshots work well for everything except video frames (those
render black — that's expected, not a bug). Typical check:

```js
import { chromium } from 'playwright-chromium'  // run from the repo root
const b = await chromium.launch()
const p = await b.newPage({ viewport: { width: 1280, height: 720 } })
await p.goto('http://localhost:3030/<N>', { waitUntil: 'networkidle' })
await p.waitForTimeout(1500)
await p.screenshot({ path: 'out.png' })
await b.close()
```

Slide numbers shift as slides are added; resolve them programmatically with
`@slidev/parser/fs` (`parse()` and search `slides[i].content`) instead of
hardcoding.
