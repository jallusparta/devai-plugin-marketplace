# LoopKit Plugin

LoopKit is a lightweight framework for creating, running, observing, and evolving local AI workflow loops from configurable modules.

It is intentionally not a fixed implementation pipeline. Teams define the modules they need, such as clarification, planning, implementation, validation, review, handoff, or documentation. LoopKit provides the local state model, setup wizard, module contract, run selection, status, and debug workflow.

## Commands

- `/loopkit:setup` - initialize or update a local LoopKit configuration for a repository or workspace.
- `/loopkit:run` - start or resume a loop run from an issue, spec, task, pasted request, or existing local work.
- `/loopkit:module` - create, edit, review, or explain a loop module.
- `/loopkit:status` - list active runs and summarize current state.
- `/loopkit:debug` - inspect detailed run events, module attempts, fixes, commits, and evidence.

## Design Principles

- Keep runtime state local by default.
- Keep external tracker updates explicit and module-owned.
- Make modules small, readable, and easy to change.
- Treat implementation as one optional module, not the core assumption.
- Prefer observable runs over hidden chat history.
- Mirror run progress into the host UI so the current stage is visible without opening state files.
- Keep the run orchestrator in control of state; delegate only bounded module work.
- Compact at module boundaries when context usage grows beyond the configured threshold.

## Local State

LoopKit uses a configurable local state directory, defaulting to `.loopkit/` in the target repository or workspace. Runtime state is intended to stay local and should normally be gitignored.

See [references/state.md](references/state.md) for details.

## Run Progress

While a run executes, the selected modules are mirrored into the host task list, and each delegated module runs as a named `loopkit-module` or `loopkit-gate` subagent labelled with its module id. State files stay the source of truth.

See [references/progress-display.md](references/progress-display.md) for details.

## Cross-Tool Use

LoopKit is packaged as a Claude Code plugin first. Its skill files are written in the Agent Skills style so they can later be adapted to OpenCode and Codex.

See [references/adapters.md](references/adapters.md) for compatibility notes.
