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

## Execution Profiles

A module can declare the `agent`, `model`, and `isolation` it should run with, for example a fast model for a mechanical gate and a stronger one for review work. Config supplies the defaults, modules override them, and the user can override per run. Built-in agents inherit the host session model; setup recommends `sonnet` for delegated work when a specific default is wanted. Host adapters may map that alias to a provider-specific model.

See [references/module-contract.md](references/module-contract.md) for the resolution order.

## Run Progress

While a run executes, the selected modules are mirrored into the host task list, and each delegated module runs as a named `loopkit-module` or `loopkit-gate` subagent labelled with its module id. State files stay the source of truth.

OpenCode V2 does not currently expose a native task-list tool. Its adapter keeps the same mirror in `modules.yml` and reports the current module as a progress line instead. Configure the two bounded agents in the host's `agents` configuration so OpenCode can delegate module and gate work by name.

See [references/progress-display.md](references/progress-display.md) for details.

## Cross-Tool Use

LoopKit is packaged as a Claude Code plugin first. Its OpenCode/Codex adapter skills are published under `.agents/skills/`, while the canonical skill instructions and shared references remain under this plugin directory.

See [references/adapters.md](references/adapters.md) for compatibility notes.
