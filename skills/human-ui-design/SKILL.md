---
name: human-ui-design
description: Design app UI that reads as human-made, not AI-generated — one choice per axis, design tokens, real references, every state designed. Use when designing or redesigning any app UI.
---

# Human UI Design

The rule this skill exists for: app UI must look 100% human-designed,
never AI-generated-looking. Users notice the difference, and they trust
the app less when it looks generated. Pair with the `unslop` skill — this
one is for designing from scratch, unslop is for fixing an existing screen.

## Why AI-generated UI looks generic (know the enemy)

A model given a vague prompt produces the most probable interface — an
average of everything it has seen. The recognizable fingerprint:

- **Default palette:** indigo-to-purple gradients, `indigo-600` buttons,
  slate greys. (Tailwind's co-founder Adam Wathan joked in Aug 2025 that
  he "turned every AI-built interface purple" by making Tailwind UI
  buttons `bg-indigo-500`.)
- **Component-library layout grammar:** hero → three identical feature
  cards → social proof → pricing → FAQ → footer. Same structure every
  time because it is the layout of every template.
- **Safe typography:** Inter for everything, default line-height, default
  tracking. Readable and entirely forgettable.
- **Incoherence:** the deepest problem. Each component is generated
  locally and plausibly, but the parts do not agree — a sharp-cornered
  card with pill buttons inside, one shadow lit from above-left and
  another from below, three different accent colours on one screen. A
  human designer picks one value per axis and repeats it everywhere; AI
  invents a new value per component.
- **Ideal-state only:** the happy path looks fine; empty, loading, error,
  and overflow states are missing or broken — a dead giveaway.

## The fix: one choice per axis, written down as tokens

Before building any screen, decide the sticky decisions ONCE and encode
them as design tokens (CSS variables in a plain HTML/CSS/JS stack). Never
let a new component invent a new value.

| Axis | Pick ONE, system-wide | Failure mode when mixed |
| --- | --- | --- |
| Corner / radius | sharp 0–4px · soft 8–12px · pill 9999px | sharp dialog + rounded buttons = "two products glued together" |
| Shadow | one scale, one light source (above), one tint | "a scene with two suns" |
| Accent colour | one accent for emphasis (+ semantic red/green/amber only) | nothing reads as important |
| Icon set | one set, one stroke weight, one size grid | mixed icon styles scream template |
| Type | one display face + one body face, one scale | font soup |
| Spacing | one unit (4dp/8dp grid) | random gaps feel accidental |
| Surface | one depth language (tonal colour shifts OR shadows, not both) | muddy hierarchy |

Concrete token file example (keep it per-app, never copy one app's tokens
into another):

```css
:root {
  --brand: #E11D48;        /* one accent, from the product's world */
  --brand-dark: #BE123C;
  --navy: #14213D;         /* dark text / header */
  --bg: #F4F5FA;
  --card: #FFFFFF;
  --text-2: #5B6478;       /* secondary text */
  --radius-card: 20px;     /* one card radius everywhere */
  --radius-btn: 999px;     /* one button radius everywhere */
  --space: 8px;            /* spacing unit; all gaps are multiples */
}
```

## Pick colours from the product's world, not from defaults

- Colour is the fastest signal a screen sends. An indigo-to-purple
  gradient instantly reads as "seen this before".
- Ask: what colours belong to THIS product's world? A blood donor app →
  deep medical red + navy (trust + urgency). A shop attendance app →
  mint/teal (calm, workday). A food app → warm spice colours. Never start
  from a library default.
- Put the palette in hex in the build brief — never "pick nice colours"
  (that is how indigo-500 happens).
- Check contrast: white text on `#6366F1` (Tailwind indigo-500) is ~4.47:1
  — just below the WCAG AA 4.5:1 bar for normal text. Verify every
  text/background pair; vibrant 2026 palettes can quietly break
  accessibility.
- Dark mode is a standard expectation in 2026, not a feature — design the
  dark theme as a first-class palette, not an inverted afterthought.

## One star per screen

- Every screen has ONE thing the eye should take away in 3 seconds. Make
  that the largest, boldest element. Everything else is supporting cast.
- Never a row of equal-sized stat cards with the same font weight — that
  is the AI default. Vary size, weight, and colour to create hierarchy
  (Nielsen Norman Group: visual hierarchy = arranging elements so the eye
  follows the order of importance you intend).
- Give layout rhythm, not three identical cards: vary card sizes, use a
  bento grid (mixed-size tiles), offset content, let one element bleed.
  Asymmetric layouts read as designed; perfectly centred stacks read as
  generated.

