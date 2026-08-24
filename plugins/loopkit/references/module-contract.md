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

## Optional Execution Frontmatter

A module may declare how it should be executed. All fields are optional and default to `inherit`.

```yaml
agent: inherit # inherit | loopkit-module | loopkit-gate | any agent type registered in the host tool
model: inherit # inherit | a model name the host tool accepts
isolation: none # none | worktree
```

Use these when a module has a genuinely different execution need, for example a cheap fast model for a mechanical gate, a stronger model for design or review work, or worktree isolation for a module that rewrites many files. Leave them out otherwise. `inherit` is the portable default and keeps the module working in tools that expose no model or agent selection.

## Execution Resolution

Resolve `agent`, `model`, and `isolation` for each module in this order, first match wins:

1. An explicit run-time instruction from the user for this run or this module.
2. The module frontmatter.
3. `defaults.execution` in the LoopKit config.
4. Built-in defaults: `loopkit-gate` for `type: gate`, `loopkit-module` for every other type; the host session model; no isolation.

Rules:

- Model names are host-specific. Treat them as opaque strings, pass them through unchanged, and never rewrite one model name into another.
- If a configured agent type is not registered in the host tool, fall back to the built-in default, warn the user once, and continue. Never fail a run over a missing agent type.
- If the host tool cannot select a model or agent per delegation, ignore these fields and run the module normally.
- Record the resolved agent, model, and isolation in the `delegated` event so a run can be explained afterwards.
- `isolation: worktree` costs setup time and disk. Use it only for modules that would otherwise conflict with parallel work.

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

Delegate using the agent, model, and isolation resolved above, so the delegation is visible and self-explaining in the host UI. With no configuration, that resolves to:

- `loopkit-gate` for modules with `type: gate`
- `loopkit-module` for `task`, `handoff`, `report`, and `custom` modules

Label every delegation `<module-id>: <short action>`, for example `lint: run eslint and fix violations`. Retries reuse the label with an attempt suffix. See `progress-display.md`.

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
