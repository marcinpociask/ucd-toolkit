---
name: ucd-personas
description: Personas block of the UCD toolkit. Builds or updates personas with goals, contexts, behaviours and the challenges they face, plus jobs-to-be-done and optional journey or empathy maps, from research synthesis or documents the user supplies. Works standalone or with ux/PROJECT.md. Use for "create personas", "update the personas", "journey map", "who are our users".
---

# UCD personas

## Start-up (every run)

1. Look for `ux/PROJECT.md` in the working directory. If it exists, read it, plus `ux/01-research/` and `ux/02-personas/`.
2. If it does not exist, run standalone: ask only the minimum context below (skip what the user already said) and invite documents or links. Offer once to save the answers as `ux/PROJECT.md`.
3. Missing upstream work is never a blocker. Proceed on stated assumptions and mark each `[assumption]`.

**Minimum context:** what the product is, what is known about users and from which sources, how many personas are useful (default 2–4), whether personas already exist that should be revised instead of replaced.

### Ask with a clickable form

Ask the questions below as a clickable form with the AskUserQuestion tool (up to 4 questions per form, 2–4 options each; the user can always pick "Other" and type). Skip any already answered by the brief or the conversation. If the tool is not available, use numbered options in text. Ask the rest of the minimum context in plain text.

| Question | Options | Multi-select |
|---|---|---|
| How many personas? | Let the data decide (Recommended) · 2 · 3 · 4 | no |
| What are they based on? | Research evidence · Mix of research and assumptions · Assumptions only (proto-personas) | no |
| Are there existing personas? | No, create new · Yes, revise them · Yes, add to the set | no |
| Any extras? | Journey map · Empathy map · No extras | yes |

## Method

1. **Decide the type.** With research evidence, build evidence-based personas. Without it, build **proto-personas**, title them as such, and list what would need validating.
2. **Segment by behaviour**, not demographics: goals, context of use, frequency, expertise, constraints. Each persona must differ in a way that changes design decisions; merge those that do not.
3. **Write each persona** to `ux/02-personas/<name>.md`:
   - Name and one-line summary; role and context of use
   - Goals (what success looks like for them)
   - Behaviours and current workarounds
   - **Challenges**: each with an ID (e.g. `ANNA-C1`), a description, the evidence or `[assumption]`, and severity for the persona
   - Jobs to be done: "When…, I want to…, so I can…"
   - Accessibility and environment considerations
   - A representative quote only if it is real; otherwise omit
4. **Index** in `ux/02-personas/README.md`: a comparison table, the primary persona and why, and a challenge list across all personas. Later blocks trace flows, screens and audit findings back to these challenge IDs, so keep IDs stable when revising.
5. **Optional**, when asked: journey map (stages, actions, thoughts, pain points, opportunities) or empathy map per persona.

## Personas that already exist outside the toolkit

Do not rewrite them. Read them where they are and write only the index, `ux/02-personas/README.md`: the comparison table, the primary persona, and the challenge list with IDs assigned in the order the challenges appear in the source, each pointing back to the source document. Mark which attributes rest on evidence and which were constructed (demographics, daily routines and quotes written for a concept project are assumptions). If `ucd-flows` already assigned IDs in `ux/03-flows/flows.md`, reuse those exactly.

## Rules

- No invented statistics, quotes or biographical colour presented as fact.
- Avoid stereotypes; include only attributes that affect design.

## Finish

Save outputs, update the Stage status row in `ux/PROJECT.md` if it exists, summarise the personas in a short table, and suggest the next block (usually `ucd-flows`).
