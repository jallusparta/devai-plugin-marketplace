# LoopKit Workflow

LoopKit runs configurable local workflow loops made of modules.

## Principles

- A loop is a selected sequence of modules.
- Modules are team-owned and easy to edit.
- Runtime state is local and observable.
- External communication is a module output, not a global assumption.
- Implementation is optional and interchangeable.
- Quality gates and fix loops must leave evidence.

## Standard Run Lifecycle

1. Resolve or create local config.
2. Capture input into the run state.
3. Ask which modules to execute.
4. Resolve module dependencies.
5. Mirror the selected modules into the host task list.
6. Execute modules in dependency order, parallelizing only when safe.
7. Write module attempts, events, and debug summaries.
8. Apply commit policy.
9. Produce a final local report.

## Orchestrator Ownership

The current agent that receives `/loopkit:run` is the orchestrator. It must execute the LoopKit lifecycle itself instead of forwarding the entire command to a generic subagent.

The orchestrator owns:

- config loading
- run creation and resume
- module selection and dependency ordering
- global run state files
- external write approvals
- the host task list mirror and delegation labels described in `progress-display.md`
- final reporting

Subagents may be used for one bounded module or module subtask at a time. They should not own the run, select additional modules, or assume slash-command execution semantics. They return structured results to the orchestrator, and the orchestrator records those results in local state.

## Module Execution

For each module:

1. Read only the relevant run state and module instructions.
2. Mark the module task `in_progress` and append the `started` event.
3. Execute the module procedure.
4. Record all commands, decisions, failures, fixes, and evidence.
5. Apply the module commit policy.
6. Update module status and complete the module task with its terminal event.
7. Persist the module attempt report, events, debug notes, and context summary.
8. Check context usage. If it is greater than 40%, compact before continuing and record the compaction event.
9. Continue, retry, or stop according to pass criteria and blockers.

## Context Compaction

LoopKit treats module boundaries as safe compaction checkpoints. At the end of every module, after durable state has been written, estimate current context usage.

If context usage is greater than 40%:

1. Update `context-summary.md` with the current continuation summary.
2. Append a `context_compaction` event to `events.jsonl`.
3. Add a human-readable note to `state.md` and `debug.md`.
4. Compact before starting the next module, or ask the host tool/user to compact if automatic compaction is not available.
5. Resume from durable run state and `context-summary.md`, not from chat history.

The threshold may be made configurable, but the default is 40%.

## Parallel Work

Parallelize only when selected modules or module-generated tasks are independent. Serialize work when modules edit the same files, rely on shared runtime state, or have unclear dependencies.
