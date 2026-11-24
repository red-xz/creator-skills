---
name: kling-shorts
description: Kling 4.0 for Shorts — character consistency with Omni Reference, honest cost math, and access from Bangladesh. Use when a Short needs AI video scenes and the same character must look identical across clips.
---

# Kling 4.0 for Shorts

Researched 2026-11-22. Kling was picked over Runway and Pika as the main
video tool because it is the best value in independent November 2026
testing, it has a real free tier, the longest single clips (30s), the most
reference assets per generation (15 vs Veo's 3), and it works from
Bangladesh with no VPN and plain Google sign-in.

## First: Sora 2 is dead, do not build on it

OpenAI announced the shutdown on March 24, 2026, closed the Sora consumer
app/web on April 26, 2026, and shut down the Sora 2 / Sora 2 Pro models
and the Videos API on September 24, 2026. OpenAI's developer docs state no
one-to-one replacement API is available. Any site or app still selling
"Sora 2 access" in late 2026 cannot be calling the real Sora models —
treat it as a scam. (See the `sora-2-retired` skill.)

## What Kling 4.0 is

- Kuaishou's video-generation model family, public since June 6, 2024.
  The current flagship is Kling 4.0, fully launched October 15, 2026
  (Flash variant September 28, 2026). Older models (1.6, 2.0, 2.5 Turbo
  Pro, 2.6, 3.0) are still in the model picker.
- Clips 3–30 seconds in one pass (1-second steps), 720p / 1080p / 4K,
  aspect ratios 21:9 / 16:9 / 1:1 / 9:16 / Auto, two-channel stereo audio
  with dialogue, SFX and ambience generated in sync with the picture,
  improved lip-sync, prompts up to 8,000 tokens.
- **Omni Reference:** up to 15 reference assets in one generation — up to
  10 images, up to 5 videos (≤30s total), up to 7 Elements (incl. up to 3
  video elements), up to 3 voice profiles (5–30s audio each). Elements
  bind a character's look AND voice across separate shots. This is the
  character-consistency system — far more reference slots than Veo's 3.
- **Keyframes:** up to 10 keyframe images placed along the timeline; the
  model animates between them. Use when a shot must land on exact beats
  (reveal, before/after). Keyframes and Omni Reference cannot be combined
  in one generation — pick one.
- **Multi-shot:** 4.0 splits a long prompt into shots on its own
  (multi-shot is on by default); 3.0 stitched up to 6 camera cuts into
  one 15s generation.
- **Motion brush + camera controls:** paint a motion path directly on a
  frame; pan/zoom/orbit/tilt camera moves. Note: as of October 2026 the
  dedicated Motion Control tool runs only on Kling 3.0 and 2.6, not 4.0 —
  in 4.0 use a reference video in Omni Reference to guide camera and
  performance instead.
- **Kling 4.0 Flash:** cheaper/faster draft tier — 720p, 3–20s, 8-bit SDR.
- **Coming soon (do NOT buy for these yet):** 10-bit HDR output (1080p/4K)
  and video extension up to 2 minutes. Both were still marked "coming
  soon" at launch.
- **Kling 3.0** (Feb 5, 2026) is still available: up to 15s clips, native
  4K, up to 60fps, multi-shot storyboards; it held the #1 public ELO
  benchmark score (1243) at launch. **Kling 2.5 Turbo Pro** remains the
  cheapest decent option for simple B-roll/drafts.
- **Audio languages (official):** dialogue in 9 languages — Chinese,
  English, Japanese, Korean, Spanish, Portuguese, German, French, Hindi —
  with accents (American/British/Indian English etc.). **Bengali is NOT
  supported.** Native dialogue works for English lines, not for Bengali
  dialogue — generate silent (or SFX-only) and dub your own voice track.
- On-screen text renders legibly in the supported languages, plus emoji
  and logos, and stays readable as the camera moves. Older models (2.5
  Turbo, 2.6) garbled on-screen text in independent November 2026 tests —
  use 3.0/4.0 when text must be readable.

## Access and cost — Bangladesh specifics

- Kling IS usable from Bangladesh. The global site is kling.ai — sign up
  with a normal email/Gmail or Google/Apple SSO. Do NOT use Kuaishou's
  mainland portal klingai.kuaishou.com (requires Chinese identity
  verification). No VPN needed; no Chinese phone number needed.
  International accounts contract with Kling AI Pte. Ltd., Singapore.
- Payment: USD via Stripe — Visa, Mastercard, Amex, international debit
  cards; Apple Pay / Google Pay in the mobile apps. No PayPal, no crypto,
  no bKash/Nagad directly. A Bangladeshi card must be enabled for
  international/dual-currency online payments, or it will be declined.
  Statement shows as `KLINGAI.COM SINGAPORE`.
- Bangladeshi resellers exist (payable by bKash/Nagad) but they are
  independent sellers, NOT official Kling partners. Prefer paying Kling
  directly; resold/shared accounts can be suspended and Kling support
  will not help you.
- Free tier: 66 credits/day, reset daily, no rollover. Output is
  watermarked and NOT licensed for commercial use — free output cannot go
  on a monetized channel. Slow queue. Still the right place to test.
- Paid plans (kling.ai membership page, re-checked Nov 9–17, 2026):
  - Standard: $10/mo list — 660 credits/mo ($6.99 first month, $8.80/mo
    renewal; ~$6.60/mo annual). Watermark-free, commercial use, 1080p/4K.
  - Pro: $37/mo list — 3,000 credits/mo ($25.99 first month, $32.56/mo
    renewal). Priority processing, priority access to new models incl. 4.0.
  - Premier: slider 8,000–38,000 credits — 18,000-credit default $207
    list ($144.99 first month, $181.99 renewal).
  - Ultra+: $619/mo list — 57,000 credits ($432.99 first month, $544.99
    renewal). Replaced the old $180 Ultra tier.
  - No credit rollover — unused monthly credits expire at the billing
    cycle.
- Credit burn (official Kling 3.0 model guide, Feb 2026): 6 credits/s at
  720p no audio, 8/s at 1080p no audio, 9/s at 720p with audio, 12/s at
  1080p with audio, 30/s at 4K. Kling 4.0 costs more: ~15 credits/s at
  1080p, ~10/s at 720p (Quantslant, Oct 15, 2026 — third-party, verify on
  the Generate button before committing). So one 10s 1080p silent clip on
  3.0 = 80 credits; with audio = 120; on 4.0 ≈ 150.
- API route: the official Kling API demands roughly $4,200 minimum over
  90 days — a non-starter for a solo creator. Third-party aggregators sell
  Kling with no minimum: PiAPI from ~$0.13/clip, fal.ai ~$0.15/video,
  roughly $0.07–$0.15 per generated second (rates observed Nov 2026,
  verify before use). Default to the web app unless a pipeline truly
  needs API calls.

## Honest volume math — read before promising anything

A 3-Shorts/day pipeline at 6 scenes × 10s = 180s/day ≈ 5,400s/month. At
3.0 1080p-no-audio (8 cr/s) that is ~43,200 credits/month. Pro (3,000 cr)
covers ~375s ≈ 6 Shorts/month; Premier 18,000 cr ≈ 37 Shorts/month
(~$182–207/mo); only Ultra+ (57,000 cr, ~$545–619/mo) covers the full
pipeline. With native audio (12 cr/s) Pro covers ~4 Shorts/month. On 4.0
(~15 cr/s) Pro covers ~3 Shorts/month. **Kling is for hero scenes, key
characters, and tests — NOT a drop-in replacement for a whole 3/day
pipeline at current volume.** The free tier alone covers about one 10s
720p silent clip per day. The cheapest path to more volume is 2.5 Turbo
Pro for drafts/B-roll + 3.0/4.0 for hero shots.

## The workflow (kling.ai web app)

1. Story first, in one sentence — who it is about, what changes, where it
   ends. That sentence decides the references.
2. Build references BEFORE generating any video. Make the character, key
   locations, and style as reference images first (reuse approved
   character sheets). A character designed after the first scene exists
   will never quite match it.
3. Choose the entry point: Omni Reference (default — images/video/voice/
   Elements, most control) or Keyframes (exact beats, images only). Never
   both in one task.
4. Give every reference ONE job and name its role in the prompt — Kling
   auto-numbers uploads (@Image1, @Video1). Write "@Image1 defines the
   character — preserve her face, hairstyle, and pink floral dress" not
   just "@Image1". If you give only IDs without roles, the model guesses
   and results vary.
5. Test one clip, check it holds, then reuse the approved reference set
   across every clip in the series. Record which set produced the approved
   result.
6. Draft cheap, finish expensive: block the scene on 4.0 Flash or 2.5
   Turbo Pro, then re-run the approved setup on 3.0/4.0 for the keeper.

## Prompt structure (roles → settings → timed beats → audio)

Kling's own template — describe visuals explicitly, minimize abstract
terms and negative instructions. The only two negatives usually needed are
"no subtitles" and "no background music" (the model may add them by
default):

```
[Asset roles]
@Image1 defines ___; preserve its ___.
@Image2 defines ___; preserve its ___. Reference the ___ of @Video1.

[Overall settings]
Scene and texture: ___; visual style: ___; camera tone: ___.

[Sequence of events]
0–X s: ___ (visuals + action + emotion)
X–Y s: ___ (camera movement + additional details)
Y s–end: ___ (closing shot)

[Audio]
Dialogue/voiceover + ambient sounds + music + sound effects
```

- One camera move per shot. A slow push-in, a pan, or a handheld follow —
  not all three.
- Describe action in beats ("takes four steps to the window, pauses,
  pulls the curtain"), not summaries.
- Name the light ("soft window light from the left") and 3–5 palette
  colors when shots must match in an edit.
- Dialogue: put it in its own block with speaker labels; keep lines
  short — a short clip fits one or two exchanges. In 4.0 you can specify
  each speaker's language, tone, pauses, gestures, and emotional response.
- Duration is a setting, not prose — writing "make it longer" in a prompt
  changes nothing; set 3–30s in 1-second steps.
- Change one thing at a time when a shot fails: freeze the camera,
  simplify the action, add detail back slowly.

## Vertical (9:16) rules

- Generate native 9:16 — never crop landscape afterward. A face framed
  for 16:9 becomes too small or loses hand actions after cropping.
- Keep face and key action in the center-safe area; leave headroom for
  movement without an empty top half.
- Avoid wide side-by-side staging of two people unless both stay readable.
- Reserve lower-screen space for the captions/CTA text added later.
- Prefer forward, upward, or depth-based motion on a tall screen.

## Where it fits (and where it does not)

- **History Shorts (best fit):** lock the historical figure's face +
  period setting as Elements/Omni references across all scenes;
  image-to-video from a period still gives the strongest realism per
  dollar. A single 30s 4.0 clip can cover up to 3 scenes via multi-shot.
  Native English dialogue works for in-scene character lines with
  lip-sync; use native audio for ambience/SFX and keep a TTS narrator
  on top.
- **Character comedy:** a full character sheet fits in Kling's 7 Elements
  / 15 references where Veo's 3 slots cannot. Bengali dialogue is NOT
  supported — generate silent (or SFX-only) and dub your own voice track.
  Do NOT fake it with Hindi dialogue.
- **Real-footage lines (gameplay, wildlife):** do NOT use Kling — those
  lines are real-footage-only by standing rule.

## QA checklist (check in this order — identity, motion, composition, audio, resolution)

- Character identity stable through the whole clip (face, hair, outfit) —
  check frame by frame at scene boundaries, not just whole-second
  checkpoints.
- No portrait-still opening: verify the first ~1s is actually animating,
  not a frozen reference frame.
- Object shape/colors/details correct; environment supports rather than
  overwhelms the subject.
- 9:16 composition designed vertically, not cropped.
- Dialogue fits the clip length and the right character appears to speak;
  lip-sync holds (independent tests: sync drifts slightly on fast
  consonants past ~10s — keep dialogue clips short); ambience matches
  visible events; no sound starting/ending unnaturally at clip edges.
- On-screen text legible (use 3.0/4.0 for text; 2.5 Turbo/2.6 garble it).
- Upscale to 1080p/4K ONLY after the creative result passes QA —
  upscaling never fixes a drifting face or wrong identity.

## Fixing common failures

- Character close but not identical → sharper identity reference; state
  each reference's role explicitly; remove references showing different
  ages/hairstyles/angles; reuse the same approved set. Use an Element
  (look + voice bound) instead of a loose image.
- Object right in one frame, wrong in another → simplify the interaction,
  reduce rotation/occlusion, give the object more screen size.
- Location dominates the subject → environment reference too strong or
  prompt overemphasizes it; make subject/action more explicit.
- Result looks like a collage → stop listing references; describe one
  coherent scene with spatial relationships and timed beats.
- Vertical feels cramped → re-plan for 9:16 before generating; move
  interactions to frame center.
- Generation rejected by the filter: Kling's 2026 "sensitive" moderation
  throws false positives on swimwear, dance, yoga, fashion with bare
  shoulders (three layers: prompt classifier, uploaded-image screen,
  output-frame check). Re-crop the reference, reword the prompt, or
  simplify the shot — do not keep resubmitting the identical prompt.
- Lip-sync drifting → shorten the dialogue clip; split a 15s monologue
  into two shorter generations.

## Guardrails (non-negotiable)

- YouTube AI disclosure = YES for any Short containing Kling clips.
  Disclosing does not hurt reach (YouTube's own words).
- Commercial use only on paid plans. Free-tier output is watermarked and
  not licensed for commercial use — never publish free-tier output. Keep
  burning the channel logo watermark on every video regardless.
- Data & IP: Kuaishou is Beijing-based; content is processed on servers
  in China under Chinese data law, and the terms grant rights to use
  uploaded material for model training. Do not upload unreleased IP,
  confidential storyboards, or anything a legal team would flag. Kling
  does not indemnify you — its terms require YOU to indemnify Kuaishou.
  For sensitive material, route through an aggregator (fal.ai/PiAPI) and
  keep the confidential material off kling.ai.
- Do NOT generate real identifiable people (including public figures) —
  characters are fictional; stay inside the policy.
- Never promise Kling for a full 3/day pipeline without the user
  approving the cost first (see volume math above). Default to the free
  tier for tests.
- Do NOT use third-party "free Kling API" resellers or shared accounts —
  use Kling's own web app, or a named aggregator (PiAPI/fal.ai) for API
  access only.

## Sources (checked 2026-11-22)

- Official: Kling 4.0 User Guide — https://kling.ai/quickstart/kling-4-model-user-guide
- Official: Kling 4.0 global launch press release, Oct 16, 2026 (GlobeNewswire) — https://www.wcia.com/business/press-releases/globenewswire/9847342/kling-ai-launches-kling-4-0-globally-with-professional-grade-output-stable-motion-and-multimodal-control/
- Official: Kling blog, "Best AI Voice Generator" — https://kling.ai/blog/best-ai-voice-generator
- Pricing (membership page re-checked Nov 9–17, 2026 by Litmus + allable.ai); credit rates: Kling 3.0 model guide (Feb 2026); Kling 4.0 ~15 cr/s at 1080p (Quantslant via cinemadrop, Oct 15, 2026 — third-party).
- Litmus Kling AI Review, re-checked Nov 9, 2026 — https://litmustools.com/review/kling/
- Kling 4.0 guide/status table — https://www.cinemadrop.com/blog/kling-4-0
- Model comparison test, Nov 12, 2026 (MyEdit) — https://myedit.online/en/blog/kling-models-compared
- Bangladesh access/payment: StackMatchup — https://stackmatchup.com/kling-ai-pricing-data-residency-access/
- Sora 2 shutdown: Superprompt guide citing OpenAI's own docs/deprecations list, checked Nov 12, 2026 — https://superprompt.com/blog/openai-sora-2-complete-guide
