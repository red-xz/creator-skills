# Unslop a Screen

Run the unslop audit and nine passes on one screen. Loads the `unslop`
skill for the full rules; this file is the run order.

## 1. Look

- [ ] Open the screen in a browser and screenshot it — judge what people
      see, not only the code
- [ ] Find the files that render it

## 2. Audit (write it down, one line per sign)

- [ ] Hue gradients on surfaces, gradient text, glows, colored shadows,
      color blobs
- [ ] Emoji used as icons or in labels
- [ ] Uppercase tracked labels (`NAVIGATION`, `PAID THIS MONTH`)
- [ ] Pulsing / looping / floating elements
- [ ] Uneven spacing (one-off values like `mt-[13px]`)
- [ ] Hype copy (`supercharge`, `unlock`, `AI-powered`, unverified claims)
- [ ] Three identical cards in a row
- [ ] Greeting headline (`Welcome back!`)

## 3. Decide how much to change

- **Heavy slop** (many signs across color, type, icons, copy) → full
  nine-pass run.
- **Light slop** (mostly designed, a few signs left) → polish mode: fix
  only what the audit found, keep the palette/type/layout, bigger ideas
  go in the report as suggestions.
- **No slop** → say so plainly, suggest at most 2–3 small refinements
  with exact values, apply only if the user agrees, stop there.

## 4. Direction (five lines, before touching anything)

- [ ] Product — what it does and for whom, one plain sentence
- [ ] Character — two or three concrete words (not "clean, modern, sleek")
- [ ] World — the place or material the product belongs to
- [ ] Moments — one or two places where the screen gets rich color/detail
- [ ] Signature — one small detail only this product would have

Show the audit + direction to the user and wait for their answer before
editing. Skip the wait only if they already said to just do it.

## 5. Nine passes, in order

1. Spacing (4px grid, same thing same size, space shows grouping)
2. Color (one tinted neutral ramp, three text roles, one accent)
3. Icons (one set, one size/stroke, emoji → line icons)
4. Copy (plain words, no hype, no exclamation marks, no greeting)
5. Type (one family + at most one partner, weights 400–600, sentence case)
6. Layout (keep sections/order; real app proportions; one primary action)
7. Details (nested radii, quiet meta, one accent per chart, real hierarchy)
8. Visuals (filler goes; hero shows something true; product preview with
   a moment)
9. Motion (remove looping/bouncy; one easing curve; no animated layout
   properties)

Finish a pass across the whole screen before starting the next.

## 6. Check

- [ ] Run the checklist at the end of the `unslop` skill
- [ ] Render again, compare with the audit list — anything still on the
      list gets fixed
- [ ] Template check: if you swapped the product name for another
      product's, would the screen still fit? If yes, push the direction
      harder

## 7. Report

Direction, a few lines per pass about what changed, and any image prompt
written. Keep renders to at most three checks.
