---
name: "youtube-intro-outro"
description: "Make a branded channel intro / logo sting (3-5 s), bumper or outro / end screen whose layout leaves room for YouTube's end-screen elements, synced to an audio sting."
---

# Intro & Outro (vinhetas de canal)

Adapted from iart-ai/youtube-video-skills (MIT). The original also ships Remotion compositions, `references/intro-outro.md` and `scripts/contact-sheet.sh` / `probe-mp4.sh` (https://github.com/iart-ai/youtube-video-skills).

Build the two pieces that bracket every video: a 3-5 s branded **intro** (logo sting that says "this is my channel") and an **outro** whose last ~20 s host YouTube's clickable end-screen elements. Both should be one reusable template where only the brand changes.

## Two hard rules (platform, not taste)

1. **Intro 3-5 s, logo hit 1-2 s.** Longer than 5 s causes measurable drop-off. The intro confirms the channel and gets out of the way.
2. **Outro: at least 20 s of held, quiet layout, and the video at least 25 s long.** End-screen elements are only allowed in the final 5-20 s. Never put your own content under them.

## Intro: the logo sting

Three beats in about 3.5 s. The mark must land exactly on the sound's impact frame, not near it.

| Beat | Window | Job |
|---|---|---|
| Windup | 0-0.8 s | build / whoosh; logo not yet readable |
| Impact | ~0.8 s | logo snaps to full on the audio hit + a flash |
| Settle | 0.8-1.2 s | overshoot relaxes to rest; tagline fades in |
| Hold | 1.2-3.5 s | brand legible, then cut to content |

- Keep IMPACT as a constant (e.g. `IMPACT = 0.8`), computed to a frame, never detected at runtime.
- The snap: scale springs from about 1.18 (or a subtler 1.04) to 1.0 starting on IMPACT; a flash decays over ~6 frames. In a stylized medium, make the flash the medium's own (light bloom, copier flash, plate slam, ink pulse).
- Audio: align the sting so its loudest transient sits on the IMPACT frame. If the user supplies a sting, find its peak first and set IMPACT from it.

## Outro: leave room for the end-screen elements

Treat the frame as thirds. YouTube's clickable elements live on the **right two thirds**; your branding, channel name and any face-cam stay in the **left third**. Avoid corners and the bottom (progress bar and UI overlap there).

| Element | Native size (1920x1080) | Where to leave room |
|---|---|---|
| Subscribe / channel circle | 294x294 | right side, roughly centered vertically, off the edge |
| Next-video card | 615x345 | upper-right or center-right |
| Playlist / link card | 294x294 | beside the video card |
| Your branding | - | left third only, top-aligned |

- Draw dashed placeholder guides for those zones behind a flag (on in previews, off in the final render) so you compose around them; the user then places the real elements in YouTube Studio.
- After a short reveal (under ~1.5 s), the plate holds with only subtle motion, nothing that competes with the cards.
- Up to 4 elements; 1 video + subscribe is the highest-CTR layout.

## Reusable brand template

Everything brand-specific comes from one object: name, logo, sting, background, foreground, accent. Fonts, layout and timing stay fixed so many channels stay structurally consistent and only identity differs.

```js
{ "name": "PixelForge", "logo": "logo.png", "sting": "sting.mp3", "bg": "#0B0B14", "fg": "#FFFFFF", "accent": "#7C5CFF" }
```

## Verify before encoding

Render stills first: intro at windup, the IMPACT frame and settle; outro at the end of the reveal and the held plate.
- On the IMPACT frame the logo is full-scale and legible and the flash fires.
- Intro 5 s or less; outro held for 20 s or more.
- Outro branding only in the left third; right two thirds quiet; nothing within ~10% of an edge or in the bottom UI band.
- Motion is a pure function of time (no timers, Date.now or Math.random).
- Only then encode the MP4s with the sting muxed in, plus a PNG of the last frame.