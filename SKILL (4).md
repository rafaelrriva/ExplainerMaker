---
name: "kinetic-typography"
description: "Animate headlines, titles, taglines and title cards: split by line, word or character, mask, blur or clip reveals, stagger timing, variable-font and text-on-path effects."
---

# Typography in Motion

Adapted from iart-ai/kinetic-typography-skills (MIT). The original also ships `references/reveal-recipes.md` and `scripts/seek-shot.sh` (https://github.com/iart-ai/kinetic-typography-skills).

## 1. Get static typography right first

Motion cannot rescue bad type. Lock line-height (1.1-1.2 for display headlines, 1.4-1.6 for body), tracking (tighten display by -1% to -3%), alignment and weight. Then split and animate.

## 2. Choose split granularity

- **By line:** calmest, most premium; elegant headlines.
- **By word:** energetic; taglines and lyric hits.
- **By character:** most kinetic; short strings only.

On the web, splitting into spans destroys the text for screen readers: put `aria-label` with the full string on the container and `aria-hidden="true"` on the fragments. Split after `document.fonts.ready` so line breaks are correct.

## 3. Reveal techniques

- **Mask / clip reveal (most robust):** each line in an overflow-hidden box; the child goes from translateY(100%) to 0. On canvas: clip to the line box and move the glyphs up from below the baseline.
- **Blur-in:** blur(12px) to 0 with opacity 0 to 1. Soft focus-pull; keep the radius modest and durations short.
- **Clip-path wipe:** inset(0 100% 0 0) to inset(0) for a directional reveal without moving the glyphs.
- **Character stagger:** fade/translate each character with a 20-40 ms offset.

## 4. Timing

- Enter with ease-out: cubic-bezier(0.16, 1, 0.3, 1) (easeOutExpo) feels premium.
- Per-fragment duration 400-600 ms.
- Stagger: lines 60-100 ms, words 40-70 ms, characters 20-40 ms.
- Cap the total reveal near ~800 ms; for long strings, reduce the per-character offset or switch to word/line.

## 5. Other effects

| Effect | Approach |
|---|---|
| Variable weight | animate font-variation-settings "wght" a to b (check the font really is variable and its axis range) |
| Text on path | SVG textPath; animate startOffset 0% to 100% |
| Stroke draw-on | text as path, animate stroke-dashoffset |

## Verify

Freeze the reveal at start, middle and end, screenshot each and check: no clipped glyphs or descenders, masks fully hide the baseline, no flash of unstyled text or wrong line breaks before fonts load, no blur fringing, accents and every glyph render. On the web, honor prefers-reduced-motion (text shown in its final state).