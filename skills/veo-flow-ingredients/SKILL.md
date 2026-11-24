---
name: veo-flow-ingredients
description: Veo 3.1 Ingredients-to-Video in Google Flow — lock a character's face, outfit, and style from reference images so the same character looks identical across scenes. Use when a Short needs character consistency across clips.
---

# Veo 3.1 Ingredients-to-Video in Google Flow

Researched 2026-11-22. The problem this solves: character drift. Ask a
video model for "the same girl" six times and you get six different girls.
Veo 3.1's Ingredients to Video locks a character's face, outfit, and style
from reference images instead of re-describing them in text every clip.

## What it is

- Google DeepMind's video model. Launched Oct 15, 2025; the update that
  matters is Jan 13, 2026 (official blog.google post): Ingredients to
  Video got much better identity consistency, native 9:16 vertical
  output, and upscaling to 1080p and 4K. A cheaper Lite tier was added
  March 2026.
- Clips are 4, 6, or 8 seconds, 720p/1080p/4K, 16:9 or 9:16, 24 fps, with
  native synchronized audio — dialogue, sound effects, ambience generated
  in the same file, lip-synced to the picture.
- Three control modes:
  - **Ingredients to Video**: up to 3 reference images (character /
    object / environment-style) guide one 8-second clip. This is the mode
    for character consistency.
  - **Frames to Video**: supply a first frame and a last frame; Veo
    generates the motion between them, with audio. Use when the shot must
    land on an exact ending (reveal, before/after).
  - **Extend**: continues a clip from its final second, so a scene can
    run a minute or more.
- All outputs carry an invisible SynthID watermark. That does NOT replace
  a burned-in logo watermark — keep burning the channel logo on every
  video.
- Access change (Oct 22, 2026): Google shut down the Veo 3.1 preview
  models in the Gemini API. The routes now are Google Flow
  (flow.google.com, consumer UI) or Vertex AI / Gemini Enterprise Agent
  Platform (API). The Gemini API's successor model is Gemini Omni Flash
  (per-token billing) — different model, do not confuse the two.

## Access and cost — Bangladesh specifics

- Google Flow IS available in Bangladesh (official Google Flow Help
  country list) and Google AI Pro is officially sold there.
- Free tier: 50 Flow credits/day, no subscription. That buys ~5 Veo 3.1
  Lite clips/day (10 credits each) or ~2 Fast clips (20 each). Video
  generation may be blocked at peak hours (~8–11 PM Bangladesh time).
  Start here — test free before paying anything.
- Google AI Plus: ৳600/month — 200 credits/month. Google AI Pro:
  ৳2,500/month — 1,000 credits/month. Per-clip cost on Pro: Lite 10
  credits (~100 clips/mo), Fast 20 (~50 clips/mo), Quality 100 (~10
  clips/mo). Extra AI credits can be bought on paid plans.
- Vertex AI API (pay-per-second, with audio): Standard $0.40/s ($3.20 per
  8s clip), Fast $0.10–0.12/s ($0.80–0.96), Lite $0.05–0.08/s
  ($0.40–0.64). Silent is roughly half price.
- Honest volume math — read before promising anything: a 3-Shorts/day
  pipeline at 6 clips each = 18 clips/day ≈ 540 clips/month. A Pro
  subscription covers ~50 Fast clips/month. Vertex Fast for the full
  pipeline would be ~$500/month. **Veo is for hero scenes, key
  characters, and tests — NOT a drop-in replacement for a whole 3/day
  pipeline at current volume.** The free tier alone covers roughly one
  6-scene Short per day on Lite.

## The workflow (Flow)

1. Story first, in one sentence — who it is about, what changes, where it
   ends. That sentence decides the ingredients.
2. Build ingredients BEFORE generating any video. Make the character, key
   locations, and style as reference images first (use Nano Banana Pro /
   Gemini 3 Pro Image inside Flow or the Gemini app — Google's own pro
   tip — or reuse approved character sheets). A character designed after
   the first scene exists will never quite match it.
3. Give every ingredient ONE job (max 3):
   - Character: face, hair, outfit, body identity. Use a sharp, evenly
     lit, front-facing reference; include enough of the body to show the
     outfit.
   - Object/product: shape, materials, readable details.
   - Environment/style: location look, lighting direction, visual
     language.
   - Do not mix a cartoon character with a photorealistic product and a
     stylized environment unless the clash is intentional.
4. Test one clip, check it holds, then extend the keepers and join them in
   Flow's Scenebuilder timeline.
5. Reuse the approved ingredient set across every clip in the series.
   Treat the reference set as a reusable asset, not a disposable
   attachment. Record which set produced the approved result.

## Prompt structure (invariants → action → audio)

Separate what must stay stable from what happens:

