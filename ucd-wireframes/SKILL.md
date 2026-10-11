---
name: ucd-wireframes
description: Wireframes block of the UCD toolkit. Turns flows or a described task into low-fidelity wireframes with layout, content hierarchy, states and annotations, as written specs and, when a Figma connector is available, as frames in Figma. Works standalone or with ux/PROJECT.md. Use for "wireframe this screen", "lo-fi for this flow", "sketch the layout".
---

# UCD wireframes

## Start-up (every run)

1. Look for `ux/PROJECT.md` in the working directory. If it exists, read it, plus `ux/02-personas/README.md`, `ux/03-flows/` and `ux/04-wireframes/`.
2. If it does not exist, run standalone: ask only the minimum context below (skip what the user already said) and invite documents, sketches, screenshots or Figma URLs. Offer once to save the answers as `ux/PROJECT.md`.
3. Missing upstream work is never a blocker. Proceed on stated assumptions and mark each `[assumption]`.

**Minimum context:** platform and viewport(s), who the user is and what they are trying to do, which screens or flow to wireframe, where the result should go (written spec, Figma, or both).

## Method

1. **Confirm scope**: list the screens and states you will produce before producing them.
2. **Spec each screen** in `ux/04-wireframes/<screen>.md`:
   - Purpose and the flow step it serves
   - Content hierarchy, top to bottom, with priority (primary / secondary / tertiary)
   - Components and actions; the single primary action
   - States: default, loading, empty, error, success, and any permission or offline states
   - Annotations: behaviour, rules, edge cases, open questions
   - Which persona challenge IDs it addresses
3. **Keep it lo-fi**: greyscale, real representative copy in place of lorem ipsum where copy carries meaning, no brand styling. The point is structure and priority.
4. **Offer two layout options** for the screens that matter most, with the trade-off of each, and recommend one.
5. **In Figma** (when a connector is available and the user wants it): confirm the target file and page first. Check whether the page or frames already exist before creating. Place frames inside a Section named for the flow, name layers meaningfully, use auto layout, and take a screenshot after creating to verify alignment and spacing; fix and re-check.

## Self-check before handing over

Every screen has one clear primary action, a way back or out, all states from the inventory, and touch targets or click areas of sensible size for the platform.

## Finish

Save specs, record Figma links in `ux/PROJECT.md` (Design files and Stage status) if it exists, summarise decisions and open questions, and suggest the next block (`ucd-hifi`, or `ucd-audit` for an early review).