## Typography and spacing carry ~70% of perceived quality

- **Type scale:** use a defined scale with roles — Display, Headline,
  Title, Body, Label (Material 3 roles). Never more than two typefaces
  per app.
- **Minimum 16sp body text** on mobile. Smaller text excludes older users
  — a large share of Android users.
- **Spacing system:** define it early — 4/8/16/24/32dp. Consistent
  padding builds trust; random gaps feel accidental.
- **Bangla typography:** use Hind Siliguri or Noto Sans Bengali; Bengali
  script needs slightly larger line-height than Latin; never set Bengali
  text tiny (it becomes unreadable faster than Latin). Test every screen
  in Bangla, not just English — Bangla strings run longer and will
  overflow layouts sized for English.
- **Real copy, real content:** write copy for the actual user in their
  words, never lorem ipsum or generic placeholder text. Design with real
  data shapes (long names, long district names, missing photos) — fake
  tidy content hides overflow bugs.

## Design every state, not just the ideal screen

For every screen, design and verify: **empty** (no data yet), **loading**
(skeleton, not a blank screen), **error** (with a clear next action),
**overflow** (long text, long lists), **one item**, **many items**.
AI-built UIs almost always skip these — a human designer never does.

## 2026 design trends — what is current (late 2026)

The big split of 2026: Apple pulls toward quiet, glass-like restraint;
Google pushes toward bold, springy expression.

- **Material 3 Expressive** (Google, unveiled May 2025, rolled out through
  2025–26): the current Android design language. Dynamic colour (palette
  from wallpaper or a seed colour), 35-shape library with shape morphing,
  spring-based motion physics (stiffness/damping instead of fixed
  durations), emphasized typography, tonal surfaces instead of
  shadow-heavy depth. Rolled into Gmail, Chrome, Docs, Keep. This is the
  primary system for Android apps.
- **Liquid Glass** (Apple, iOS 26): translucent, glass-like surfaces,
  quiet restraint. Relevant only if an iOS version ever exists — do not
  copy Apple patterns into an Android app.
- **Motion physics:** animations follow spring physics now — bouncy,
  natural, responsive to touch. Fixed "300ms ease-in-out" is the old way.
  Use spring motion for component feedback (press, toggle, expand); keep
  durations short.
- **Bento grids:** mixed-size card tiles (named after Japanese lunch
  boxes) — a strong way to break the "three identical cards" pattern on
  home screens and dashboards.
- **Glassmorphism 2.0:** frosted panels used WITH PURPOSE — to create
  depth and separate layers (e.g. a floating bottom nav over content).
  Not glass everywhere for decoration.
- **Calm design:** 2026 is a year of clarity, trust, and craft after years
  of visual noise. Restraint reads as professional; decoration for its own
  sake reads as dated.
- **Micro-interactions:** small feedback moments — a button press that
  bounces, a heart that fills, a toggle that springs. They make an app
  feel alive and human. Keep them fast (<200ms) and purposeful; never
  decorative lag.
- **Bottom navigation** remains the standard for mobile apps; floating
  bottom nav with a raised centre action is the current premium pattern.
- **Accessibility is not optional:** WCAG contrast, touch targets ≥48dp,
  `prefers-reduced-motion` support (motion-physics animations must have a
  reduced-motion variant), dynamic text sizes.

## Component libraries and design systems

For a plain HTML/CSS/JS + Capacitor stack (web tech wrapped as Android
apps), NOT React:

- **Recommended:** hand-built CSS with design tokens following Material 3
  principles (tonal surfaces, M3 type scale, spring motion via CSS
  transitions). Tailwind CSS is an option for faster styling, but ONLY
  with a custom theme (custom colours, custom radius) — never Tailwind
  defaults, or the app will look like every AI-generated Tailwind app.
- **shadcn/ui** (free, MIT): the most widely adopted React component
  system in 2026 — components copied into your repo (not a dependency),
  Tailwind-styled, Radix/Base UI primitives, WAI-ARIA accessible. Use
  ONLY if a future app is React/Next.js. It is not usable in plain-HTML
  apps.
- **MUI** (React): implements Material Design; free core, paid advanced
  components; official Figma kit (paid).
- **HeroUI** (React, formerly NextUI): Tailwind v4 + React Aria
  accessibility, good-looking defaults.
- **Material Web** (@material/web): Google's web components for Material
  3 — in maintenance mode; usable but not where Google's energy is
  (Compose-first now).
- **Rule for any library:** a library gives you correct components, not a
  designed product. The tokens, the hierarchy, the copy, and the states
  are still your job. A library used with its defaults produces the
  generic look.

