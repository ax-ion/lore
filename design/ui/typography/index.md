# Typography — UI

---

## Type Scale — Use a Ratio, Not Arbitrary Sizes

Picking font sizes randomly produces visual noise. Use a multiplier:

| Scale | Ratio | Feel |
|-------|-------|------|
| Major Second | 1.125 | Subtle, tight — good for dense UIs |
| Major Third | 1.25 | Balanced — good for most products |
| Perfect Fourth | 1.333 | Expressive — good for marketing |
| Major Sixth | 1.5 | Bold — good for display/editorial |

Starting from 16px base with 1.25:
`12 → 14 → 16 → 20 → 25 → 31 → 39 → 49`

Use a tool: [typescale.com](https://typescale.com)

---

## Font Pairing

One pairing rule that holds: **one font for UI (sans-serif), one for headings (can be serif or display), never more than two.**

Pairings that work:
- Inter + Fraunces — clean UI + distinctive editorial heading
- Inter + Cal Sans — both clean, Cal Sans has personality
- Geist + anything — Geist is neutral enough to carry a whole product alone
- System font stack + a display font for headings only

Don't pair two fonts that are too similar (two geometric sans-serifs). The contrast is the point.

---

## Line Height

- **Body text**: 1.5–1.6 — tight is fatiguing to read
- **Headings**: 1.1–1.3 — tall line height on big text looks awkward
- **UI labels / buttons**: 1.0–1.2 — these aren't paragraphs

---

## Line Length (Measure)

45–75 characters per line for readable body text. Beyond 80 characters and the eye loses its place returning to the next line. Below 40 and the rhythm feels choppy.

In practice: max-width on prose content. `prose` class in Tailwind Typography handles this.

---

## Weight Contrast Over Size Alone

A common mistake is using only size to create hierarchy. Weight does more:
- `font-weight: 400` body + `font-weight: 700` heading creates hierarchy even at similar sizes
- Using `font-weight: 500` for everything flattens the hierarchy even if sizes vary

The full weight range (100–900) rarely needs to be used. Usually three weights are enough: regular (400), medium (500), bold (700).

---

## Minimum Sizes

- Body copy: never below **14px** (16px preferred)
- Captions/labels: never below **12px**
- Below 12px: don't do it, even for "fine print"

---

## What Gets Overlooked

- **Letter spacing on all-caps** — uppercase text needs `letter-spacing: 0.05–0.1em` or it reads as a wall
- **Font loading** — flash of unstyled text (FOUT) or invisible text (FOIT) degrades perceived performance. Use `font-display: swap` and preload critical fonts.
- **Optical size** — some variable fonts have an `opsz` axis. Using it makes text at small sizes more legible.
- **Prose vs UI text** — prose needs generous spacing; UI elements (labels, buttons, nav) need tighter spacing. Don't apply the same line-height globally.
- **Monospace for code** — always use a dedicated monospace font for code blocks, never a proportional font
