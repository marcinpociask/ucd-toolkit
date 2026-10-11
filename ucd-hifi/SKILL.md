---
name: ucd-hifi
description: High-fidelity design block of the UCD toolkit. Takes wireframes or existing screens to hi-fi mockups using the project's design system (tokens, variables, components), including states, responsive behaviour and handoff notes. Works with Figma connectors when available. Works standalone or with ux/PROJECT.md. Use for "make this hi-fi", "apply the design system", "polish these screens", "prepare for handoff".
---

# UCD hi-fi

## Start-up (every run)

1. Look for `ux/PROJECT.md` in the working directory. If it exists, read it, plus `ux/04-wireframes/` and `ux/05-hifi/`.
2. If it does not exist, run standalone: ask only the minimum context below (skip what the user already said) and invite Figma URLs, brand guidelines or screenshots. Offer once to save the answers as `ux/PROJECT.md`.
3. Missing upstream work is never a blocker. Proceed on stated assumptions and mark each `[assumption]`.

**Minimum context:** which screens, the source (wireframes, existing screens, or description), the design system or library to use (or that none exists yet), platform and viewports, accessibility target (default WCAG 2.2 AA).

### Ask with a clickable form

Ask the questions below as a clickable form with the AskUserQuestion tool (up to 4 questions per form, 2–4 options each; the user can always pick "Other" and type). Skip any already answered by the brief or the conversation. If the tool is not available, use numbered options in text. Ask the rest of the minimum context in plain text.

| Question | Options | Multi-select |
|---|---|---|
| What is the source? | Wireframes · Existing screens to polish · A description only | no |
| Which design system? | Existing Figma library · Third-party kit (Material, HIG…) · None yet, propose a foundation | no |
| Which viewports? | Mobile · Tablet · Desktop · Other device | yes |
| Which states to cover? | Core: default, loading, empty, error (Recommended) · Interactive: hover, pressed, focus, disabled · Success and confirmation · Dark mode | yes |

## Method

1. **Read the design system first.** With a Figma connector, pull the file's variables, styles and components before designing. Reuse what exists; never hard-code a value that has a token, and never redraw a component that exists in the library.
2. **No design system yet?** Propose a minimal foundation and get agreement before applying it: colour roles (with contrast-checked pairs), type scale, spacing scale, radius, elevation, and the core components the screens need.
3. **Build the screens**: confirm the target file and page, check for existing frames before creating, use auto layout and component instances, name layers meaningfully, keep frames inside a Section.
4. **Cover the states** from the wireframe spec (default, loading, empty, error, success, disabled, focus) and the viewports agreed.
5. **Validate visually**: screenshot after each screen, check alignment, spacing rhythm, hierarchy, contrast and truncation with long content; fix and re-check (up to three passes), then show the user.
6. **Handoff notes** in `ux/05-hifi/<screen>.md`: tokens and components used, new components or tokens introduced and why, interaction and motion notes, responsive rules, accessibility notes (focus order, labels, contrast results), open questions.

## Rules

- Confirm before writing to a Figma file, and never modify library components or variables without an explicit yes.
- Flag any place the design departs from the design system instead of hiding it.

## Finish

Save notes, record Figma links in `ux/PROJECT.md` (Design files and Stage status) if it exists, summarise what was built and what is still open, and suggest running `ucd-audit` on the result.
