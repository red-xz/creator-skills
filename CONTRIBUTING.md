# Contributing to Creator Skills

Contributions are welcome — this bundle is built by a small creator, for
small creators. You do not need to be an expert to contribute.

## How to contribute

1. Fork the repo and create a branch for your change.
2. Keep changes small and focused — one skill, one fix, or one template
   at a time.
3. Open a pull request with a short description of what changed and why.

## Good first contributions

See [GOOD-FIRST-ISSUES.md](GOOD-FIRST-ISSUES.md) for small, well-scoped
tasks: new skills, translations, template improvements, typo fixes.

## Ground rules

- **Original content.** Write in your own words from public knowledge
  and your own experience. Do not paste content from other repos,
  courses, or books. (The one exception is `unslop`, which adapts Damir
  Sokolovsky's CC BY 4.0 work and keeps his credit.)
- **No real private data.** Never include real credentials, API keys,
  phone numbers, account IDs, or tester emails. Examples use placeholders
  (`user@example.com`, `YOUR_VAPID_KEY`, `<APP_ID>`).
- **Honest about tools.** If a tool shut down, changed price, or is not
  available in a region, say so plainly with a date and a source. Stale
  tool claims are the fastest way to waste someone's money.
- **Defense only for security.** The `web-security-defense` skill covers
  hardening, auditing your own systems, and responsible disclosure. No
  offensive content, no attack payloads, no exploitation guides.
- **Plain language.** The reader is a beginner creator. Explain the
  jargon the first time you use it. No filler, no hype words, no
  "in today's fast-paced world".
- **Human-made, not AI-looking.** This repo is held to the same standard
  as the skills inside it: write like a person, with real examples and
  opinions, not generic filler.

## Skill format

Each skill is `skills/<name>/SKILL.md` with frontmatter:

```yaml
---
name: skill-example
description: What this skill covers, and when the agent should load it.
---
```

Body structure: what it is → when to use it → the working method (with
real numbers and real examples) → honest limits and gotchas → guardrails
→ sources with dates.
