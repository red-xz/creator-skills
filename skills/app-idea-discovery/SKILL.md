---
name: app-idea-discovery
description: Find new app ideas from review mining, complaint mining, trends, and real local problems — then validate before building. Use when deciding what app to build next, or when checking whether one named idea is worth building.
---

# Finding New App Ideas

## The core rule: stop looking for ideas, find painful problems

- Profitable apps almost never come from inventing a brand-new idea. They
  come from solving a painful, existing problem better than the current
  options (solo-dev consensus, 2026).
- A good idea solves a **frequent, painful problem for a specific group of
  people who already look for solutions** — and ideally already pay for
  something in that space.
- Watch for **clumsy workarounds**: spreadsheets, paper notebooks,
  WhatsApp groups, repetitive copy-pasting, fragile manual processes. When
  people do a 5-step manual dance for an everyday job, that is a product
  waiting to exist. (A shop attendance app and a blood donor finder both
  came from exactly this pattern.)
- Competitors existing is a GOOD sign — it proves demand. No competitors
  usually means no demand, not an open field.

## The PAID / PAIN / GAP test (score every idea against this)

An idea is worth pursuing only when the evidence shows at least two of
three:

1. **PAID** — people already pay for something that does this job (a
   competing app, a service, a paper ledger they pay someone to keep).
2. **PAIN** — people complain about the current options, recently and
   repeatedly, in their own words.
3. **GAP** — a specific niche is ignored, overcharged, or buried in
   features it does not need.

Two of three earns user interviews. Three of three makes it a priority.
Zero or one: drop it, however exciting it sounds.

## Method 1: Review mining (the highest-signal method)

Read what people hate about apps that already exist — it is free, public,
and in their own words.

- Pick 3–5 competing apps in a category: the leader, a mid-tier app, and
  a fading app (recent reviews worse than old ones — users are looking
  for a way out).
- Read by star tier, not chronologically:
  - **1-star**: dealbreakers — crashes, surprise paywalls, feeling
    cheated. Acute pain.
  - **2–3-star**: feature gaps — users who want to love the app but
    cannot. These are your ideal early adopters; they articulate exactly
    what is missing.
  - **5-star**: the moat — what you must build just to get a seat at the
    table. Read for boundaries, not inspiration.
- Capture in a table: Date | App | Stars | Raw quote (exact words, do not
  paraphrase) | The job they were trying to do | Category tag (missing
  feature, pricing, reliability, design, support, privacy).
- Target ~100 reviews per competitor (roughly 40 recent 1-star, 40 recent
  3-star, 20 recent 5-star). Across 5 apps that is ~500 demand signals.
- Rewrite each complaint as a job-to-be-done: **"When I [situation], I
  want to [action], so I can [result]."**
- A theme that appears across SEVERAL competitors is a market gap, not
  one app's bug. A missing feature requested across several apps is a
  niche worth testing.
- Practical route: export reviews to CSV (e.g. Apify's App Store & Google
  Play Reviews Scraper — free tier exists; Apple only shares the latest
  ~500 reviews per app/country/sort, Google Play has no fixed limit),
  filter to 1–3 stars, and let an AI cluster them into ranked themes with
  quotes and counts. Weight complaints by thumbs-up count.
- Phrases to hunt for: "I wish it could…", "Please add…", "Used to be
  great until…", "too expensive for…", "why can't it just…".

## Method 2: Complaint mining in communities

- Search Reddit, Facebook groups/pages, YouTube comments, and niche
  forums for complaints in the category: "[category] + problem / hate /
  wish / alternative / too expensive".
- Facebook is especially useful for Bangladesh: people complain in
  Bengali in public groups and page comments about everyday services.
- Look for the same complaint from many people over time — one person's
  wish is a data point, a repeated wish is a pattern.
- Note: GummySearch (a Reddit-mining tool) shut down in Nov 2025 after
  losing Reddit API access — do not depend on a single platform's data
  tools.

## Method 3: Trend sources

- **Google Trends** (trends.google.com): check whether interest in the
  problem is stable, growing, or declining. A declining trend kills an
  idea no matter how good it sounds.
- **Google Play top charts / new releases** (Bangladesh + global): what
  categories are rising; which new apps are climbing fast.
- **Product Hunt** (producthunt.com): what new products launch daily;
  which get the most upvotes — a window into what early adopters want.
- **Appfigures / data.ai / Sensor Tower**: download and revenue estimates
  for competitors (free tiers are limited; paid data is optional, not
  required).
- **YouTube / TikTok / Facebook Reels**: what app-review and "best apps"
  videos are getting views — demand expressed as attention.

## Method 4: Your own life (best source for Bangladesh)

- Daily friction is a valid idea source: shop operations (attendance,
  salary, credit ledger), family needs (child vaccination records,
  medicine reminders), community needs (blood donors, mess management,
  local market prices).
- Ideas that worked came from real local problems, not from copying
  global trends. Prefer ideas where you can talk to 10 real users
  yourself (shopkeepers, neighbours, family).

## Validation — before writing any code

Run these in order; each step is cheap and each can kill the idea early.

1. **Write the problem, not the solution.** One sentence: who has what
   problem, how often, what it costs them in time or money.
2. **Assumption mapping.** List what must be true for the idea to work;
   rank by importance × least evidence. Test the riskiest assumption
   first.
