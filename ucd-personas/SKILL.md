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

## Rules

- No invented statistics, quotes or biographical colour presented as fact.
- Avoid stereotypes; include only attributes that affect design.

## Finish

Save outputs, update the Stage status row in `ux/PROJECT.md` if it exists, summarise the personas in a short table, and suggest the next block (usually `ucd-flows`).
