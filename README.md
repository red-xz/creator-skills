# Creator Skills

Skills for an AI agent that helps a small creator actually ship things —
Shorts, thumbnails, app UIs, Firebase apps, storefronts — instead of just
talking about them.

12 skills · 4 workflow commands · 3 templates. Built while running two
YouTube channels and two small Firebase apps from Bangladesh, so a lot of
the notes are about what is cheap, what is free, and what quietly breaks
when you are not in the US.

## Quickstart

```bash
git clone https://github.com/red-xz/creator-skills.git
# copy skills/ into your AI coding agent's skills directory, e.g. ~/.claude/skills/
cp -r creator-skills/skills ~/.claude/skills/
```

The agent discovers skills by their frontmatter descriptions and loads the
relevant one when the task matches — e.g. "write the title and description
for this Short" loads `youtube-shorts-seo`. `commands/` and `templates/`
are plain Markdown. Paste them into your agent's context or your own notes
when you need the checklists.

## Where this came from

I run two YouTube channels — **History They Never Taught You** (history
Shorts, three a day at peak) and **GTA 6 Secrets** (real gameplay clips
plus commentary, nothing AI-generated on screen) — and two Firebase apps:
a blood donor finder and a shop attendance app. These skills are the
checklists I ended up writing for myself after making the same mistakes
more than once.

A few things I learned the hard way, baked into the skills:

- The topic decides whether a Short moves, not the metadata. Metadata wins
  the first test audience; after that, viewer behaviour rules. I spent too
  long polishing titles for videos nobody wanted to watch.
- Every AI video tool will eventually die or change price. Sora 2 — the
  biggest launch of 2025 — shut down in April 2026. There is a skill in
  here that is just a record of that, so nobody pays a reseller for access
  to a dead tool.
- "AI-looking" UI is a real problem, not a vibe complaint. Users notice
  the purple gradients and the three identical cards, and they trust the
  app less. Two skills in this bundle exist only to fix that.
- Firebase's free tier covers a surprising amount — hosting, auth,
  push notifications, test distribution — but the moment you need a
  server-side trigger, you hit the Blaze wall. The Firebase skills say
  exactly where that wall is.

## Skills

| Skill | What it covers |
|---|---|
| `youtube-shorts-seo` | Titles, descriptions, tags, thumbnails, retention editing, and diagnosing a stalled Short |
| `youtube-hype-2026` | Hype (free + paid), the Oct 2026 Shorts originality change, and the Feb 2027 Partner Program bar doubling |
| `kling-shorts` | Kling 4.0 for Shorts — character consistency, honest cost math, Bangladesh access |
| `veo-flow-ingredients` | Veo 3.1 Ingredients-to-Video in Google Flow — same character across scenes |
| `sora-2-retired` | Sora 2 is shut down. What it was, what to use instead, and how to spot the scams selling "access" |
| `unslop` | The 9-pass fix for AI-looking UI — spacing, colour, icons, copy, type, layout, details, visuals, motion |
| `human-ui-design` | Designing app UI that reads as human-made: tokens, one choice per axis, real references, every state designed |
| `firebase-app-distribution` | Ship APK builds to testers by email, no Play Store needed |
| `firebase-push-notifications` | FCM push for web + Android — topics, quotas, and the Spark-plan limits |
| `animated-storefront` | The gliding product-rail hero for a small shop site — pure CSS or GSAP |
| `app-idea-discovery` | Finding app ideas from review mining, complaint mining, and real local problems — then validating before building |
| `web-security-defense` | Defensive web security only: OWASP Top 10:2025, hardening checklists, responsible disclosure |

## Commands

Checklist-style workflow docs in `commands/`:

- `package-a-short.md` — title, description, tags, thumbnail, related
  video, and the pre-upload checks for one Short
- `plan-a-shorts-week.md` — pick the week's topics, check they are not
  already covered, and spread them across the week
- `unslop-a-screen.md` — run the unslop audit and nine passes on one screen
- `check-an-app-idea.md` — the 30-minute verdict on one named app idea

## Templates

Fill-in templates in `templates/`:

- `short-script.md` — the 60-second Short script structure: hook, beats,
  payoff, CTA
- `short-metadata.md` — title / description / tags / hashtags, filled in
  per Short
- `app-idea-one-pager.md` — one page per app idea: problem, evidence,
  PAID/PAIN/GAP score, verdict

## Learning path

`docs/learning-path.md` maps the skills onto a first-month plan: week 1
Shorts packaging, week 2 video generation, week 3 app UI, week 4 Firebase
and app ideas. It assumes an hour or two a day and no prior experience.

## How to use with an AI coding agent

This bundle follows the [Agent Skills open standard](https://agentskills.io):
each skill is a `skills/<name>/SKILL.md` file with frontmatter (`name`,
`description`). Copy the `skills/` folder into your agent's skills
directory (for example `~/.claude/skills/` for Claude Code, or your
agent's equivalent) and the agent loads the right skill for the task.

## The honest version

- These skills will not make a video go viral. Nothing does that
  reliably. What they do is stop you losing views to fixable mistakes —
  a dead first two seconds, a title that buries the keyword, a thumbnail
  that repeats the title, a UI that screams "generated".
- Small channels do break out on one Short. I have seen 98-subscriber
  channels pull 20K views on a single video. Size is not the gate; the
  video is. But most Shorts will not break out, and the back catalog does
  most of the work over time — which is why you never delete a slow
  starter.
- AI video tools are rented, not owned. Budget for the tool dying, the
  price doubling, or the free tier shrinking. Keep two live alternatives
  warm at all times.

## Contributing

Small, specific contributions are welcome — see [CONTRIBUTING.md](CONTRIBUTING.md).
Beginner-friendly tasks are listed in [GOOD-FIRST-ISSUES.md](GOOD-FIRST-ISSUES.md).

## License

MIT — see `LICENSE`. The `unslop` skill adapts work by Damir Sokolovsky
(CC BY 4.0) and keeps his credit inside the skill file.

---

If this helps you ship something, star it — it helps other small creators
find it.