## Tools

- **Figma** (free starter plan): the standard design tool. Design the
  screens in Figma FIRST for any significant redesign, show the user
  screenshots, and only then build. Standing rule: show design photos
  first, then finalize.
- **Figma Make:** prompt-to-app inside Figma (closed beta, Mac only at
  last check) — useful for quick mockups, not a substitute for real
  design decisions.
- **v0** (Vercel): generates React + Tailwind + shadcn code from
  prompts/screenshots. Free tier; Plus ~$30/user/mo. React-only.
- **Subframe:** generates several UI variations side by side from
  screenshots, outputs React + Tailwind. Free tier; Pro ~$20/editor/mo.
- **Google Stitch** (Google Labs): quick UI exploration by text or voice
  — good for early exploration, not production code.
- **Honest limits:** AI design tools produce the generic look by default
  — they are only as good as the references, tokens, and constraints you
  feed them. Prices change often; check the pricing page before buying
  anything. None of these tools replaces the token discipline in this
  skill.

## References — study real products, don't guess

- Before designing, study 2–3 shipped apps in the same category and name
  ONE specific property to take from each (e.g. "bKash's pink brand +
  clean card hierarchy", "Pathao's bottom sheet pattern"). Vague
  references ("make it like a modern app") produce the average; specific
  references produce a design.
- For Bangladesh apps, study the Play Store screenshots of the top local
  apps (bKash, Nagad, Pathao, Chaldal) — they show what Bangladeshi users
  already understand.

## Pre-ship UI checklist (run before showing the user any design)

1. Tokens file exists and every colour/radius/shadow on screen comes from
   it — no hardcoded one-off values.
2. One star per screen — the 3-second glance test passes.
3. No indigo/purple default gradient anywhere; no three identical cards
   in a row.
4. Bangla + English both tested at real content lengths; no overflow at
   320px width.
5. Empty, loading, error, and overflow states designed and screenshotted.
6. Contrast checked on every text/background pair (WCAG AA 4.5:1 for body
   text).
7. Touch targets ≥48dp; reduced-motion variant exists.
8. Dark mode (if offered) is a real palette, not an inversion.
9. Screenshots taken at real phone size and shown to the user BEFORE
   finalizing (standing rule).

## What to avoid

- Indigo/purple gradients, default Tailwind colours, default shadcn theme.
- Three identical cards, vertically stacked centred sections, hero →
  features → pricing → FAQ structure.
- Inter for everything with no typographic hierarchy.
- Glassmorphism everywhere, heavy shadows, decoration that does not
  separate layers or guide the eye.
- Designing only the happy path.
- Copying a competitor's trade dress (logo, brand colours, distinctive
  layout) — take a property, not an identity.
- Rounded-2xl on everything: one radius personality per app, applied
  consistently.

## Sources (researched 2026-11-22)

- Wavespace, "8 UI Design Trends in 2026 (with real examples)" — https://www.wavespace.agency/blog/ui-design-trends
- Asapp Studio, "Android UI Tips 2026" — https://www.asappstudio.com/android-ui-tips-2026/
- Design Studio UI/UX, "16 Mobile App UI/UX Design Trends to Watch in 2026" — https://www.designstudiouiux.com/blog/mobile-app-ui-ux-design-trends/
- Android Authority, "Material 3 Expressive deep dive" — https://www.androidauthority.com/google-material-3-expressive-features-changes-availability-supported-devices-3556392/
- Supercharge, "Material 3 Expressive: New Components, Motion, Shapes, and More" — https://supercharge.design/blog/material-3-expressive
- "5 Things To Do So Your Web UI Doesn't Look AI-Generated" — https://main.d2vp3tpr4o6nqy.amplifyapp.com/blog/web-ui-not-look-ai-generated/
- Authon, "How to fix the 'AI-generated' look in your frontend" — https://blog.authon.dev/how-to-fix-the-ai-generated-look-in-your-frontend
- Refcat, "Why AI-Generated UI Looks Generic, and How to Fix It" — https://refcat.app/en/blog/why-ai-generated-ui-looks-generic-and-how-to-fix-it
- dev.to, "Why AI-Generated UIs Look 'Off' — and the One Principle That Fixes It" — https://dev.to/kiwibreaksme/why-ai-generated-uis-look-off-and-the-one-principle-that-fixes-it-4j20
- Subframe, "Best AI UI Design Tools in 2026 (Tested)" — https://www.subframe.com/tips/best-ai-ui-design-tools
- Create UI, "The 15 Best React UI Component Libraries in 2026" — https://createui.co/blog/best-react-ui-component-libraries
