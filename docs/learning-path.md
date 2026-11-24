# Learning Path — First Month

This maps the skills in this bundle onto a first-month plan. It assumes
~1–2 hours a day and no prior experience. Slow down rather than skip: a
shallow pass over every skill is worth less than fluency in three.

## Week 1 — Shorts packaging

The highest-leverage week. Most small channels lose views to fixable
packaging mistakes, not to the algorithm.

- Read `youtube-shorts-seo` end to end. Then take one of your own Shorts
  (or a Short you admire) and score it against the retention rules: payoff
  within 2.5s? Something changing every 3–8s? Loop opened early, payoff
  held to 55–85%?
- Read `youtube-hype-2026`. Know where Hype fits (500 subs + YPP,
  long-form only, first 7 days) and what the Feb 2027 bar doubling means
  for your monetization plan. Do not chase Hype before 500 subs.
- Exercise: package three Shorts on paper using
  `commands/package-a-short.md` + `templates/short-metadata.md` — title,
  description, tags, thumbnail concept — before producing any of them.
  Decide the title and thumbnail before production, every time.

Skills: `youtube-shorts-seo`, `youtube-hype-2026`

## Week 2 — Video generation

- Read `sora-2-retired` first (5 minutes). It exists so you never pay a
  reseller for access to a dead tool, and so you judge new tools against
  the Cameo + native-audio bar.
- Read `veo-flow-ingredients`, then `kling-shorts`. Compare them on the
  thing that matters for your content: Veo gives you 3 reference images
  and 8-second clips with native audio; Kling gives you 15 reference
  slots, 30-second clips, and better character consistency for
  multi-character scenes — but no Bengali dialogue.
- Do the volume math for your own pipeline before spending anything. A
  3-Shorts/day pipeline at 6 scenes each is ~540 clips/month; a Pro
  subscription on either tool covers a small fraction of that. Both tools
  are for hero scenes and tests at solo-creator budgets, not for the whole
  pipeline.
- Exercise: build one character reference set (character sheet or
  ingredients), generate one test clip on the free tier of each tool, and
  check it against the QA checklist — identity first, then motion,
  composition, audio, resolution. Upscale only after the creative result
  passes.

Skills: `sora-2-retired`, `veo-flow-ingredients`, `kling-shorts`

## Week 3 — App UI that does not look generated

- Read `human-ui-design`. The core idea is one choice per axis, written
  down as tokens before any screen is built. Pick a real app you use and
  name its token choices: one radius, one accent, one icon set, one type
  scale.
- Read `unslop`. Then take a screen you built (or any AI-generated UI)
  and run the audit: list every slop sign, one line each. Write the five
  direction lines before touching anything.
- Exercise: run `commands/unslop-a-screen.md` on one real screen. Fix the
  passes in order — spacing first, visuals and motion last. Render at
  most three times.
- Exercise: design one screen's empty, loading, error, and overflow
  states. If you have only ever designed the happy path, this is the week
  that changes.

Skills: `human-ui-design`, `unslop`

## Week 4 — Firebase and app ideas

- Read `firebase-app-distribution` and `firebase-push-notifications`.
  The key facts: both are no-cost on the Spark plan; App Distribution
  replaces expiring download links with a permanent tester channel; FCM
  topics (`blood_Apos_Dhaka`) are the targeting mechanism; Cloud
  Functions — the automatic trigger — needs Blaze, so on Spark you send
  from the console or an external server.
- Exercise: set up App Distribution for a test build and invite one
  tester (yourself). Ship one build through it end to end.
- Read `app-idea-discovery`. Then run `commands/check-an-app-idea.md` on
  one idea you have been carrying around — the 30-minute verdict. If it
  scores below 2 on PAID/PAIN/GAP, drop it and move on. The skill is as
  much about dropping ideas as finding them.
- Read `web-security-defense` and run the hardening checklist on any site
  you own. Headers, updates, backups, 2FA — the boring half of security
  is most of it.

Skills: `firebase-app-distribution`, `firebase-push-notifications`,
`app-idea-discovery`, `web-security-defense`

## After month 1 — go deeper where it pays

- **Shorts:** the next level is topic selection, not more metadata work.
  Study which topics break out for channels your size, and repeat the
  format that worked — packaging first, volume second.
- **Video:** keep two live tools warm at all times. When one dies or
  doubles in price (and one will), you switch the same week instead of
  rebuilding the pipeline.
- **Apps:** the storefront skill (`animated-storefront`) is the next
  build — a product-rail hero for a real shop, starting with the pure-CSS
  pattern. Ask the owner the questions in the skill before building.
- **Security:** PortSwigger Web Security Academy (free) is the long
  learning path; the skill's labs section has the rest.

## Standing rules

- One target phrase per video. One accent per screen. One star per
  screen. One program at a time for security work.
- Never delete a slow starter. Never delete and repost.
- Never publish free-tier video output on a monetized channel.
- Never put a service-account key or tester emails in a public repo.
- AI disclosure = YES on any video containing AI-generated clips.
- Keep two video tools warm. Vendor risk is real — Sora 2 proved it.
