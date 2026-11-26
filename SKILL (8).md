---
name: "soundtrack"
description: "Write a code-synthesized score and sound effects (Web Audio) for a canvas animation, synced to its cuts, and check that hits land on the beat without startling jumps."
---

# Soundtrack

Adapted from iart-ai/javascript-animation-skills (MIT). The original also ships `templates/groove.js`, `templates/score.js` and `scripts/sync-check.mjs`; fetch them from https://github.com/iart-ai/javascript-animation-skills when a shell is available.

## Write the sound for this film

A film's sound is written for that film: its own instruments, rhythm and harmony in Web Audio, from nothing (oscillators, noise, filters, envelopes, delays). If the project provides a sound kit (for example `SOUND.kit` with `k.play`, `k.tone`, `k.noise`, `k.bed`, `k.music`), schedule everything through it and reuse the same event times as the picture. No two films should sound alike because they share a template.

The same score function renders offline (OfflineAudioContext) to a WAV for the MP4, and plays live in the page preview.

Don't ask the user to choose a music source up front. At delivery, mention in one line that AI-generated music or their own track also work.

## How the music follows the picture

- **Tempo map.** Each scene gets a whole number of bars so every cut lands on a downbeat.
- **Mark cuts with harmony, not volume.** Walk each scene home to the dominant; the cut arrives on the tonic. A +7 to +10 dB jump on a cut reads as a jump scare; +3 to +5 dB with a chord change reads as a clean edit.
- **Don't thin the opening bar** if it's the only bar before the first cut.
- **No extra accent on the cut's downbeat.** The chord change is enough.
- **Hard cuts inside a scene count.** Put them in the cue list too.
- **Give the eye something to lock onto.** Legato music with no percussion has no accents for cuts to land on.
- **Bring layers in one or two per bar.** Kick and bass together after a quiet intro is a startle; stagger them.
- **Use a break.** Silence for a bar before the payoff is the strongest beat in a short.

## Sound effects (explainers)

- Sync is everything: a sound starts on the exact frame its event appears.
- Score the events that land: pops, stamps, labels landing, arrows completing, scene transitions, the wrong/right moment, the key number (the biggest hit) and the takeaway (a resolving sound).
- Drawing makes its medium's noise while it draws (marker, chalk, pen strokes matched to the draw-on length; typing while text types).
- Counters tick at most ~12 times a second, slowing as they settle.
- Hierarchy: effects in front, bed or music clearly underneath (music gain 0.6 or less), no more than ~3 sounds at once, small silences so big hits read. Medium-true palette, not generic swooshes.

## Other sources (only when asked)

- AI-generated music or the user's own track: mux it with ffmpeg. With music you don't control, the picture follows the music: measure offsets and move scene boundaries, keeping each scene in local time so moving a boundary never touches scene code.

## Always: check it

For each cut and declared hit, measure the offset to the nearest strong audio onset and the loudness jump into it. Fail on OFF-BEAT (more than ±100 ms, ~3 frames) or STARTLE (more than +6 dB versus the second before). Skip the opening second and the final fade. Fix and re-run until it passes, or until every remaining STARTLE is a deliberate stinger you can name.

## Limits

Synthesized: music box, plucks, pads, bells, soft percussion are fine. Realistic voices, orchestras and genre production are not; use AI music or a real track for those.