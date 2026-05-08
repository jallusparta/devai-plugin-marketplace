# Module Contract

A LoopKit module is a small, readable workflow unit. It can clarify requirements, plan work, implement code, run a quality gate, produce a report, create a handoff artifact, or do any other team-defined step.

Modules are deliberately plain Markdown with YAML frontmatter so teams can edit them without learning a custom framework.

## Required Frontmatter

```yaml
id: module-id
title: Human readable title
description: One sentence describing when this module should run.
type: task # task | gate | handoff | report | custom
default_enabled: false
requires: []
can_edit: false
can_commit: false
commit_policy:
  mode: inherit # inherit | never | ask | per_module | per_fix | per_task
communication:
  target: none # none | issue | pr | report | custom
  timing: never # never | final | on_failure | always
  requires_user_approval: true
outputs: []
```

## Body Structure

```markdown
## Purpose

What this module is responsible for.

## Inputs

What files, run state, tracker content, or project context the module should read.

## Procedure

The steps the agent should follow.

## Pass Criteria

How the module decides whether it succeeded.

## Outputs

What artifacts, state updates, evidence, or summaries the module must produce.

## Observability

What should be recorded in `events.jsonl`, `debug.md`, and `module-runs/<module-id>/`.

## Communication

What, if anything, should be prepared for external communication. External writes should follow the local config and user approval rules.
```

## Commit Policy Resolution

The module commit policy overrides the top-level config. If the module uses `inherit`, use `defaults.commit_policy.default`. If neither is clear, ask before committing.

## Communication Scope

Communication is owned by modules, not a separate global layer. Modules may produce handoff summaries or suggest issue/PR comments, but should not post externally unless the config permits it and approval rules are satisfied.

## Delegation Contract

The orchestrator may delegate a module or bounded module subtask to a subagent, but never the entire LoopKit run.

Delegated prompts must state:

- this is one LoopKit module or subtask, not a generic implementation request
- the module id and run id
- the module procedure and pass criteria
- relevant input and run-state summary
- allowed edits, commands, commits, and external writes
- that the subagent must not run other modules
- that the subagent must not mutate global run state unless explicitly allowed

Subagents should return structured results with:

- `status`: passed, failed, blocked, skipped, or partial
- `actions`: concise summary of work performed
- `files_changed`: files edited or inspected when relevant
- `commands_run`: commands and exit statuses
- `validation`: checks performed and results
- `evidence`: screenshots, logs, reports, or output paths
- `blockers`: unresolved blockers or missing inputs
- `commits`: commit hashes created, if any
- `risks`: residual risks or deferred findings
- `recommended_next_action`: what the orchestrator should do next

The orchestrator persists these results into module reports, events, debug notes, and the context summary.
