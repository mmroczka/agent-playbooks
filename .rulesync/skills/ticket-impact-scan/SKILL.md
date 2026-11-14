---
name: ticket-impact-scan
description: Find existing Linear tickets that completed branch or PR changes affect or make stale, when the work is ready for review or merge or the developer requests an impact scan.
---

## Select the workflow

Resolve the current working directory's Git repository root and absolute common
Git directory. Outside Git, use the bundled workflow.

First inspect `<common-git-directory>/skill-overrides/ticket-impact-scan` itself, including
whether it is a symlink. If present but broken, unreadable, or missing its readable
`SKILL.md`, report the configuration error and stop. Otherwise select the first
available workflow in this order:

1. `<common-git-directory>/skill-overrides/ticket-impact-scan/SKILL.md`
2. `<repository-root>/.agents/skills/ticket-impact-scan/workflow.md`
3. In older checkouts only, `<repository-root>/.claude/skills/ticket-impact-scan/SKILL.md`,
   provided it is a standalone workflow, not a selection or compatibility entry.
4. `workflow.md` beside this entry.

Read and follow only the selected workflow, preserving the user's arguments.
Resolve its companion files relative to that workflow file. A private override
is a complete workflow, not another selection entry. If a configured override
is broken or unreadable, report it instead of silently using a different workflow.
Repository-wide instructions still apply.
