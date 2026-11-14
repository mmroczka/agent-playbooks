---
name: release-flow
description: Use when preparing commits or pull requests, merging changes, or determining how a repository releases and deploys.
---

## Select the workflow

Resolve the current working directory's Git repository root and absolute common
Git directory. Outside Git, use the bundled workflow.

First inspect `<common-git-directory>/skill-overrides/release-flow` itself, including
whether it is a symlink. If present but broken, unreadable, or missing its readable
`SKILL.md`, report the configuration error and stop. Otherwise select the first
available workflow in this order:

1. `<common-git-directory>/skill-overrides/release-flow/SKILL.md`
2. `<repository-root>/.agents/skills/release-flow/workflow.md`
3. In older checkouts only, `<repository-root>/.claude/skills/release-flow/SKILL.md`,
   provided it is a standalone workflow, not a selection or compatibility entry.
4. `workflow.md` beside this entry.

Read and follow only the selected workflow, preserving the user's arguments.
Resolve its companion files relative to that workflow file. A private override
is a complete workflow, not another selection entry. If a configured override
is broken or unreadable, report it instead of silently using a different workflow.
Repository-wide instructions still apply.
