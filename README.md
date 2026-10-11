# UCD Toolkit

A set of Claude skills that turn a User-Centred Design process into reusable blocks. Each block covers one stage, from research to post-design audit, and can be run on any product, on a new project or one already in progress.

## The blocks

| Command | Stage | What it does |
|---|---|---|
| `/ucd-kickoff` | Setup | Runs an intake interview, analyses documents, links and Figma files, and writes the project brief |
| `/ucd-research` | Research | Plans research (interview guides, surveys, screeners) or synthesises raw material into themes and insights |
| `/ucd-personas` | Personas | Builds personas with goals, behaviours and the challenges they face |
| `/ucd-flows` | Flows & IA | Task analysis, user flows, navigation model and screen inventory |
| `/ucd-wireframes` | Wireframes | Low-fidelity specs with states and annotations, optionally built in Figma |
| `/ucd-hifi` | Hi-fi | High-fidelity screens using the project's design system, plus handoff notes |
| `/ucd-audit` | Audit | Heuristic evaluation, accessibility checks and design-system consistency review of a component, flow or screen |
| `/ucd-status` | Any time | Shows where the project stands and recommends the next step |

## How it works

**The skills hold the method; the project holds the knowledge.** Nothing in the toolkit is specific to one product. `/ucd-kickoff` writes a brief to `ux/PROJECT.md` in the project folder, and each stage saves its output beside it:

```
your-project/
  ux/
    PROJECT.md        ← brief, sources, design files, stage status
    inputs/           ← summaries of documents you provided
    01-research/
    02-personas/
    03-flows/
    04-wireframes/
    05-hifi/
    06-audit/
```

Each block reads the brief and the output of earlier stages, so context does not have to be explained again in every session.

**Every block also works on its own.** If there is no brief, the block asks only the few questions it needs and proceeds. The stage order is a default, not a gate: you can run an audit on an existing screen without having done anything else.

**Traceability.** Persona challenges get stable IDs. Flows, wireframes and audit findings refer back to them, so a design decision can be traced to the user problem it addresses.

## Principles built in

- Research and personas never invent participants, quotes or statistics. Without real data, output is labelled as assumptions or proto-personas to validate.
- Anything unverified is marked `[assumption]`.
- Nothing is written to a Figma file without confirmation, and an audit never changes the design itself.
- An audit is an expert review. It complements usability testing with real users and does not replace it.

## The audit

`/ucd-audit` accepts a Figma link, the current Figma selection, screenshots or a URL, and evaluates against:

- Nielsen's 10 usability heuristics
- WCAG 2.2 AA quick checks (contrast, target size, focus, labels)
- Design-system consistency (tokens, components, states)
- Persona challenges, when personas exist

Each finding has a location, the heuristic or criterion violated, evidence, a severity from 0 to 4 and a concrete fix. Running it again on the same scope compares against the previous report. The checklists live in [ucd-audit/heuristics.md](ucd-audit/heuristics.md).

## Installation

Requires [Claude Code](https://claude.com/claude-code) (desktop app, CLI or IDE extension). Clone this repository as your personal skills folder.

Windows (PowerShell):

```powershell
git clone https://github.com/marcinpociask/ucd-toolkit.git "$env:USERPROFILE\.claude\skills"
```

macOS / Linux:

```bash
git clone https://github.com/marcinpociask/ucd-toolkit.git ~/.claude/skills
```

The target folder must not exist yet, or must be empty. Restart Claude afterwards. To update later, run `git pull` in that folder.

For the Figma-based blocks (wireframes, hi-fi, audit), connect a Figma MCP connector in Claude. Without one, the audit works from screenshots.

## Getting started

Open a session in a project folder and run:

```
/ucd-kickoff
```

Or go straight to a single block, for example:

```
/ucd-audit https://www.figma.com/design/…?node-id=12-345
```

## Customising

Each skill is a plain Markdown file (`<skill>/SKILL.md`). Edit the instructions, templates or checklists to match your own process; changes apply the next time the skill runs.

## Author

Marcin Pociask
