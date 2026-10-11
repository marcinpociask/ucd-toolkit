---
name: ucd-audit
description: Post-design audit block of the UCD toolkit. Runs a heuristic evaluation (Nielsen's 10), accessibility checks and design-system consistency review on a Figma component, flow or full screen, or on screenshots or a live URL, and produces severity-rated findings with fixes. Works standalone on any design, with or without ux/PROJECT.md. Use for "audit this screen", "heuristic evaluation", "review this flow", "check this component", "UX review".
---

# UCD audit

Expert-review pass on finished or in-progress design. It complements usability testing with real users; it does not replace it. Say so in every report.

## Start-up (every run)

1. Look for `ux/PROJECT.md` in the working directory. If it exists, read it, plus `ux/02-personas/README.md` and `ux/03-flows/` so findings can be traced to persona challenges and intended flows. If personas live outside the toolkit, use the challenge ID table at the top of `ux/03-flows/flows.md` when there is one.
2. If it does not exist, run standalone: ask only the minimum context below (skip what the user already said). Offer once to save the answers as `ux/PROJECT.md`.
3. Missing context is never a blocker. Audit against general heuristics and mark context-dependent judgements `[assumption]`.

**Minimum context:** what to audit (Figma link, current Figma selection, screenshots, or URL), the scope type (component / flow / screen), platform, who the user is and what task they are doing, accessibility target (default WCAG 2.2 AA).

### Ask with a clickable form

Ask the questions below as a clickable form with the AskUserQuestion tool (up to 4 questions per form, 2–4 options each; the user can always pick "Other" and type). Skip any already answered by the brief, the request (e.g. a pasted Figma link) or the conversation. If the tool is not available, use numbered options in text. Ask the rest of the minimum context (the user and their task) in plain text.

| Question | Options | Multi-select |
|---|---|---|
| What is the scope? | Screen · Flow · Component | no |
| What will you give me? | Figma link · Current Figma selection · Screenshots · Live URL | no |
| Which platform? | Mobile · Web · Desktop · Other device | no |
| Accessibility target? | WCAG 2.2 AA (Recommended) · WCAG 2.2 AAA · No target defined (audit against AA) | no |

After the report, ask a second form: publish the report as a shareable page (Yes · No), and write findings back to Figma (No · As comments · As annotations).

### Figma check

When the source is a Figma link or the current selection, check the connection first: if no Figma tools are available or the status check fails, ask:

| Question | Options |
|---|---|
| Figma is not connected. How do you want to continue? | Set up the connection now (Recommended) · Audit from screenshots or exports instead · I will connect it myself, then tell you |

On "Set up the connection now", run the `ucd-figma-connect` skill, then come back here. A read-only connection is enough for an audit. Name the connected file in the report's scope section; if it differs from the file recorded in `ux/PROJECT.md` (a copy, a backup), say so.

## 1. Gather evidence

Use whichever Figma connector tools are available:

- Screenshot of each frame or component in scope; look at it before judging.
- Structure and properties: layer metadata, design context, component properties and variants.
- Variables and styles in use, to detect hard-coded values and off-system components.
- For flows: prototype connections or the user's stated order of frames. If the order is unclear, ask.
- Built-in lint or accessibility audit tools, if the connector has them; treat their output as input to your own judgement.

Without Figma access, work from screenshots or the live page and state what could not be inspected (e.g. exact colour values, component structure).

## 2. Evaluate

Read `heuristics.md` in this skill's folder and apply the checklist for the scope type:

- **Component**: states and variants complete, naming and properties, token usage, contrast, target size, content resilience (long text, localisation), consistency with sibling components.
- **Screen**: all ten heuristics, visual hierarchy, primary action clarity, states, accessibility, consistency with the design system.
- **Flow**: everything for screens, plus step count, entry and exit points, error recovery, progress and system status across steps, dead ends, consistency of patterns between steps.

When personas exist, walk the task as the primary persona and note where each of their challenge IDs is addressed, ignored or made worse.

Measure where you can (contrast ratios from actual colour values, target sizes from frame dimensions) instead of estimating. If a value is estimated from a screenshot, say so.

## 3. Report

One finding per issue, each with:

| Field | Content |
|---|---|
| ID | A-01, A-02… |
| Location | Frame / layer name, with node link if available |
| Heuristic | Which one(s) violated, or WCAG criterion |
| Issue | What is wrong, in one or two sentences |
| Evidence | What you observed or measured |
| Severity | 0–4 (scale in `heuristics.md`) |
| Persona impact | Challenge ID(s), if personas exist |
| Fix | Concrete, specific recommendation |

Structure of the report:

1. Scope and method (what was inspected, what was not, and the reminder about usability testing)
2. Summary: counts by severity, top three issues to fix first
3. What works well (brief, specific)
4. Findings table, sorted by severity
5. Quick wins vs. structural changes
6. Open questions for the designer

Save to `ux/06-audit/<YYYY-MM-DD>-<scope>.md`. Offer to publish the report as a shareable page.

## 4. Optional: write back to Figma

Only after the user agrees, and stating exactly what will be added: pin each finding as a comment or annotation on its frame, prefixed with the finding ID and severity. Never change the design itself during an audit; offer fixes as a follow-up.

## Re-audit

If an earlier report exists for the same scope, compare: which findings are resolved, which remain, what is new.

## Finish

Update the Stage status row in `ux/PROJECT.md` if it exists and give the summary section in chat.
