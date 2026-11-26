---
name: "javascript-animation"
description: "Make short animated films or explainers where every frame is drawn in JavaScript on a canvas (seekable, deterministic), then render to MP4 and self-check the frames."
---

# JavaScript Animation (every frame drawn in code)

Adapted from iart-ai/javascript-animation-skills (MIT). The original pack also ships `templates/starter.html` and `scripts/render.mjs`, `asset-audit.mjs`, `layout-check.mjs`; fetch them from https://github.com/iart-ai/javascript-animation-skills when a shell is available.

One HTML file holds the whole piece; a headless browser seeks it frame by frame into an MP4.

## Default flow: don't stop to ask

Run straight through. Ask before starting only if there is no subject at all.

1. **Read the brief.** Infer the form (story, explainer, poem, loop), length (default 15-20 s) and aspect (default 1920x1080 or the size the brief names). On-screen text is in the language the user wrote the brief in.
2. **Plan the look and sound from the subject and audience.** Never reuse the look or sound of a previous piece by default. If the user points at a reference style, borrow its techniques, never its characters, story or compositions. When the user supplies a reference style source (an `explainer(ctx, W, H, t)` + `scoreSound(k)` template), that style wins: reuse its textures, finishing passes, palette and transitions.
3. **Beat grid, storyboard and blocking, as data** (see Storyboard below). These go into the page as `BPM`, `SECTIONS`, `SHOTS`, `EVENTS`: scenes, camera and soundtrack all read them, so picture and sound line up by construction.
4. **Build.** Keep the contract: `draw(frame)` / `explainer(ctx, W, H, t)` is a pure function of time. Use seeded rng, never `Math.random` or `Date`.
5. **Self-check, then render** (see QC). Fix and re-check until clean.
6. **Deliver** the MP4 and the HTML, then offer in one or two lines what can change.

## Rules that prevent the common failures

- **Pure function of time.** No requestAnimationFrame state, no CSS animations, no accumulated physics.
- **A hand-drawn line boils, it doesn't jitter.** Change the wobble seed every 4 frames (~7.5 changes/s), not every frame.
- **Rounded forms for bodies.** Few-point polygons read as signs.
- **Pick the angle that makes the pose read.**
- **Draw back to front, explicitly.**
- **Hit points on cuts and actions.** Every cut and visible action is in `EVENTS`; the soundtrack lands on them.
- **Text never collides.** Claim every text box and key object; place labels only where free.

## Storyboard, blocking and the beat grid

Write these before any drawing code, as data in the page.

### 1. Beat grid
- Pick a tempo from the mood. Every cut and visible action sits on a beat or half beat.
- Section shapes: escalation (intro, build, peak, break, payoff), steady, steps (explainers: a motif per step, a pause, a resolve), verse/return.
- A short silence before a payoff is a strong beat.

### 2. Shot list
One row per shot: from-to (beats), framing, camera move, action, blocking, the beat the action lands on, sound, transition.

| Form | Typical shot length |
|---|---|
| Comedy, hype | 1-3 s |
| Story | 2-5 s |
| Explainer | 3-6 s (one idea per shot) |
| Lullaby, ambient, poem | 5-10 s |

- Vary framing (wide, medium, close, extreme close).
- Keep every shot alive: a slow push or drift, or a secondary motion.
- Vary transitions: hard cut, match cut, push into / pull out of an object. Save the dip-to-paper for chapter breaks.

### 3. Blocking: one world, many cameras
- Put every character and prop in one continuous world with a track over global time. Shots are cameras looking at it.
- Carry something over every cut; keep screen direction; props, light and time of day persist.
- Things rest on surfaces; nothing hovers unless that's the point.

### 4. Story logic
- Every beat is caused by the previous one ("A causes B", not "A, then B").
- Show the metaphor in the picture, not only in a label.
- Punchlines get their own shot.

### 5. Events
`EVENTS = [[seconds, 'soundName', arg], ...]` lists every visible action with a sound. The scenes trigger the action at the same time; the score plays its sound.

## QC: self-check before delivering

Render a contact sheet (one frame per second, stepping off cuts) and a still at the action beat of every shot.

Frames
- No blank or near-blank frames except intended dips at cuts.
- Every scene reads in one second as a thumbnail.
- Text fits its box, never overlaps a face, key object or other text; every glyph renders (check accents and non-Latin text).
- Labels that type on: the box grows with the text.

Shapes and staging
- Each shape reads as the thing it is; silhouettes read; nothing floats; draw order is right; recurring characters stay consistent.

Storyboard conformance
- A still at each shot's action beat matches its row, with the cause of the action visible.

Director pass (contact sheet at 2 fps)
- Pace fits the form; framing varies; at least one push-in or pull-out; no dead frames; every visible action has its sound; the look fits the audience; it doesn't look or sound like your previous piece.

Motion
- Hand-drawn lines boil at ~7.5 changes/s. Endings hold after motion settles. Loops: first and last frame match.

Facts
- Every fact on screen has a source you can name; list assumptions.

Render stills of the frames you change instead of re-rendering the whole film each time. Do at least two rounds.