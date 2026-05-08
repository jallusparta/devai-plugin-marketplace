---
name: debug
description: Inspect detailed LoopKit run events, module attempts, fixes, commits, evidence, and external writes.
---

# LoopKit Debug

Use this skill when the user asks what happened during a run, why a module failed, what fixes were applied, which commits were created, or what evidence was produced.

Reference files:

- `../../references/observability.md` for event and attempt formats.
- `../../references/state.md` for run state layout.

## Workflow

1. Locate the requested run. If no run is specified, list likely active or recent runs and ask which one to inspect.
2. Read `events.jsonl`, `debug.md`, and relevant module attempt reports.
3. If the user asks for a specific module or failure, load only that module's attempt files and evidence index.
4. Summarize what happened in chronological order.
5. Identify fixes, commits, skipped work, external writes, and remaining risks.
6. Do not rerun modules or edit files unless the user explicitly asks.

## Output

Return:

- concise timeline
- failed attempts and causes
- fixes applied
- commits created
- evidence paths
- external communication performed or prepared
- recommended next action
