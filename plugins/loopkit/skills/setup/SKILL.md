---
name: setup
description: Initialize or update a local LoopKit configuration for a repository or workspace.
---

# LoopKit Setup

Use this skill when the user wants to set up LoopKit for a new repository, workspace, team, or organization, or when they want to change the local loop configuration.

Reference files:

- `../../references/setup-wizard.md` for the setup flow.
- `../../references/config-template.yml` for the config shape.
- `../../references/state.md` for local state layout.
- `../../references/module-contract.md` for module format.

## Workflow

1. Determine the target repository or workspace.
2. Check whether a LoopKit config already exists in the configured or default state directory.
3. If no config exists, run the quick setup wizard from `setup-wizard.md`.
4. If a config exists, ask whether to view, update, or replace it.
5. Keep setup local. Do not create external tracker comments or commits unless the user explicitly asks.
6. Write or update `<state_dir>/config.yml`.
7. If the user wants initial modules, route to `/loopkit:module` after config is created.

## Output

Summarize:

- state directory
- tracker type
- external write policy
- default commit policy
- configured modules or note that none exist yet
- next useful command