1. **Invariants first**: "Use the supplied girl as the same character,
   the supplied village courtyard as the environment. Preserve her pink
   floral dress, braid, and the courtyard's mud walls and tin roof."
2. **Action + camera**: "She runs across the courtyard toward camera,
   laughing, and stops at the doorway. Handheld medium shot, slow
   push-in. Warm late-afternoon sunlight."
3. **Audio only when needed**: name sounds tied to visible events
   ("[Ambient: village birds, distant goat bell]", one short spoken line
   with the speaker named). Keep dialogue to ONE short sentence per 8s
   clip, and do not stack several dramatic camera moves on top of dialogue
   — more simultaneous constraints = more failure modes.
4. Describe one coherent scene, not a list of the references — listing
   them separately produces a collage look.

## Vertical (9:16) rules

- Generate native 9:16 — never crop landscape afterward. A face framed
  for 16:9 becomes too small or loses hand actions after cropping.
- Keep face and key action in the center-safe area; leave headroom for
  movement without an empty top half.
- Avoid wide side-by-side staging of two people unless both stay readable.
- Reserve lower-screen space for the captions/CTA text added later.
- Prefer forward, upward, or depth-based motion on a tall screen.

## Where it fits (and where it does not)

- **History Shorts**: lock the historical figure's face + the period
  setting as ingredients across all 6 scenes. Best use case — one figure,
  many scenes.
- **Multi-character comedy**: 3 slots is a real limit — three characters
  leaves no room for environment. Use a group sheet as the character
  ingredient and describe the environment in text, or one character +
  environment for solo scenes. (Kling's 15 reference slots fit this
  better — see `kling-shorts`.)
- **Voice/mouth matching**: native dialogue audio generated in Veo can
  fix the voice/mouth mismatch — generate the line IN Veo so lips match,
  instead of dubbing TTS over a silent clip. Test this on one scene
  before committing.
- **Real-footage lines (gameplay, wildlife):** do NOT use Veo — those
  lines are real-footage-only by standing rule.

## QA checklist (check in this order — identity, motion, composition, audio, resolution)

- Character identity stable through the whole clip (face, hair, outfit).
- Object shape/colors/details correct; environment supports rather than
  overwhelms the subject.
- 9:16 composition designed vertically, not cropped.
- Dialogue fits the clip length and the right character appears to speak;
  ambience matches visible events; no sound starting/ending unnaturally
  at clip edges.
- Upscale to 1080p/4K ONLY after the creative result passes QA —
  upscaling never fixes a drifting face or wrong identity.

## Fixing common failures

- Character close but not identical → sharper identity reference; remove
  style conflicts; drop references showing different ages/hairstyles/
  angles; reuse the same approved set.
- Object right in one frame, wrong in another → simplify the interaction,
  reduce rotation/occlusion, give the object more screen size.
- Location dominates the subject → environment reference too strong or
  prompt overemphasizes it; make subject/action more explicit.
- Result looks like a collage → stop listing references; describe one
  coherent scene with spatial relationships.
- Vertical feels cramped → re-plan for 9:16 before generating; move
  interactions to frame center.

## Guardrails (non-negotiable)

- YouTube AI disclosure = YES for any Short containing Veo clips.
  Disclosing does not hurt reach (YouTube's own words).
- Flow policy: no editing uploaded videos of identifiable minors; no
  generating videos of prominent people. Characters are fictional — stay
  inside the policy, never generate a real person.
- Never promise Veo for a full 3/day pipeline without the user approving
  the cost first (see volume math above). Default to the free tier for
  tests.
- Do NOT use third-party "free Veo API" resellers or shared accounts —
  use Google's own Flow/Vertex routes only.

## Sources (checked 2026-11-22)

- Official: blog.google "Veo 3.1 Ingredients to Video" (Jan 13, 2026, Ricky Wong, Google DeepMind) — https://blog.google/innovation-and-ai/technology/ai/veo-3-1-ingredients-to-video/
- Official: Google Flow Help, supported countries (Bangladesh listed) — https://support.google.com/labs/answer/16353544
- Official: Google AI Pro support page (Bangladesh listed) — https://support.google.com/googleone/answer/16476811
- Pricing (Vertex AI page, checked Oct 25 / Nov 11, 2026 by multiple trackers): Standard $0.40/s, Fast $0.10–0.12/s, Lite $0.05–0.08/s with audio; Gemini API Veo previews shut down Oct 22, 2026.
- Bangladesh plan prices (Nov 2026 guides, from Google's BD subscription page): Plus ৳600/mo, Pro ৳2,500/mo.
- Workflow detail: media.io Veo 3.1 Ingredients tutorial; GEroundtable Flow guide; Flow credits table (catchaiinfo).
