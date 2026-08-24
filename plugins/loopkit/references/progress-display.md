# Progress Display

A LoopKit run should be readable from the host tool's UI without opening state files. The run state files stay the source of truth; the UI is a mirror of them.

There are two display surfaces. Both are optional for correctness and required for a good run.

## 1. Host Task List

Most agent tools expose a live task or todo list (`TaskCreate`/`TaskUpdate` in current Claude Code, `TodoWrite` in older versions). LoopKit mirrors the selected modules into it so the user can see which stage is running.

Rules:

- After module selection is confirmed, create one task per selected module, in dependency order, before executing anything.
- Task text is `<module-id>: <module title>`. Keep it stable for the whole run so the list does not reshuffle.
- Set the task to `in_progress` at the same moment the `started` event is appended to `events.jsonl`.
- Set the task to `completed` at the same moment the terminal event (`passed`, `failed`, `blocked`, `skipped`) is appended.
- Exactly one module task is `in_progress` at a time, unless modules are running in parallel, in which case one per parallel module.
- A module retry does not create a new task. Keep the module task `in_progress` across its fix loop attempts.
- If a module ends in `failed` or `blocked`, complete its task and add one follow-up task describing the blocker and the next action.
- If the user adds or removes modules mid-run, update the task list to match `modules.yml`.
- After compaction, rebuild the task list from `modules.yml` and `context-summary.md`, not from chat history.

The task list is a mirror. If it ever disagrees with `modules.yml` and `events.jsonl`, the state files win.

If the host tool has no task list, skip this section and print a short module progress line instead: `run <run-id> · module 3/7 · lint · running`.

## 2. Named Module Subagents

When a module is delegated, the delegation should be visible and self-explaining in the UI. In Claude Code each subagent renders as its own labelled panel, so the label is the run's stage indicator.

Rules:

- Use the agent resolved for the module, never a generic agent. With no configuration that is `loopkit-module` for `task`, `handoff`, `report`, and `custom` modules, and `loopkit-gate` for `gate` modules. See the execution resolution rules in `module-contract.md`.
- The delegation description is `<module-id>: <short action>`, for example `lint: run eslint and fix violations`. No generic descriptions such as "implement the change".
- One delegation per module or bounded module subtask. Never delegate the whole run.
- For a fix loop, reuse the same description with an attempt suffix: `lint: fix violations (attempt 2)`.
- Record the delegation in `events.jsonl` with the module id and attempt so the UI panel and the event log can be matched afterwards.

## Not In Scope

Status line integration (`statusLine`, `subagentStatusLine`) is user-level configuration, not plugin-shipped. A repository that wants a persistent LoopKit status line can point its status line command at the newest `<state_dir>/runs/*/state.md`.
