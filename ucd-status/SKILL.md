---
name: ucd-status
description: Shows where a project stands in the UCD toolkit and what to do next. Reads ux/PROJECT.md and the ux/ folder, reports each stage's status and outputs, flags stale or missing work, and recommends the next block. Use for "where are we in the UX process", "ucd status", "what's next", or when picking up a project after a break.
---

# UCD status

1. Read `ux/PROJECT.md`. If it does not exist, say so, list any UX material you can find in the working directory, and suggest `ucd-kickoff` to onboard the project. Stop there.
2. Check each stage folder (`ux/01-research/` … `ux/06-audit/`) against the Stage status table. Correct the table where files and status disagree, and tell the user what you changed.
3. Report as a table: stage, status, key outputs (as links), last updated.
4. Flag:
   - Downstream work older than the upstream work it depends on (e.g. personas revised after flows were written)
   - Outputs carrying many `[assumption]` markers that later stages rely on
   - Audit findings of severity 3–4 still open
   - Open questions in the brief that block the next stage
5. Recommend one next action and the block to run for it. Any block can be run on its own at any time; the order is a default, not a gate.
