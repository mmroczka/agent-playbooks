# Agent playbooks

Public reusable guidance. The [authoring contract](AGENTS.md) owns contribution rules.

## Rulesync pilot

Authored pilot skills live in `.rulesync/skills/`. Use Rulesync 43.8.2.
For a new consumer selection, create the lockfile with a plain install first:

```sh
npx --yes rulesync@43.8.2 install
```

Review and commit the generated lockfile. For subsequent installs or CI:

```sh
npx --yes rulesync@43.8.2 install --frozen
npx --yes rulesync@43.8.2 generate
```

The default preview writes Claude Code and Codex skills under `.rulesync-output/`,
leaving active installations untouched. Installation fetches dependencies;
generation emits runtime files. Commit `rulesync.jsonc` and a `rulesync.lock` when external sources are selected,
not curated caches or generated output. Sources and skill selections are explicit.

For an update, change the pinned source revision, run `install --update`, review
the source diff and lockfile, then regenerate in a fresh preview directory.
Local additions use distinct skill names. A same-name local skill replaces the
entire upstream skill; upstream changes require manual review, not an automatic merge.

Hermes skills require global scope in this version. Verify generation with an
isolated home before the integration owner selects a real profile. Installed files
do not prove runtime loading or implicit selection.

Generate into fresh, exclusively owned output directories. Default generation can
leave removed companion files, while `--delete` can remove unrelated skills.
Verify the complete output file manifest, preserve the previous config/lock/source
revision and output snapshot, and restore that snapshot for rollback. Mixed-owner
installation cleanup belongs to the scoped rollout, not this preview.

## Consumer selection

Select this repository’s `.rulesync/skills` source path and the desired skills (`linear-workflow`, `ticket-impact-scan`, `release-flow`, `babysit`)
explicitly from a reviewed commit. For GitHub transport the source form is
`loop-guardian/agent-playbooks@<reviewed-commit>:.rulesync/skills`.
Workspace adaptations remain additive skills in their owning repositories.
Teammates can consume this baseline without access to a personal repository.

Preview output is for inspection. Runtime installation, profile selection and actual
skill loading are separate integration steps; these commands do not activate skills
in an existing user catalog.

## Workflow overrides

The workflow packages use one discoverable `SKILL.md` and load one selected body
on invocation. Selection is private clone override, repository workflow, legacy
Claude repository workflow, then bundled personal default. Repository-wide rules
still apply. Other skill packages are unchanged.

Keep repository bodies in `.agents/skills/<name>/workflow.md` with the entry beside
it. Claude uses a small `.claude/skills/<name>/SKILL.md` compatibility entry pointing
to the canonical entry. Before replacing an existing standalone entry, move its
repository-specific workflow body and required companions into the canonical package.
Keep the existing directory so local extras survive updates.
Companion files belong beside the selected workflow. Older checkouts with a standalone
Claude workflow remain supported during migration.

For a private replacement, put a complete workflow package at
`<absolute-git-common-directory>/skill-overrides/<name>/SKILL.md`, or symlink that
package directory to your private source. Resolve the directory from the target
checkout with `git rev-parse --path-format=absolute --git-common-dir`. This is local
Git metadata, shared by the clone's worktrees and never committed. Each developer
owns their own replacements; another clone requires its own opt-in. Remove the
replacement to resume repository defaults. Do not point it at another selection
entry; use the actual workflow body and its companions.

Claude and Hermes select a same-name entry natively. For Codex, when both personal
and repository entries exist, keep exactly one advertised entry using **user-level**
`~/.codex/config.toml` selection. Install or update the complete personal package to
this workflow-selection version before applying the filters:

```toml
[[skills.config]]
name = "ticket-impact-scan"
enabled = false

[[skills.config]]
path = "/absolute/path/to/personal/ticket-impact-scan/SKILL.md"
enabled = true
```

Use the installed canonical absolute path and repeat for each selected package.
The entry still selects the current repository's body. Project-level skill filters
are not applied by Codex. Remove both filters when removing the personal package,
or repository discovery remains disabled. Developers without personal copies need
no filters or setup. Restart an existing agent session after changing installations
or selection. This controls skill discovery, not access permissions or MCPs.
