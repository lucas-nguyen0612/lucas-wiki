# Design system — projection-grade slides

This is the shared design language for every deck, regardless of track (plain HTML or
React). The rules here exist because the output is **projected to a room**, not read on
a personal screen. Internalise the mental model first; the specifics follow from it.

## The one mental model: this is projection, not a web app

There is exactly **one operator** — the presenter — on **one machine**. Slides are
thrown onto a big screen (projector, or screen-share in Meet/Zoom). The audience only
**looks**. They never click, type, or touch anything.

Two mistakes follow from forgetting this, and both are common:

1. **Text too small.** Web-sized type (`text-sm`, `16px`, `1rem`) is illegible from the
   back of a room. On a 1080p canvas, `16px ≈ 8pt` — half the minimum.
2. **Treating it like an app.** Building input fields, "Submit" buttons, login, score
   collection, anything that stores data. There is no backend and nowhere for data to
   go. If a component raises the question *"where does this data go / who reads it?"*,
   it is wrong — remove it.

## Typography floor (non-negotiable)

Sizes are projection sizes on a **1920×1080** screen (1pt ≈ 2px). There is **no single
"correct" size** — each role has a **range**, and you pick within it per slide based on how
much content is on it. The floor is the hard bottom; the hero ceiling is the hard top.

| Role                | Floor (hard min) | Projection range — pick per slide | Hero ceiling |
| ------------------- | ---------------- | --------------------------------- | ------------ |
| Body / bullet       | 20pt · 40px      | **40–48px**                       | 52px         |
| Subtitle / lead     | 24pt · 48px      | **48–60px**                       | 64px         |
| Section head (h2)   | —                | **52–64px**                       | 72px         |
| Main title (h1)     | 36pt · 72px      | **80–104px**                      | 120px        |
| Caption / slide no. | 16pt · 32px*     | **32–38px**                       | —            |

\* caption/slide-number is the one role allowed below the body floor (never < 16pt = 32px),
since it isn't primary reading.

**How to pick within the range — this is the point:**

- **Text-heavy slide** (several bullets, a long quote, a dense table): drop toward the
  **bottom of the range** — down to the floor if needed — so the content fits without
  overflowing or scrolling. A slide that overflows is worse than one a notch smaller.
- **Sparse slide** (a few words, one stat, a cover): move toward the **top of the range**,
  or use the hero ceiling on a *single* hero element (cover title, one big number). Bump
  *that one element*, not the globals.
- **Ordinary slide:** land in the middle of the range. Don't default to the ceiling —
  oversized type looks shouty and crowds the slide.
- **Never below the floor**, whatever the content. If it still won't fit at the floor, the
  slide has too much on it — split it into two, don't shrink past the floor.

- **Don't use fixed `px`/`rem` for slide text.** Both templates are fluid, so use
  frame-relative units: `clamp(min, vw/vh, max)` for type, `em`/`%`/`vh` for spacing —
  the `max` is the projection size you pick from the range above. Fixed px only belongs in
  a fixed-canvas deck that is then scaled (not the default).
- **Acceptance test:** zoom the screen to ~33% (or stand 3–4 m back). If you can still
  read the bullets, it passes — and nothing is clipped at the slide edges.

Two ways to satisfy the floor:

- **Fluid `clamp()`** (both templates' default): size text as `clamp(min, vw/vh, max)`,
  where the **`max` is the size you chose from the range above** for that role on that
  slide. E.g. an ordinary body line `clamp(28px, 2.6vw, 44px)`; the same line on a
  text-heavy slide tightened to `clamp(28px, 2.4vw, 40px)`; a hero headline opened up to
  `clamp(56px, 6.4vw, 112px)`. The `min` is a small-window fallback, the `max` is the
  projection size, the middle scales with the viewport. Slides fill the whole screen at
  any aspect ratio — no letterbox/pillarbox bars. **Best default.**
- **Fixed canvas + scale**: size everything in px on a 1920×1080 stage, then
  `transform: scale()` to fit. Sizes are pixel-exact, but the deck letterboxes/pillarboxes
  on any non-16:9 screen (16:10 laptops, ultrawides, resized windows). Use only when you
  truly need pixel-locked layout and control the projector's aspect ratio.

## Content discipline

- One idea per slide. Few words. Let the presenter's voice carry the detail.
- Prefer a real visual (image, diagram, screenshot) over a paragraph.
- Vietnamese copy should sound like someone talking on stage — plain, honest, direct.
  No marketing tone, no hype. Say what the tech does and what it doesn't.

## Allowed interaction (presenter-controlled only)

Interaction exists to make the slide change visually while the presenter clicks:

- ✅ Reveal content step by step (progressive bullets, expand a card, flip).
- ✅ Move between slides; jump via the dot strip / table of contents.
- ✅ Toggle a before/after compare, tabs, or an accordion **whose content already exists**.
- ✅ Timers, countdowns, animation, highlight, hover.

Never: text inputs, "Submit/Save", answer collection, scoring, login, or anything that
assumes storage (DB, an API call, localStorage for someone's answers).

## Required chrome on every deck

- A visible **navigation slider** (the dot strip) and **slide number** at the bottom,
  so the presenter can jump around live. Both scaffolds include this — keep it.
- Keyboard navigation: → / Space / PageDown advance; ← / PageUp go back; Home/End jump.

## Slide layout recipes

Reach for these instead of inventing structure each time. (Tailwind classes shown for
the React track; the plain-HTML template uses equivalent inline styles.)

**Title** — badge top, big headline + one-line lead centre, presenter line bottom.
`flex flex-col justify-between`, headline `clamp(64px,9vw,120px) font-black`.

**Bulleted point** — `h2` heading + 3–5 short bullets, generous `gap`. Keep bullets to
one line each; if a bullet wraps twice, split the slide.

**Two-column compare** — `grid grid-cols-2 gap-12`, each column a card
(`rounded-3xl p-12`). Use for before/after, problem/solution, myth/reality.

**Big stat** — one huge number (`clamp(120px,18vw,260px)`) + a short caption. One stat
per slide; the number is the whole point.

**Quote** — centred, large italic/serif line, attribution as caption below.

**Full-bleed image** — `fullBleed` slide, image `object-cover` filling the frame, text
in an overlaid panel with a translucent/blurred background for contrast.

## Motion (React track: Framer Motion)

- Slide transitions are handled by `Deck` (a short cross-fade). Don't fight it.
- Inside a slide, animate entrance with small `initial → animate` offsets
  (`y: 24, opacity: 0` → `y: 0, opacity: 1`, ~0.4s), staggering with `delay`. Subtle
  beats flashy — motion should guide the eye, not perform.
- For step-by-step reveals, drive a local `useState` step counter from the same keyboard
  handler pattern, or split into separate slides (simpler and usually better).

## Optional: ambient background

A drifting gradient backdrop adds polish but is never required and must never reduce
text contrast. If you want it, the pattern (from real decks) is: 2–3 large blurred
radial "blobs" absolutely positioned with slow CSS keyframe drift, plus optional
floating dust motes. Keep it behind a `z-index` floor and `pointer-events: none`.
Reference implementation lives in the repo decks; copy and re-tint per deck palette.

## Palette

The scaffolds ship a warm neutral default (`--bg #f8f3e7`, `--ink #1f2430`,
`--accent #9d6248`, `--soft #6d6a66`). Replace per deck/brand — change the CSS variables
(HTML) or the hex values in `Deck`/`Slide`/`index.css` (React). Keep one accent colour
and use it consistently for emphasis.
