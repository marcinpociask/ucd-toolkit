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

### Ask with a clickable form

Ask the questions below as a clickable form with the AskUserQuestion tool (up to 4 questions per form, 2–4 options each; the user can always pick "Other" and type). Skip any already answered by the brief or the conversation. If the tool is not available, use numbered options in text. Ask the rest of the minimum context in plain text.

| Question | Options | Multi-select |
|---|---|---|
| What do you need? | Plan research · Synthesise existing material · Desk research | no |
| Plan: which methods are feasible? | User interviews · Survey · Usability test · Competitive review | yes |
| Plan: which instruments should I produce? | Interview guide · Survey · Screener · Usability test script | yes |
| Synthesise: what kind of material is it? | Interview notes or transcripts · Survey results · Reviews or support tickets · Analytics | yes |

Ask only the rows that match the chosen mode.

## Pick the mode

Use the form answer, or the request itself when it already makes the mode obvious.

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
