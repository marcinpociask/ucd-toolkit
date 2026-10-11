---
name: ucd-research
description: UX research block of the UCD toolkit. Plans research (goals, methods, interview guides, surveys, screeners) and synthesises raw material (interview notes, transcripts, survey exports, reviews, analytics) into themes, insights and opportunity areas. Works standalone or with ux/PROJECT.md. Use for "plan user research", "write an interview guide", "synthesise these interviews", "competitive analysis".
---

# UCD research

## Start-up (every run)

1. Look for `ux/PROJECT.md` in the working directory. If it exists, read it, plus anything in `ux/inputs/` and `ux/01-research/`.
2. If it does not exist, run standalone: ask only the minimum context below (skip what the user already said) and invite documents or links. Offer once to save the answers as `ux/PROJECT.md`.
3. Missing context is never a blocker. Proceed on stated assumptions and mark each `[assumption]` in the output.

**Minimum context:** what the product is, who the users are, what decision this research should inform, what material already exists.

## Pick the mode

Ask which one applies if it is not obvious from the request.

### Plan
- Turn the decision to be informed into 3–6 research questions.
- Recommend methods matched to the questions, timeline and access to users; say why, and what each method cannot tell you.
- Produce the instruments asked for: interview guide (warm-up, open non-leading questions, probes, wrap-up), survey, screener, usability test script, or competitive review grid.
- Output: `ux/01-research/plan.md` and one file per instrument.

### Synthesise
- Read every source provided. Keep a source ID for each (P1, P2, survey, reviews…).
- Extract observations as atomic notes, each tagged with its source ID and, where possible, a short verbatim quote.
- Cluster into themes (affinity mapping). For each theme: what was observed, how many sources support it, the strongest quote, the implication for design.
- Separate **finding** (seen in the data) from **interpretation** (your reading of it). Flag themes resting on a single source.
- End with needs, pain points, opportunity areas phrased as "How might we…", and gaps the data does not cover.
- Output: `ux/01-research/synthesis.md`.

### Desk research
- Competitive or analogous-product review, domain background, heuristics from published sources. Cite every source. Output: `ux/01-research/desk-research.md`.

## Rules

- Never invent participants, quotes or numbers. If there is no real data, say so and label the output as hypotheses to validate.
- Report sample sizes plainly; do not turn 3 of 5 interviews into a percentage.

## Finish

Save outputs, update the Stage status row in `ux/PROJECT.md` if it exists, give a five-line summary, and suggest the next block (usually `ucd-personas`).
