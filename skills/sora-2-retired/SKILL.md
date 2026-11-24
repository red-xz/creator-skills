---
name: sora-2-retired
description: Sora 2 is discontinued — this is a record of what it was, what its best ideas were, and what to use instead. Use when someone suggests Sora 2 for a video, or when judging a new AI video tool against what Sora proved.
---

# Sora 2 — Retired (do not build on it)

> **STATUS — DISCONTINUED. DO NOT build a workflow around Sora 2.**
> OpenAI shut Sora down in 2026. This skill is kept as a record of what it
> was, what its best ideas were (Cameo / native audio), and what to use
> instead — so nobody wastes time or money chasing a dead tool.

## What it was

Sora 2 was OpenAI's text-to-video and image-to-video model, launched
September 30, 2025, with a standalone iOS app and a social feed. It
generated realistic video with physically accurate motion, world-state
persistence across shots, and — its signature feature — synchronised
dialogue and sound effects generated in the same pass as the video (no
separate TTS step).

Key features while live:

- **Native audio:** dialogue, sound effects and ambience generated with
  the video in one prompt, with automatic lip-sync.
- **Cameo:** a verified digital likeness of yourself (created in the iOS
  app by reading numbers aloud and moving your head). You — or anyone you
  gave permission to — could drop "you" into generated scenes. Public
  cameos (e.g. Sam Altman) could be used by anyone. This was the closest
  any mainstream tool came to the "same character in every video" problem.
- **Remix / storyboard / camera controls:** restyle a clip, direct shots,
  keep a scene consistent across cuts.
- **C2PA Content Credentials** watermarking on all output.

## Discontinuation timeline (verified, OpenAI help center)

- **March 24, 2026** — OpenAI notified developers the Sora 2 API would
  shut down.
- **April 26, 2026** — Sora web and iOS app experiences discontinued.
- **September 24, 2026** — Sora API (sora-2 / sora-2-pro) discontinued.
- OpenAI named **no replacement model** and no one-to-one replacement API.
- Old content can still be exported at `sora.chatgpt.com/sunset`
  (OpenAI recommends exporting as soon as possible; data is permanently
  deleted after any final export window).

Source: https://help.openai.com/en/articles/20001152-what-to-know-about-the-sora-discontinuation

## Pricing while it was live (historical — no longer purchasable)

- Consumer access was bundled in ChatGPT Plus ($20/mo) and Pro ($200/mo);
  there was no standalone Sora subscription. A free tier existed briefly
  (limited videos, 480p, watermark).
- Reported limits while live: Plus ~100 videos/mo at up to 1080p and 25
  seconds; Pro up to 4K and 60 seconds with priority generation.
  (Secondary sources; OpenAI's pricing pages are gone.)
- API: ~$0.10/sec (Standard 720p) to ~$0.70/sec (Pro 1080p) — a 10-second
  clip cost roughly $1–$7.

## Availability in Bangladesh

Sora 2 launched invite-only in the US and Canada (Sept 30, 2025). There is
no verified record of it ever opening generally in Bangladesh before the
April 2026 shutdown. A VPN would not have helped after shutdown — the
servers are gone. **Verdict: never usable from Bangladesh in practice, and
now unusable everywhere.** Do not pay anyone selling "Sora 2 access" or
invite codes — it is a scam.

## What to use instead (Nov 2026)

| | Sora 2 (dead) | Veo 3.1 in Google Flow | Kling 4.0 |
|---|---|---|---|
| Status | Discontinued Apr/Sep 2026 | Live | Live |
| Native dialogue + SFX | Yes, in one pass | Yes | Varies by mode |
| Consistent character | Cameo (likeness) | Ingredients-to-video (reference images) | Reference-image / elements |
| Best clip length | Up to 25–60s | 8s per clip | Up to 30s |
| Use for Shorts? | No — gone | Yes | Yes |

See the `veo-flow-ingredients` and `kling-shorts` skills in this bundle
for the live workflows.

## Lessons worth keeping (the ideas outlive the tool)

1. **Cameo proved the demand:** creators want a verified, reusable
   likeness so the same face appears in every video. Until a live tool
   offers this, use reference-image workflows (Veo Ingredients, Kling
   elements, character sheets) to hold character consistency.
2. **Native audio in one pass** (dialogue + SFX + lip-sync together) is
   the quality bar for new tools — judge any Sora successor on whether
   its mouth movements match its own audio, not on a separate TTS track.
3. **Vendor risk is real:** a tool can vanish in months even after a huge
   launch. Never build a channel's whole pipeline on one generator; keep
   at least two live alternatives warm (Veo + Kling today).

## Gotchas

- Many blogs and "pricing guides" still list Sora 2 as available with
  Plus/Pro prices — they are stale (some dated Oct 2026, after the
  shutdown). Always check `help.openai.com` before trusting any Sora
  claim.
- No waitlist, no invite, no paid tier brings it back. Anyone selling
  access is a scam.
- If old Sora clips still exist in an account, export them from
  `sora.chatgpt.com/sunset` before OpenAI deletes the data.

## When to use this skill

- When someone suggests Sora 2 for a video: answer is "it's shut down,
  use Veo 3.1 / Kling 4.0 instead."
- When evaluating a new AI video tool: use the Cameo + native-audio bar
  above as the comparison checklist.

## Sources

- OpenAI Help Center, "What to know about the Sora discontinuation":
  https://help.openai.com/en/articles/20001152-what-to-know-about-the-sora-discontinuation
- Timeline/capabilities cross-check: https://www.solidaitech.com/2026/05/sora-ai.html
  and https://www.pikyai.com/articles/sora-review-2026 (both confirm the
  April 26 / September 24, 2026 shutdown dates).
- Last verified: 2026-11-24.
