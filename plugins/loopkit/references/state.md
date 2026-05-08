# Local State

LoopKit uses file-based state so runs are resumable, debuggable, and portable across AI coding tools.

## Default Layout

```text
.loopkit/
├── config.yml
└── runs/
    └── <run-id>/
        ├── manifest.yml
        ├── input.md
        ├── modules.yml
        ├── events.jsonl
        ├── state.md
        ├── debug.md
        ├── context-summary.md
        ├── module-runs/
        │   └── <module-id>/
        │       ├── attempt-001.md
        │       └── evidence/
        └── final-report.md
```

## File Roles

- `config.yml`: local LoopKit settings for the repository or workspace.
- `manifest.yml`: run identity, source input, selected modules, worktree, branch, status, and current phase.
- `input.md`: snapshot of the input request, issue, spec, or pasted text.
- `modules.yml`: selected modules, dependency order, statuses, and result paths.
- `events.jsonl`: append-only machine-readable run events.
- `state.md`: concise human-readable run journal.
- `debug.md`: detailed debug view of module attempts and fixes.
- `context-summary.md`: compact continuation state used after compaction or session recovery.
- `module-runs/`: module attempt reports and evidence.
- `final-report.md`: final local summary suitable for user review or external handoff.

## Ownership Rules

- The orchestrator owns global run state.
- Modules produce attempt reports and evidence.
- If subagents are used, they should return structured results or write scoped result files, not mutate global state directly unless the active module explicitly allows it.
- The orchestrator records subagent results in `events.jsonl`, `state.md`, `debug.md`, `context-summary.md`, `modules.yml`, and `final-report.md`.
- Failed, skipped, or blocked modules still get module reports and events.
- External tracker updates are not state. Record what was posted in events and attempt reports.

## Context Summary

`context-summary.md` is the durable continuation summary for compaction and recovery. Keep it concise but sufficient to continue the run without relying on chat history.

Include:

- run goal and source input reference
- current worktree and branch
- selected modules and statuses
- current or next module
- changed files
- commits created
- validation results
- evidence paths
- blockers, risks, and deferred decisions
- paths to detailed module reports

Update it at every module boundary before any compaction.
