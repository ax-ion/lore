# Color — UI

Not about hex codes. About decisions that hold up across an entire product.

---

## The 60-30-10 Rule

Every UI has three color roles:
- **60%** — dominant neutral (backgrounds, surfaces)
- **30%** — secondary (sidebars, cards, secondary surfaces)
- **10%** — accent (CTAs, highlights, interactive elements)

Breaking this ratio is why UIs feel "busy" or "flat." The accent color should be rare enough to mean something.

---

## Semantic Colors — Pick One Set and Never Break It

| Role | Convention |
|------|-----------|
| Success | Green |
| Error | Red |
| Warning | Amber/Yellow |
| Info | Blue |
| Neutral | Gray |

The problem isn't picking these — it's when you use a red heading for emphasis or a green badge for "new" and now red no longer means error. Semantic colors only work if they're consistent everywhere.

---

## Contrast — What Actually Matters

WCAG AA minimums (non-negotiable for any production UI):
- Body text on background: **4.5:1**
- Large text (18px+ or 14px bold): **3:1**
- UI components and icons: **3:1**

Tools: [Coolors contrast checker](https://coolors.co/contrast-checker), [WebAIM](https://webaim.org/resources/contrastchecker/)

Don't eyeball it. What looks fine on your calibrated monitor fails on a cheap phone screen in sunlight.

---

## The Gray Problem

Gray is the hardest color. There are two families and mixing them destroys cohesion:

- **Cool grays** — blue/purple undertone — work with blue-heavy palettes
- **Warm grays** — yellow/red undertone — work with warm palettes

Most design systems pick one and stay there. Tailwind's slate (cool) vs stone (warm) vs zinc (neutral) are all different answers to this same problem. Pick one, use it everywhere.

---

## Dark Mode — Don't Just Invert

Common mistake: take the light mode palette and invert it. Result: harsh white text on pure black, everything glows.

Dark mode best practices:
- Background should be **dark gray, not black** — `#0f0f0f` or `#1a1a1a` not `#000000`
- Elevation uses **lighter grays**, not shadows (shadows disappear on dark backgrounds)
- Reduce saturation on colors — vivid colors are harder to look at against dark backgrounds
- Text is **off-white**, not pure white — `#e2e2e2` or `#f0f0f0`

---

## Proven Palette Foundations

Don't start from scratch. Start from these and customize:

- **[Radix Colors](https://www.radix-ui.com/colors)** — 28 scales, each with 12 steps, light + dark, designed for UI. Best for serious products.
- **Tailwind palette** — opinionated, widely understood, battle-tested. Usable as-is.
- **[Realtime Colors](https://realtimecolors.com)** — visualize a full palette on a real UI before committing.

---

## Saturation Fatigue

A fully saturated accent color looks great in isolation. Across an entire product it becomes exhausting. Rule: bring saturation down 20-30% from what "looks good" in isolation and it'll hold up better in context.

---

## What Gets Overlooked

- **Hover/active states** need to be distinct but not jarring — typically 10-15% darker/lighter than base
- **Disabled states** should look visibly different — low opacity (40-50%) or muted gray, not just slightly lighter
- **Focus rings** for keyboard nav — don't remove `outline: none` without replacing it with something visible
- **Link colors** need to be distinguishable from body text without relying solely on underline
