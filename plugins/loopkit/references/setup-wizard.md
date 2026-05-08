# Setup Wizard

The setup wizard creates or updates a local LoopKit config. Keep it short by default and offer advanced customization only when useful.

## Quick Setup Questions

Ask only what is needed to create a usable config:

1. State directory: default `.loopkit`.
2. Tracker or external system: `none`, `gitlab`, `github`, `jira`, `linear`, or `custom`.
3. External writes: `never`, `ask`, or `allowed`.
4. Default commit policy: `never`, `ask`, `per_module`, `per_fix`, or `per_task`.
5. Default preset: `none` or a user-defined preset.
6. Whether to create an initial module now.

## Defaults

Recommended universal defaults:

```yaml
state_dir: .loopkit
defaults:
  preset: none
  external_writes: ask
  commit_policy:
    default: ask
modules: []
presets: {}
tracker:
  type: none
  external_writes: ask
commands: {}
```

## Advanced Setup

Only ask advanced questions when the user requests them or when a selected module requires the answer.

Advanced topics:

- branch or worktree strategy
- standard lint/test/build commands
- external tracker conventions
- required approval points
- evidence retention
- custom module locations
- team-specific reporting expectations

## Local Only

Runtime state should normally be local and gitignored. Do not commit `.loopkit/runs/` unless the user explicitly wants to share run state.
