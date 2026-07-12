# AiCraft — Color & Style Reference

Last updated: 2026-06-17 (`style-improvements` branch)

This is the single source of truth for the site's colors. All values live as
tokens in [`src/styles/global.css`](../src/styles/global.css); this document
mirrors them in a form you can paste into Canva, Figma, or any design tool.

> **Updating the logo in Canva?** Jump to [Logo guidance](#logo-guidance).
> The short version: pull from **Gold `#D9AA52`**, **Coral `#EC6A4C`**,
> **Teal `#1F8A8A`**, and **Indigo `#4F46E5`**, all on a **Cream `#F3EFE6`**
> or **Ink `#1C1C1C`** background.

---

## Core palette

| Role | Name | Hex | RGB | Token |
|------|------|-----|-----|-------|
| Background | Cream | `#F3EFE6` | `243, 239, 230` | `--color-bg` |
| Surface | White | `#FFFFFF` | `255, 255, 255` | `--color-surface` |
| Tinted surface | Mist | `#EAF1F0` | `234, 241, 240` | `--color-tint` |
| Text | Ink | `#171717` | `23, 23, 23` | `--color-ink` |
| Text (soft) | Soft ink | `#5F5A53` | `95, 90, 83` | `--color-ink-soft` |
| Dark panel | Panel | `#1C1C1C` | `28, 28, 28` | `--color-panel-dark` |
| Border | Sand | `#D8D2C8` | `216, 210, 200` | `--color-border` |

## Accent palette (the "splashes of color")

| Name | Hex | RGB | Token | Used for |
|------|-----|-----|-------|----------|
| Gold | `#D9AA52` | `217, 170, 82` | `--color-accent` | Primary accent, buttons on dark, warm gradient start |
| Coral | `#EC6A4C` | `236, 106, 76` | `--color-coral` | Warm gradient end, chart accent |
| Teal | `#1F8A8A` | `31, 138, 138` | `--color-teal` | Cool gradient start, tinted surfaces |
| Indigo | `#4F46E5` | `79, 70, 229` | `--color-indigo` | Cool gradient end, dark-band lead-in |

---

## Gradients

All gradients are linear. Angle is `100deg` for fills (`.grad-text`,
composition cards) and `90deg` (left→right) for the thin section bands.

| Name | Stops | Token | Where it appears |
|------|-------|-------|------------------|
| **Sunrise** | Gold `#D9AA52` → Coral `#EC6A4C` | `--grad-sunrise` | Hero headline accent (`.grad-text`), first section band |
| **Tide** | Teal `#1F8A8A` → Indigo `#4F46E5` | `--grad-tide` | Mid-page section bands |
| **Dusk** | Indigo `#4F46E5` → Ink `#1C1C1C` | `--grad-dusk` | Band leading into the dark CTA "anchor" sections |

## Hero backdrop

The homepage hero uses `src/assets/graph-concept.png` — a node-graph illustration — as a
right-anchored background rather than a foreground graphic.

The artwork ships with a **white** plate, which would read as a pale rectangle against the
cream page. Two CSS properties do the work of hiding that:

- `mix-blend-mode: multiply` — multiplying the artwork against Cream `#F3EFE6` erases its white
  background entirely, so the nodes look printed onto the page rather than pasted over it.
- a horizontal `mask-image` gradient — dissolves the image to nothing before it reaches the
  text column, which is what keeps headline contrast intact.

If you swap the artwork, keep both: any replacement needs a white or very light background for
the multiply trick to work, and the mask must still clear the left ~45% of the hero.

CSS form (for reference):

```css
--grad-sunrise: linear-gradient(100deg, #D9AA52, #EC6A4C);
--grad-tide:    linear-gradient(100deg, #1F8A8A, #4F46E5);
--grad-dusk:    linear-gradient(100deg, #4F46E5, #1C1C1C);
```

Tinted section surface (top→bottom, tint fading to cream):

```css
linear-gradient(180deg, #EAF1F0, #F3EFE6);
```

---

## Section rhythm

The page reads top-to-bottom as alternating beats, separated by 6px gradient bands:

```
Cream hero  →  [Sunrise band]  →  Tinted/Cream section
            →  [Tide band]     →  Tinted section
            →  [Dusk band]     →  Dark panel CTA (anchor / final beat)
```

- **Cream** (`#F3EFE6`) — default reading surface.
- **Mist tint** (`#EAF1F0` → cream) — secondary sections (services, case study, pilots, footers).
- **Panel** (`#1C1C1C`) — high-contrast CTA anchor, gold button on top.

---

## Logo guidance

For adjusting the logo in Canva, use these combinations so it sits naturally on
the site:

**Backgrounds the logo must work on**
- Cream `#F3EFE6` (nav bar, most pages) — *primary; design for this first.*
- Ink / Panel `#1C1C1C` (dark CTA sections, footer) — *needs a light or gold variant.*

**Logo color options (pick from the accent palette)**
- **Gold** `#D9AA52` — warmest, matches the primary accent. Safe on both cream and dark.
- **Coral** `#EC6A4C` — more energetic; pairs with gold as a sunrise gradient.
- **Teal** `#1F8A8A` — cooler, "data/tech" feel.
- **Indigo** `#4F46E5` — strongest cool accent; high contrast on cream.
- **Ink** `#171717` — neutral mark for cream backgrounds.

**If you want a gradient logo / icon**
- Warm mark: fill with **Sunrise** — Gold `#D9AA52` → Coral `#EC6A4C`.
- Cool mark: fill with **Tide** — Teal `#1F8A8A` → Indigo `#4F46E5`.

**Contrast notes**
- On cream, avoid pure white; use Ink or an accent.
- On the dark panel, use Gold `#D9AA52`, white, or a light tint — not Indigo or Ink.
- Keep a single-color fallback version (Gold or Ink) for small sizes where a
  gradient would muddy.

---

## Where the tokens live

`src/styles/global.css`, in the `@theme` block (colors) and the `:root` block
(gradients). Change a value there and it propagates to every page, the section
bands, the hero composition, and the headline accents — there are no hardcoded
color values in the page templates.
