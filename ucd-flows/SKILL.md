---
name: ucd-flows
description: Flows and information architecture block of the UCD toolkit. Produces task analysis, user flows (happy path, alternatives, errors), sitemap or navigation model and a screen inventory, traced to persona goals and challenges, as Markdown and optionally as diagrams in a Figma or FigJam file. Works standalone or with ux/PROJECT.md. Use for "map the user flow", "information architecture", "sitemap", "what screens do we need".
---

# UCD flows and IA

## Start-up (every run)

1. Look for `ux/PROJECT.md` in the working directory. If it exists, read it, plus `ux/02-personas/` and `ux/03-flows/`.
2. If it does not exist, run standalone: ask only the minimum context below (skip what the user already said) and invite documents, links or Figma URLs. Offer once to save the answers as `ux/PROJECT.md`.
3. **Look for flows that already exist**, in the documents and, when a Figma connector is available, in the design file (page and section names such as "flows", "journeys", "storyboard"). Screenshot what you find. Build on it, do not duplicate it, and say what yours adds.
4. Missing upstream work is never a blocker. Proceed on stated assumptions and mark each `[assumption]`.

**Minimum context:** the product and platform, who the user is for this flow, the task or goal to map, existing screens or navigation that must be respected.

### Journey or task flow?

Teams use "user flow" for two different things. Name which one exists and which one you are producing:

| | Journey storyboard | Task flow |
|---|---|---|
| Answers | What does the ideal experience look like, and why? | What can happen during this task? |
| Shape | A line of steps, often with screen thumbnails, pains and design responses | A branching diagram with decisions |
| Paths | Happy path | Happy path, alternatives, errors, exits, every entry point |
| Used for | Presenting and aligning | Finding the screens and states that have to be designed |

This block produces task flows. If only journeys exist, the task flows extend them; keep both.

### Ask with a clickable form

Ask the questions below as a clickable form with the AskUserQuestion tool (up to 4 questions per form, 2–4 options each; the user can always pick "Other" and type). Skip any already answered by the brief or the conversation. If the tool is not available, use numbered options in text. Ask the rest of the minimum context in plain text.

| Question | Options | Multi-select |
|---|---|---|
| Which outputs do you need? | User flows · Sitemap or navigation model · Screen inventory · Task analysis | yes |
| What is the starting point? | Personas and goals · Existing screens or navigation to respect · A description only | no |
| Where should diagrams go? | Markdown file (Mermaid) · Markdown + a page in the Figma design file · Markdown + FigJam board | no |
| Which platform? | Mobile · Web · Desktop · Other device | no |

The Markdown file is always written; Figma or FigJam is an addition, never a replacement.

### If the diagrams go to Figma

Check the connection before promising anything: if no Figma tools are available or the status check fails, ask:

| Question | Options |
|---|---|
| Figma is not connected. How do you want to continue? | Set up the connection now (Recommended) · Continue with Markdown only · I will connect it myself, then tell you |

On "Set up the connection now", run the `ucd-figma-connect` skill, then come back here.

## Method

1. **Scope.** List the key tasks. If personas exist, derive tasks from their goals and jobs to be done. Look beyond the journeys already documented: interruptions the system starts (calls, alerts), diagnostic tasks ("why did this happen?"), recovery tasks and anything a navigation item promises but no journey covers. Offer the list as a multi-select form and confirm the priority order before detailing more than three flows.
2. **Challenge IDs.** Flows refer to persona challenge IDs. If personas exist without IDs (for example, written before the toolkit), assign IDs in a table at the top of `flows.md`, in the order the challenges appear in the source, and say that you did. Do not rewrite the personas.
3. **Task analysis** per task: trigger, preconditions, steps, decisions, success criteria, what can go wrong.
4. **User flow** per task as a Mermaid flowchart plus a short step table. Always include entry points, the happy path, alternative paths, error and empty states, and exits. Start the file with an overview table: flow, persona, frequency, challenge IDs addressed, source.
5. **Mark what is not established.** Tag every step the sources do not state as `[assumption]`, and every screen the flow needs that has no design as `not designed`. A flow that runs through screens that do not exist is a finding; list it.
6. **IA.** Sitemap or navigation model (Mermaid or indented list): top-level sections, hierarchy, cross-links. State the organising principle and one alternative you rejected. Show undesigned destinations as dashed.
7. **Screen inventory** table: screen, purpose, key content and actions, states (default, loading, empty, error, success), flows it belongs to, design status. Split it into screens in scope and screens the flows require but nobody has designed. End with a coverage summary: which states and viewports are missing across the set.

## Diagrams in Figma or FigJam

Only when the user chose it in the form or asked for it.

1. **Confirm the target.** State the connected file's name and the page you will create, and get a yes. If the name differs from the file recorded in `ux/PROJECT.md` (a copy, a backup, a library), stop and ask.
2. **Follow the file's conventions.** Read the existing page list first. Match its naming pattern, including an emoji or icon prefix if pages use one, and place the new page next to related pages. Never create a page whose name already exists.
3. **Match the file's diagram language** if it has one (fonts, colours, annotation components of a wireframe kit). Otherwise use a plain greyscale set with one accent colour.
4. **Structure.** A "Read me" section with a one-paragraph explanation, a legend of every node type, and the path to the Markdown file. Then one Section per flow, titled with the flow ID and name, with persona, frequency, challenge IDs and the goal in a header.
5. **Node types**, each visually distinct: entry point, action or system response, screen, decision, error or degraded state, exit. Tag assumptions (dashed outline plus a small "ASSUMPTION" label) and undesigned screens ("NOT DESIGNED").
6. **Layout.** Happy path on one straight row, left to right. Branches above and below it. Label every edge that leaves a decision; when several branches share a trunk, put each label next to its target.
7. **Connectors.** FigJam has real connectors. A Figma design file does not: draw arrows as vector paths with an arrow cap, with orthogonal elbows.
8. **Verify.** Screenshot every section after drawing. Check for overlapping lines and nodes, clipped text and unlabelled branches; fix and re-check. Say which sections you checked.
9. Keep diagram and Markdown in step: same node names, same flow IDs.

## Output

`ux/03-flows/flows.md` (or one file per flow for large projects), `ux/03-flows/ia.md`, `ux/03-flows/screen-inventory.md`.

## Finish

Save outputs, update the Stage status row and the Design files table in `ux/PROJECT.md` if it exists, list open questions and risky assumptions in the flows, and suggest the next block: usually `ucd-wireframes`, starting with the most important screen the flows found to be undesigned.
