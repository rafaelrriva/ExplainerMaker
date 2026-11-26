---
name: "logo-animation"
description: "Animate a logo or brand mark (intro stinger, brand reveal, app splash, loader loop) with one clear technique, intact geometry and a clean final frame synced to a sound logo."
---

# Logo Animation

Adapted from iart-ai/motion-design-skills (MIT). The original also ships `references/logo-patterns.md` and `scripts/seek-shot.sh` (https://github.com/iart-ai/motion-design-skills).

Bring a brand mark to life with one clear idea, on-brand geometry and a crisp settle, for web (SVG/Lottie), video intros/outros or app splash, and always ship a static end-frame fallback.

## Core principle

Pick ONE technique per logo: draw OR build OR morph, not all at once. Reveals run 0.8-2.5 s. Never distort brand geometry: scale and fade are safe, skew and squash usually are not. Respect clearspace (keep the mark's minimum margin clear of motion debris). On the web, provide a `prefers-reduced-motion` path that shows the final mark with no motion.

## Technique map

| Technique | Best for | Mechanism |
|---|---|---|
| Stroke draw-on | Line marks, monograms, signatures | stroke-dashoffset 1 to 0 (pathLength=1) or a partial path on canvas |
| Mask wipe / reveal | Filled shapes, gradients | animate a clip / mask |
| Build-on (stagger) | Multi-piece marks, grids | per-group opacity + transform, staggered |
| Morph | Icon to wordmark, shape to logo | matched path interpolation |
| Idle loop | Loaders, ambient splash | seamless cyclic transform |
| Wordmark | Logotypes | per-letter mask/translate stagger |

Build-on order: base/container first, then accents, wordmark last so the eye lands on the name. Back-ease entrances (`back.out(1.6)`), ~0.5 s per piece, ~80 ms stagger.

SVG draw-on quick start:

```html
<path class="ink" d="..." fill="none" pathLength="1" stroke-dasharray="1" stroke-dashoffset="1"/>
<style>@keyframes draw{to{stroke-dashoffset:0}} .ink{animation:draw 1.1s cubic-bezier(.65,0,.35,1) forwards}</style>
```

## Using the real logo

If the user supplies the logo file, it is the source of truth: convert SVG paths to Path2D (canvas) or inline SVG, or draw the PNG itself. Never redraw the mark from memory. If only a description is given, draw it faithfully and list what you assumed.

## Sound-logo sync

When audio exists, the final settle frame lands exactly on the sonic accent. Decide the audio first, find the peak timecode, then time the reveal so the mark snaps to full on that frame. A tiny overshoot-and-settle (scale 1.04 to 1.00 over ~0.15 s) on the beat adds impact. A settle that floats free of the sound feels cheap.

## Delivery targets

- Web hero: inline SVG + CSS or one GSAP timeline.
- App, designer-made: Lottie with a poster fallback frame.
- Video intro/outro: a seekable canvas page or Remotion/After Effects render, pre-rendered at 2x for crispness.

## Verify

Freeze the animation at start, middle and end (a `?t=N` harness or `window.seek(t)`), screenshot each and check:
- One technique; geometry undistorted; clearspace clear.
- No half-drawn strokes at the end frame; the final frame is the true logo.
- Reveal 2.5 s or less; if audio is present, the settle lands on the sound-logo peak.
- Static end-frame fallback shipped (PNG/SVG).
Fix and re-screenshot the same moments until every frame is clean.