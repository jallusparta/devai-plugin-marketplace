# Devai Plugin Marketplace

Local marketplace for reusable AI workflow plugins and skills.

This repository is intentionally tool-neutral where possible:

- Claude Code installs plugins from `.claude-plugin/marketplace.json`.
- OpenCode and Codex can load Agent Skills from `.agents/skills/<name>/SKILL.md`.
- Canonical plugin content lives under `plugins/<plugin-name>/`.

## Included Plugins

### `loopkit`

Configurable local workflow loops for AI coding agents.

Claude Code commands:

- `/loopkit:setup`
- `/loopkit:run`
- `/loopkit:module`
- `/loopkit:status`
- `/loopkit:debug`

OpenCode/Codex skills:

- `loopkit-setup`
- `loopkit-run`
- `loopkit-module`
- `loopkit-status`
- `loopkit-debug`

### `spec`

Lightweight intent, design, and bug specification skills for product and engineering teams.

Claude Code commands:

- `/spec:intent`
- `/spec:design`
- `/spec:bug`

OpenCode/Codex skills:

- `spec-intent`
- `spec-design`
- `spec-bug`

## Claude Code Local Install

From Claude Code:

```text
/plugin marketplace add https://github.com/jallusparta/devai-plugin-marketplace
/plugin install loopkit@devai-plugin-marketplace
/plugin install spec@devai-plugin-marketplace
```

For validation:

```sh
claude plugin validate https://github.com/jallusparta/devai-plugin-marketplace
```

## OpenCode / Codex Local Use

Point the agent at this repository or copy/symlink `.agents/skills/loopkit-*` and `.agents/skills/spec-*` into a project or global skills directory.

The adapter skills are thin wrappers. The canonical instructions remain in each plugin's `skills` directory and shared references remain in each plugin's `references` directory.

## Publishing Notes

If publishing to a public skill index such as skills.sh, publish the `.agents/skills/*` adapter skills and keep links back to this repository. Keep Claude Code distribution through the native plugin marketplace because it preserves namespaced slash commands and plugin metadata.
