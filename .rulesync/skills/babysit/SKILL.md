---
name: babysit
description: Use when asked to babysit, watch, or shepherd a pull request through review, or work through reviewer comments.
---

## Select the workflow

Resolve the current working directory's Git repository root and absolute common
Git directory. Outside Git, use the bundled workflow.

First inspect `<common-git-directory>/skill-overrides/babysit` itself, including
whether it is a symlink. If present but broken, unreadable, or missing its readable
`SKILL.md`, report the configuration error and stop. Otherwise select the first
available workflow in this order:

1. `<common-git-directory>/skill-overrides/babysit/SKILL.md`
2. `<repository-root>/.agents/skills/babysit/workflow.md`
3. In older checkouts only, `<repository-root>/.claude/skills/babysit/SKILL.md`,
   provided it is a standalone workflow, not a selection or compatibility entry.
4. `workflow.md` beside this entry.

Read and follow only the selected workflow, preserving the user's arguments.
Resolve its companion files relative to that workflow file. A private override
is a complete workflow, not another selection entry. If a configured override
is broken or unreadable, report it instead of silently using a different workflow.
Repository-wide instructions still apply.
