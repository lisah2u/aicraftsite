# Changelog

All notable changes to the AiCraft website are recorded here.

## [Unreleased] — `style-improvements` branch

### 2026-06-17 — Gradient-forward visual refresh

A site-wide style pass to replace a flat, single-accent palette and
near-invisible section transitions with a **gradient-forward** system:
color now arrives as gradient "splash" bands between sections and as solid
tinted surfaces, giving each section its own identity and a clear visual rhythm.

See [`docs/STYLE.md`](docs/STYLE.md) for the full color reference (hex codes,
gradients, and usage), including the values needed to update the logo in Canva.

#### Added
- **Palette tokens** in `src/styles/global.css`: `--color-coral` (`#EC6A4C`),
  `--color-teal` (`#1F8A8A`), `--color-indigo` (`#4F46E5`), and
  `--color-tint` (`#EAF1F0`), alongside the existing gold accent.
- **Gradient tokens**: `--grad-sunrise` (gold → coral), `--grad-tide`
  (teal → indigo), and `--grad-dusk` (indigo → ink).
- **Reusable utilities** in `global.css`:
  - `.band` / `.band--sunrise` / `.band--tide` / `.band--dusk` — 6px gradient
    "splash" bands that punctuate section transitions.
  - `.grad-text` / `.grad-text--tide` — gradient-clipped text for headline accents.
- **`docs/STYLE.md`** — color and gradient reference / lightweight style guide.

#### Changed
- **Home hero (`src/pages/index.astro`)**: replaced the animated spinning-triangle
  canvas with a static gradient composition (blurred color blobs + a tilted
  Tide-gradient card + a white "report" card). Subtle one-time motion only:
  chart bars grow on load (staggered) and the blobs drift slowly. Honors
  `prefers-reduced-motion`.
- **Section surfaces** across all pages: swapped `rgba(255,255,255,0.x)` white
  washes for solid tinted gradients (`linear-gradient(180deg, var(--color-tint), var(--color-bg))`).
- **Section transitions**: added sunrise / tide / dusk gradient bands between
  major sections on every page.
- **Hero headline accents**: a key phrase on each page hero is now
  gradient-clipped (e.g. "clear dashboards", "small-studio delivery",
  "better decisions", "insights", "idea or problem").
- **About page CTA**: converted from a light section to the dark "anchor"
  treatment (with a gold button), matching the home and services page CTAs.

#### Removed
- The old triangle/connection canvas animation and its ~140 lines of JS from
  `index.astro`.
- `src/pages/preview/style.astro` — the temporary mockup page used to compare
  directions during this work.

#### Files touched
- `src/styles/global.css`
- `src/pages/index.astro`
- `src/pages/about.astro`
- `src/pages/services.astro`
- `src/pages/knowledge.astro`
- `src/pages/knowledge/[slug].astro`
- `src/pages/contact.astro`
