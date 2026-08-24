# Adapter Notes

LoopKit is packaged as a Claude Code plugin first, but its core instructions use the Agent Skills pattern so they can be adapted to other tools.

## Claude Code

Claude Code uses this plugin through the marketplace. Skills are invoked as namespaced commands:

```text
/loopkit:setup
/loopkit:run
/loopkit:module
/loopkit:status
/loopkit:debug
```

Claude Code also loads the `loopkit-module` and `loopkit-gate` agents from `agents/`, and renders the host task list, so both progress surfaces in `progress-display.md` are available.

## OpenCode

OpenCode can load compatible skills from:

- `.opencode/skills/<name>/SKILL.md`
- `.claude/skills/<name>/SKILL.md`
- `.agents/skills/<name>/SKILL.md`
- matching global skill folders

OpenCode requires `name` and `description` frontmatter. Unknown fields are ignored. To adapt LoopKit, copy or symlink individual skill folders and keep the references with them.

OpenCode V2 configuration uses an array of skill sources and an `agents` map:

```json
{
  "skills": ["/path/to/.agents/skills"],
  "agents": {
    "loopkit-module": { "mode": "subagent" },
    "loopkit-gate": { "mode": "subagent" }
  }
}
```

The Claude plugin's `agents/` directory is not discovered by OpenCode automatically. Register equivalent agents in the project or global OpenCode configuration, and give them the bounded-module instructions from `agents/loopkit-module.md` and `agents/loopkit-gate.md`.

## Codex

Codex can load skills from `.agents/skills/<name>/SKILL.md` or user/admin skill folders. It also supports plugin packaging.

To adapt LoopKit, copy or symlink the skill folders into `.agents/skills` and keep references reachable from the skill directory.

## Interaction Differences

When a tool supports multi-select questions, use native multi-select for module selection. Otherwise ask the user to reply with comma-separated module IDs.

When a tool lacks a direct subagent API, execute modules serially and preserve the same state and observability files. The LoopKit agent types are then unavailable, so keep the module-named labels in the run output instead.

Per-module `agent`, `model`, and `isolation` settings are host-specific. Pass model names through unchanged, and ignore any of the three that the host tool cannot honor. A config written for one tool must still run on another, so `inherit` is always the safe default.

OpenCode V2 currently has no TaskCreate/TodoWrite-style task-list API. Use the module-selection flow from `run-selection.md`, keep the task mirror in `modules.yml`, and replace the host task-list UI with the short module progress line described in `progress-display.md`.
