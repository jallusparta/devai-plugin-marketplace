---
name: run
description: Start or resume a configurable local workflow loop from an issue, spec, task, pasted request, or existing work.
---

# LoopKit Run

Use this skill to run a local workflow loop made of configured modules. The input can be any useful work source: issue number, issue URL, spec file, pasted request, task description, branch, worktree, or existing local changes.

Reference files:

- `../../references/workflow.md` for the run lifecycle.
- `../../references/run-selection.md` for module selection.
- `../../references/state.md` for run state.
- `../../references/observability.md` for events and debug output.
- `../../references/module-contract.md` for module execution rules.
- `../../references/progress-display.md` for host task list and subagent labelling.

## Workflow

1. Execute `/loopkit:run` as the current orchestrator. Do not delegate the whole command to a generic subagent.
2. Locate and read the LoopKit config. If missing, ask to run `/loopkit:setup`.
3. Resolve the input source and create or resume `<state_dir>/runs/<run-id>/`.
4. Snapshot the source input to `input.md` and initialize `manifest.yml`, `modules.yml`, `events.jsonl`, `state.md`, `debug.md`, and `context-summary.md`.
5. Ask which modules should execute using the selection flow in `run-selection.md`.
6. Resolve module dependencies and safe parallelization.
7. Mirror the selected modules into the host task list in dependency order, following `progress-display.md`.
8. Execute selected modules according to their module contracts. The orchestrator may delegate one bounded module or module subtask at a time, but it keeps ownership of run state. Delegate with the LoopKit agent types and module-named descriptions from `progress-display.md`.
9. Record every module start, result, failure, fix, commit, skip, external write, and compaction checkpoint in `events.jsonl`, and flip the module's task status in the same step.
10. Write module attempt reports under `module-runs/<module-id>/`.
11. Maintain `state.md`, `debug.md`, and `context-summary.md` as the run progresses.
12. At the end of each module, persist module results first, then check context usage. If context usage is greater than 40%, compact before continuing and record the compaction. Rebuild the task list from `modules.yml` after compaction.
13. Produce or update `final-report.md` when selected modules complete or the run stops.

## Guardrails

- Never treat `/loopkit:run` as a generic implementation prompt.
- Never send the entire `/loopkit:run` command to a generic subagent and expect slash-command semantics there.
- Do not start implementation until the config has been read and the run directory exists.
- The orchestrator owns `manifest.yml`, `modules.yml`, `events.jsonl`, `state.md`, `debug.md`, `context-summary.md`, and `final-report.md`.
- Subagents may execute only one scoped module or module subtask. They return structured results; the orchestrator persists global run state.
- Delegate modules to `loopkit-module` or `loopkit-gate`, never to a generic agent, and label each delegation `<module-id>: <short action>`.
- The host task list is a mirror of `modules.yml`. Never let it drift, and never treat it as run state.
- Do not assume implementation is required. Run only selected modules.
- Do not invent default modules if none are configured.
- Do not post externally unless a selected module requests it, config allows it, and approval rules are satisfied.
- Apply commit policy from the module first, then the top-level default.
- If a module is unclear or unsafe, stop and ask before proceeding.
- Compact only after the current module report, events, debug notes, and context summary have been persisted.

## Output

Return a concise run summary:

- run id
- selected modules
- completed modules
- failed or blocked modules
- commits created
- evidence/debug paths
- next action
