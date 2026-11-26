---
name: "explainer-video"
description: "Plan and structure a 15-90 s animated explainer: one core idea, problem-stakes-solution-how-payoff arc, one analogy, timed script, storyboard and captions."
---

# Explainer Video

Adapted from iart-ai/explainer-video-skills (MIT). Turn one message into a paced short: script → storyboard → scene build → narration/caption sync → edit → polish, with one consistent style system.

## Story structure (decide this first)

An explainer is an argument, not a feature tour.

- **One core idea.** A single sentence the viewer can repeat afterward. If you can't state it in one line, cut scope until you can.
- **Script-first.** Write and time the words before you storyboard or animate; cutting a sentence is cheaper than cutting a built scene.
- **Earn the "how" with stakes.** Make the viewer feel the cost of the problem before showing the mechanism.

| Stage | Narrative job | What the viewer should think |
|---|---|---|
| Problem | Name the pain in their words | "That's me." |
| Stakes | Show what the pain costs | "I need this fixed." |
| Solution | The fix, in one line | "Oh — that solves it." |
| How it works | The mechanism in 1–3 concrete steps | "I get how it does that." |
| Payoff / CTA | The after-state + one next action | "I want that." |

For a pure concept explainer (no product), use: hook question → the parts → the mechanism step by step → the key number or result → takeaway.

### Pick one analogy and ride it

Choose a single metaphor from the viewer's world and keep it across scenes; switching analogies resets comprehension. If the analogy needs its own explanation, it's the wrong one.

### Pacing per beat

| Beat | Feel | Cut rhythm |
|---|---|---|
| Problem / Stakes | Brisk, a little tense | Faster cuts, short holds |
| Solution | A beat of relief | One clear hold |
| How it works | Deliberate, one step at a time | Slowest — hold each step to read |
| Payoff / CTA | Confident, open | Hold the end card; one CTA |

## Script formula

| Beat | Share of runtime |
|---|---|
| Problem | ~20% |
| Solution | ~15% |
| How | ~45% |
| Payoff | ~20% |

Write VO in spoken language (contractions, short sentences). Read it aloud and time it before building.

## VO timing math

- ~2.3 words/sec (140 wpm); slow technical lines to ~2.0.
- Scene length ≈ words / 2.3 + ~0.4 s breathing room.
- A beat with no VO still needs ≥1.0 s to register.

## Scene building

- Diagrams reveal progressively: nodes → edges → labels, with staggered entrances and connectors that draw on.
- Keywords pop in on the stressed word.
- Stats count up with an ease-out so they settle.
- Visuals illustrate the line being spoken; show, don't decorate.

## Captions

Assume muted autoplay. Keep ≤2 lines, ≤42 chars/line, on screen ≥1.0 s, gone before the next line. Drive captions from the same timing array as the scene cuts so they never drift.

## Style-system consistency

Lock one type scale, one color grammar (color = meaning, never reassigned) and one easing curve before building scene 2. Reuse the same enter/exit transitions so the piece feels like one object, not a montage.

## Output checklist

- Single clear message; every scene advances it.
- VO timed; scene lengths derived from VO.
- Storyboard maps each line to a visual.
- Captions available and readable.
- Consistent type, color and motion across scenes.
- End card with one clear takeaway or CTA.
- Before finishing, render stills at the start, inside each scene's hold and at the last frame; check the caption and the visual match at each, nothing clipped or off-canvas, then encode.