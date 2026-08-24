---
name: loopkit-run
description: Start or resume a configurable local workflow loop from an issue, spec, task, pasted request, branch, or existing local work.
compatibility: opencode,codex
---

# LoopKit Run

Use this skill to run a local workflow loop made of configured modules.

Load and follow the canonical instructions in `../../../plugins/loopkit/skills/run/SKILL.md`.

Keep shared references reachable from `../../../plugins/loopkit/references/`, especially:

- `workflow.md`
- `run-selection.md`
- `state.md`
- `observability.md`
- `module-contract.md`

## OpenCode V2 Host Rules

- Use the canonical module-selection flow: default set, all configured modules, custom selection, or resume. Ask for comma-separated module IDs when native multi-select is unavailable.
- OpenCode V2 has no native TaskCreate/TodoWrite-style task list. Keep `modules.yml` as the source of truth and report progress as `run <run-id> · module <n>/<total> · <module-id> · <status>`.
- Delegate only one bounded module or subtask at a time with the configured `loopkit-module` or `loopkit-gate` subagent. Never delegate the whole run.

When the host tool does not support namespaced slash commands, treat `loopkit-run` as equivalent to `/loopkit:run`.
