# DevAI Plugin Marketplace

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

## Claude Code Local Install

From Claude Code:

```text
/plugin marketplace add /Users/apartanen/Development/devai-plugin-marketplace
/plugin install loopkit@devai-plugin-marketplace
```

For validation:

```sh
claude plugin validate /Users/apartanen/Development/devai-plugin-marketplace
```

## OpenCode / Codex Local Use

Point the agent at this repository or copy/symlink `.agents/skills/loopkit-*` into a project or global skills directory.

The adapter skills are thin wrappers. The canonical instructions remain in `plugins/loopkit/skills` and shared references remain in `plugins/loopkit/references`.

## Publishing Notes

If publishing to a public skill index such as skills.sh, publish the `.agents/skills/loopkit-*` adapter skills and keep links back to this repository. Keep Claude Code distribution through the native plugin marketplace because it preserves namespaced slash commands and plugin metadata.