3. **Problem interviews (10–20 people).** Talk to strangers who match the
   target user — never friends/family (they will be polite). Ask about
   their problem and current behaviour, NOT about your solution ("Would
   you use an app that…?" always gets a yes — it proves nothing). Read
   *The Mom Test* by Rob Fitzpatrick before the first interview — it is
   the standard guide to asking questions that do not lie to you.
4. **Smoke test landing page.** A one-page site describing the app with a
   signup button. Real signups (or pre-payments) are the strongest signal;
   expressed interest is the weakest. A page can be built and shared in a
   day.
5. **Concierge / Wizard of Oz test.** Deliver the service manually (over
   WhatsApp, by hand) before building the app. If nobody wants the manual
   version, nobody wants the app version.
6. **Pre-sale.** Ask for money before building. Even a small pre-payment
   is worth more than 100 "great idea!" comments.
7. **Score the survivors** (1–5 each): paid proof, pain intensity
   (frequency × cost × emotion), gap clarity, solo feasibility (one or two
   core flows, buildable and maintainable by one person), and your own
   access to the audience.

## Bangladesh-specific angles

- **Payments:** bKash and Nagad are how Bangladesh pays — bKash ~4.2 crore
  active users, Nagad ~2.8 crore (Oct 2026 figures); together MFS wallets
  move close to ৳6,000 crore/day. PayPal does NOT work in Bangladesh. Any
  app that takes money must plan for bKash/Nagad (via gateways like
  SSLCommerz, AamarPay, ShurjoPay) — never assume cards or PayPal.
- **Devices:** most users are on low-end Android phones with limited
  storage and slow connections. An app idea that needs a flagship phone or
  heavy downloads will not reach its audience. Keep APKs small, work
  offline where possible.
- **Language:** Bangla-first (or at least full Bangla) is a real
  differentiator — most global apps are English-only, and many
  Bangladeshi users are far more comfortable in Bangla.
- **USSD fallback:** MFS wallets work on feature phones via USSD (*247#
  bKash, *167# Nagad). For mass-reach ideas, consider whether a
  non-smartphone path matters.
- **Trust:** Bangladesh users are wary of new apps asking for money or
  personal data. Ideas that need sensitive data (health, money) need a
  clear trust story from day one.
- **Local problems beat global trends:** ideas rooted in Bangladeshi daily
  life (shop bookkeeping, school fees, crop prices, transport, religious
  calendar events, local services) face less competition than ideas copied
  from US app charts.

## Runbook: the idea hunt (60–90 minutes)

1. Pick a problem space (or ask for one audience).
2. Revenue-proof scan: find 5–10 paid products in the space — if nobody
   pays, stop.
3. Review-pain mining on the top 3–5 (Method 1).
4. Community complaint mining (Method 2).
5. Search-demand check on the top 3 candidates only (Method 3) — demand
   last, because it is the easiest signal to misread.
6. Write each surviving candidate as one narrow sentence: "[Tool that does
   one tedious job] for [specific niche] who currently use [workaround or
   paid tool] and complain about [pain]."
7. Score with PAID/PAIN/GAP + solo feasibility. Present the top 3 with
   evidence quotes and the score — never a bare list of ideas.

## Runbook: the idea check (one named idea, ~30 minutes)

1. Find the 3 closest paid competitors.
2. Mine their 1–3-star reviews for gaps.
3. Mine community complaints about the core job.
4. Check search demand.
5. Verdict: GO (evidence strong) / DIG DEEPER (one more test needed) /
   DROP (evidence weak) — with reasons.

## Honest limits — do not overpromise

- No method guarantees an idea will succeed. Validation reduces risk; it
  does not remove it.
- Review mining finds gaps in EXISTING categories — it will not surface
  ideas nobody has imagined yet. Pair it with trend-watching and your own
  life.
- Interview and landing-page signals are directional, not proof. People
  say yes and then never install.
- Competitor download/revenue estimates from free tools are rough — treat
  them as order-of-magnitude, not fact.
- An idea that scores well but you have no access to its audience (cannot
  reach the users, cannot talk to them) is a bad pick.

## Sources (researched 2026-11-22)

- GoDaddy, "How to validate an app idea before you build it" — https://www.godaddy.com/resources/skills/how-to-validate-an-app-idea
- Programming Insider, "10 Proven Frameworks for Validating Product Ideas" — https://programminginsider.com/10-proven-frameworks-for-validating-product-ideas-before-writing-a-single-line-of-code/
- Design and Tech, "How to Validate a Mobile App Idea Before Spending Money on Development" — https://www.designandtech.net/how-to-validate-a-mobile-app-idea-before-spending-money-on-development
- Unthinkable, "Mining App Store Reviews for Product Ideas" — https://unthinkableapp.com/blog/read-app-store-reviews-product-ideas
- dev.to, "Find your competitor's weak spots: export App Store and Google Play reviews and let AI sort the complaints" — https://dev.to/kazm_cemz_7f4650563415/find-your-competitors-weak-spots-export-app-store-and-google-play-reviews-and-let-ai-sort-the-5hl4
- Muaz.io, "How to Validate an App Idea with Competitor Research Before You Build" — https://muaz.io/blog/validate-app-idea-competitor-research/
- Synthiya, "How to find app ideas in App Store reviews" — https://www.synthiya.ai/guides/find-app-ideas-in-reviews
- Validated Idea Hunt (PAID/PAIN/GAP framework) — https://www.claudepluginhub.com/skills/carriegale2710-find-saas-plugins-find-saas/validated-idea-hunt
- Deshiz, "6 Best Mobile Banking Apps In Bangladesh (2026)" — https://deshiz.com/mobile-banking-apps-bangladesh/
- Deshiz, "9 Best Digital Wallets In Bangladesh (2026)" — https://deshiz.com/digital-wallets-bangladesh/
