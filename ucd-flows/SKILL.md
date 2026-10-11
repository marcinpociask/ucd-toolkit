---
name: ucd-flows
description: Flows and information architecture block of the UCD toolkit. Produces task analysis, user flows (happy path, alternatives, errors), sitemap or navigation model and a screen inventory, traced to persona goals and challenges. Works standalone or with ux/PROJECT.md. Use for "map the user flow", "information architecture", "sitemap", "what screens do we need".
---

# UCD flows and IA

## Start-up (every run)

1. Look for `ux/PROJECT.md` in the working directory. If it exists, read it, plus `ux/02-personas/` and `ux/03-flows/`.
2. If it does not exist, run standalone: ask only the minimum context below (skip what the user already said) and invite documents, links or Figma URLs. Offer once to save the answers as `ux/PROJECT.md`.
3. Missing upstream work is never a blocker. Proceed on stated assumptions and mark each `[assumption]`.

**Minimum context:** the product and platform, who the user is for this flow, the task or goal to map, existing screens or navigation that must be respected.

### Ask with a clickable form

Ask the questions below as a clickable form with the AskUserQuestion tool (up to 4 questions per form, 2–4 options each; the user can always pick "Other" and type). Skip any already answered by the brief or the conversation. If the tool is not available, use numbered options in text. Ask the rest of the minimum context in plain text.

| Question | Options | Multi-select |
|---|---|---|
| Which outputs do you need? | User flows · Sitemap or navigation model · Screen inventory · Task analysis | yes |
| What is the starting point? | Personas and goals · Existing screens or navigation to respect · A description only | no |
| Where should diagrams go? | Markdown file (Mermaid) · FigJam · Both | no |
| Which platform? | Mobile · Web · Desktop · Other device | no |

## Method

1. **Scope.** List the key tasks. If personas exist, derive tasks from their goals and jobs to be done; confirm the priority order with the user before detailing more than three flows.
2. **Task analysis** per task: trigger, preconditions, steps, decisions, success criteria, what can go wrong.
3. **User flow** per task as a Mermaid flowchart plus a short step table. Always include entry points, the happy path, alternative paths, error and empty states, and exits. Note which persona challenge IDs each flow addresses.
4. **IA.** Sitemap or navigation model (Mermaid or indented list): top-level sections, hierarchy, cross-links. State the organising principle and one alternative you rejected.
5. **Screen inventory** table: screen, purpose, key content and actions, states needed (default, loading, empty, error, success), flows it belongs to.
6. If the user wants the diagrams in FigJam or Figma and a Figma connector is available, offer to create them there; confirm before writing to any file.

## Output

`ux/03-flows/flows.md` (or one file per flow for large projects), `ux/03-flows/ia.md`, `ux/03-flows/screen-inventory.md`.

## Finish

Save outputs, update the Stage status row in `ux/PROJECT.md` if it exists, list open questions and risky assumptions in the flows, and suggest the next block (usually `ucd-wireframes`).
