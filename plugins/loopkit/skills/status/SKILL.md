---
name: status
description: Show active LoopKit runs, selected modules, current state, blockers, and next actions.
---

# LoopKit Status

Use this skill to inspect local LoopKit runs without changing code or state unless the user explicitly asks for cleanup.

Reference files:

- `../../references/state.md` for run state layout.
- `../../references/observability.md` for event interpretation.

## Workflow

1. Locate the LoopKit state directory.
2. List active runs under `<state_dir>/runs/`.
3. For each relevant run, read `manifest.yml`, `modules.yml`, recent `events.jsonl` entries, and `state.md`.
4. Summarize status without loading bulky evidence unless needed.
5. Identify the next action: resume, debug, rerun module, create module, or final handoff.

## Output

Return:

- run id
- input summary
- current status
- selected modules and their state
- last significant event
- blockers
- next command or action
