---
name: animated-storefront
description: Build an animated e-commerce storefront hero — garments hanging from a horizontal rail that glide along it while the pastel background slowly shifts colour. Use when building or improving a small shop site with a product-rail hero.
---

# Animated Storefront (Product-Rail Hero)

The reference look: a clothing site where garments hang from a horizontal
rail and glide along it while the pastel background slowly shifts colour
(the wearebrand Reel that popularised it). This skill is how to build that
hero for a real small shop — no brand logos, no trademarked material, the
shop's own products only.

## Reference look (what to reproduce)

- Header: logo left, small menu (Home, New Drop, ...), search / account /
  cart icons right.
- "NEW COLLECTION" heading above the rail.
- One horizontal rail across the screen; garments hang from it, each with
  a small white price tag at the top. Garments glide sideways, sliding in
  and out at the edges, forever.
- Background shifts slowly between pale yellow-green, pale lilac, and
  white.
- Tagline lower-right (e.g. "Crafted in heavyweight fleece. Cut
  oversized. Made to last.").
- NEVER use another brand's logo, name, or trademarked material. The
  reference demo was Nike-branded; your versions use the shop's own brand
  and products only.

## Core technique: the seamless gliding rail

The rail is an infinite marquee. The one rule: the animation's end state
must match its start state exactly, or the eye catches the jump at the
loop point.

- Duplicate the product set so the track holds identical copies side by
  side.
- Animate the track by exactly ONE copy's width, then reset — the reset is
  invisible because the next copy is in exactly the first copy's place.
- Easing must be linear (`linear` / GSAP `ease: "none"`). Any easing curve
  pulses visibly at every repeat boundary. `yoyo` is a ping-pong, not a
  loop.
- Put spacing on the ITEMS (`margin-right`), never a flex `gap` on the
  track: a gap between the last item of one copy and the first of the next
  breaks the exact-width math. With per-item margins, every copy is
  exactly identical.
- One copy must be at least as wide as the viewport, or a gap appears
  mid-loop. With 2 copies, one copy must cover the whole viewport; with 3
  copies (translate by -1/3), one copy only needs to cover half the
  viewport. Use 3 copies for this reason. On very wide (4K) screens add a
  4th copy or widen items.
- Pause on hover (`animation-play-state: paused`) and respect
  `prefers-reduced-motion` (turn the animation off).
- Fade the rail edges with a mask so garments dissolve instead of being
  cut off hard: `mask-image: linear-gradient(to right, transparent, black
  5%, black 95%, transparent)`.
- Animate `transform` only (`translate3d`), never `left`/`margin` —
  transforms are GPU-composited and stay at 60fps. Add `will-change:
  transform` to the track.
- If measuring widths in JS (GSAP), wait for images to load first
  (`window load` event or an imagesLoaded-style check) or widths are wrong.

### Pattern A — pure CSS (recommended for a small shop; zero dependencies)

```html
<div class="rail-viewport"> <!-- overflow: hidden + edge mask -->
  <div class="rail-track">  <!-- display:flex; width:max-content -->
    <!-- the product set, repeated 3x; duplicates aria-hidden="true" -->
    <div class="garment">…</div>
    …
  </div>
</div>
```

```css
.rail-track {
  display: flex;
  width: max-content;
  will-change: transform;
  animation: railGlide 40s linear infinite;
}
.rail-viewport:hover .rail-track { animation-play-state: paused; }
@keyframes railGlide {
  from { transform: translate3d(0, 0, 0); }
  to   { transform: translate3d(calc(-100% / 3), 0, 0); } /* 3 copies */
}
.garment { margin-right: 28px; } /* spacing on items, NOT track gap */
```

### Pattern B — GSAP (when you need drag, velocity control, or per-item motion)

```js
// Track holds the content twice; tween by exactly one copy's width.
gsap.to(".track", {
  xPercent: -50,
  duration: 20,
  ease: "none",
  repeat: -1,
});
```

- For drag control or items that wrap individually, use the `modifiers` +
  `gsap.utils.wrap` approach — this is the engine inside GSAP's
  `horizontalLoop` helper (a `repeat: -1` timeline of per-item tweens with
  `modifiers: { time: gsap.utils.wrap(0, duration) }`).
- For many items animated per-frame (e.g. cards on a sine wave), use
  `gsap.quickSetter` inside one `gsap.ticker` callback instead of many
  tweens — one callback writing transforms directly keeps performance flat.
- CDN: `https://cdn.jsdelivr.net/npm/gsap@3.12.5/dist/gsap.min.js` (+
  `ScrollTrigger.min.js` for scroll effects). GSAP is free for most use;
  check the current licence before commercial use.

## Background colour transitions

### CSS-only (timed cycle, no scroll needed)

```css
.hero { animation: bgCycle 18s ease-in-out infinite alternate; }
@keyframes bgCycle {
  0%   { background-color: #f2f4dc; } /* pale yellow-green */
  50%  { background-color: #ece7f5; } /* pale lilac */
  100% { background-color: #faf9f6; } /* warm white */
}
```

`alternate` makes the cycle run back smoothly instead of snapping. Keep
colours pale so dark text stays readable throughout.

### GSAP + ScrollTrigger (colour follows scroll position — for a longer page)

Put the palette in the markup as data attributes; one loop wires every
section. Toggle at the viewport centre so the new palette takes over
exactly when the new section dominates the screen; `overwrite: "auto"`
prevents flicker on fast scrolls.

```js
gsap.registerPlugin(ScrollTrigger);
gsap.utils.toArray(".color-section").forEach((section) => {
  ScrollTrigger.create({
    trigger: section,
    start: "top center",
    end: "bottom center",
    onToggle: (self) => {
      if (self.isActive) {
        gsap.to("body", {
          backgroundColor: section.dataset.bg,
          color: section.dataset.fg,
          duration: 0.6,
          overwrite: "auto",
        });
      }
    },
  });
});
```

```html
<section class="color-section" data-bg="#f2f4dc" data-fg="#1c1c1a">…</section>
```

For a scrubbed (scroll-position-driven) blend instead of a toggle, tween a
CSS variable with `scrub: true` and `immediateRender: false`.

## Header layout pattern

```css
header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 18px 32px;
}
```

Logo (mark + wordmark) left, `<nav>` centre, icon buttons right (inline
SVG, `currentColor`, 22px). On mobile (<720px) hide the nav links and keep
logo + icons; add a hamburger only if the real site needs one. Keep the
header transparent over the hero so the shifting background shows through.

## Which platform for a small shop

| Option | When to pick it | Notes |
|---|---|---|
| **Shopify theme** (custom section) | The shop needs real checkout, inventory, and payments, and the owner is OK with a monthly fee | The rail becomes a custom theme section (Liquid + the CSS/JS above). Products come from the Shopify catalog, so prices/photos update themselves. Paid apps exist for infinite scroll, but the hero rail is hand-coded, not an app. |
| **Custom static site** (plain HTML/CSS/JS) | Showcase / catalog site, orders taken on WhatsApp or in person, no online payment yet | Cheapest to host (free on GitHub Pages / Netlify / Cloudflare Pages), fastest on slow mobile data, full control of the animation. No CMS — product changes mean editing the file. Best first step for a small shop. |
| **WordPress + WooCommerce** | Owner wants to edit products himself in a dashboard and take online orders | Heaviest option; the rail goes in as a custom block/template or a code snippet. More maintenance (updates, security) — see the `web-security-defense` skill before touching a live WordPress site. |

Recommendation: start with the custom static site; move to Shopify only
when online checkout is actually needed. Do not promise a platform until
the owner answers the questions below.

## Ask the site owner BEFORE building the real site

- Which platform is the site on (or should it be)? Shopify, WordPress, or
  a fresh static site? Who hosts it, and do we have access?
- Product photos: real photos of the actual products? (AI stand-ins are
  for a demo only — a real shop must show real stock.) Same background and
  same orientation for every product, or the rail looks uneven.
- Brand: shop name, logo file, brand colours, and the exact tagline
  wording.
- Products: how many in the rail, names, and prices? Which are the
  featured ones?
- What happens on click — product page, WhatsApp order, or add-to-cart?
  Is there online payment (bKash/Nagad/cards) or cash on delivery /
  in-shop only?
- Language: Bengali, English, or both?
- Domain: does he own one already?

## Free voice/video calls on the site (later feature — brief notes)

Feasible with WebRTC, a free open standard built into browsers:

- 1-to-1 calls are peer-to-peer in the browser — no per-minute charge. A
  tiny signalling server is still needed (to set calls up); a small VPS
  or a serverless function is enough.
- STUN (finding the caller's public address) is free — Google's public
  STUN servers (`stun:stun.l.google.com:19302`) are free to use.
- TURN (relaying media when a direct connection fails behind strict NAT /
  firewalls) is the real cost: either self-host coturn on a VPS
  (bandwidth cost only, roughly a $5–10/month VPS for light use) or pay a
  hosted TURN provider by bandwidth.
- Fastest routes: embed **Jitsi Meet** (open source; self-host free, or
  use meet.jit.si free) or use **Agora's free tier** (~10,000
  minutes/month free) / Daily.co free tier for a managed SDK. Group calls
  need an SFU server (Jitsi / LiveKit self-hosted) — heavier than 1-to-1.
- Do not build this until the storefront itself is decided: it needs
  HTTPS, a backend for signalling, and a decision on who the calls are
  for (customer support 1-to-1 is the sensible first use).

## Sources (researched 2026-11-21)

- GSAP seamless loop technique: https://annnimate.com/learn/timeline/seamless-loop
- Infinite marquee setup (duplicate content + overflow hidden):
  https://university.webflow.com/videos/infinite-marquee-animation-on-scroll
- Pure-CSS infinite scrolling list: https://www.louzers.com/posts/css-infinite-scrolling-marquee
- CSS scroll shelf (snap rail + faded edges): https://purecss.com/examples/scroll-shelf/
- ScrollTrigger background-colour sections:
  https://webdevpuneet.com/ui-snippets/scroll-color-sections/ and
  https://lab.good-fella.com/blog/gsap-scrolltrigger-examples
- GSAP sine-wave marquee cards (quickSetter performance pattern):
  https://www.madeforaward.com/collections/component-0028/gsap-infinite-marquee-cards-sine-wave-image-animation/code
