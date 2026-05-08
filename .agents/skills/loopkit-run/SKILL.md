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

When the host tool does not support namespaced slash commands, treat `loopkit-run` as equivalent to `/loopkit:run`.
