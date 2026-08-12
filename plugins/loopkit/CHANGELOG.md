# Changelog

## 0.4.0

- Added host task list mirroring so the running module is visible in the tool UI.
- Added `loopkit-module` and `loopkit-gate` agents so delegated modules render as named, self-explaining subagents.
- Added `references/progress-display.md` and a `delegated` observability event.

## 0.3.0

- Added canonical module ordering from configured module registration order.
- Added guidance for semantically inserting extra selected modules without overusing `requires`.
- Added TDD module ordering examples for mixed implementation workflows.

## 0.2.0

- Added explicit orchestrator ownership rules for `/loopkit:run`.
- Added subagent delegation contract for bounded module and subtask execution.
- Added module-boundary context compaction guidance and observability records.

## 0.1.0

- Initial LoopKit plugin with setup, run, module, status, and debug skills.
- Added references for local state, module contracts, run selection, observability, and cross-tool adaptation.
