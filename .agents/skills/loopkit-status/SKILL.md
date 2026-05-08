---
name: loopkit-status
description: Show active LoopKit runs, selected modules, current state, blockers, and next actions.
compatibility: opencode,codex
---

# LoopKit Status

Use this skill to inspect local LoopKit runs without changing code or state unless the user explicitly asks for cleanup.

Load and follow the canonical instructions in `../../../plugins/loopkit/skills/status/SKILL.md`.

Keep shared references reachable from `../../../plugins/loopkit/references/`, especially:

- `state.md`
- `observability.md`
