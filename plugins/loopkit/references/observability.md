# Observability

LoopKit runs must be understandable without relying on chat history. Each run writes machine-readable events and human-readable summaries.

## Event Log

Write append-only JSON lines to:

```text
<state_dir>/runs/<run-id>/events.jsonl
```

Example events:

```json
{"ts":"2026-05-07T10:15:00Z","module":"lint","event":"started","attempt":1}
{"ts":"2026-05-07T10:16:00Z","module":"lint","event":"failed","attempt":1,"summary":"3 lint errors","evidence":"module-runs/lint/attempt-001.md"}
{"ts":"2026-05-07T10:22:00Z","module":"lint","event":"fix_committed","commit":"abc123","summary":"Removed inline style"}
{"ts":"2026-05-07T10:24:00Z","module":"lint","event":"passed","attempt":2}
{"ts":"2026-05-07T10:25:00Z","module":"lint","event":"context_compaction","threshold":0.4,"usage_before":"estimated >40%","summary_path":"context-summary.md"}
```

## Module Attempts

Each module attempt should write a concise report:

```text
<state_dir>/runs/<run-id>/module-runs/<module-id>/attempt-001.md
```

Include:

- inputs used
- commands run
- result
- failures
- fixes applied
- commits created
- evidence paths
- next action

## Debug Summary

Maintain or generate:

```text
<state_dir>/runs/<run-id>/debug.md
```

This file is for humans. It should answer:

- What ran?
- What was skipped and why?
- What failed?
- What fixed it?
- What commits were created?
- What external writes happened?
- When did context compaction happen?
- What should happen next?

## Context Compaction Records

When context usage is greater than 40% at a module boundary, record compaction in:

- `events.jsonl` with event `context_compaction`
- `state.md` as a concise continuation note
- `debug.md` with the reason, threshold, and summary path
- `context-summary.md` as the durable continuation summary

The compaction record should identify the module that just completed, the threshold used, whether the threshold was estimated or measured, and where the continuation summary was written.
