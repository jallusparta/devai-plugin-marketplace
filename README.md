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

### `wiki`

Initialize and maintain an evidence-linked LLM wiki, with immutable sources, scoped verification, linked project documents, resumable intake, and compact human reviews.

- Skills: `curate`, `submit`, `audit`.
- Canonical instructions: `plugins/wiki/skills/<skill-name>/SKILL.md`.
- Repository discovery: `.agents/skills/<skill-name>` symlinks to each complete canonical skill directory.
- Includes project `AGENTS.md` generation and workflow/automation recommendations.
- Submit captures evidence-linked inbox entries; audit reports problems read-only; curate integrates changes and prepares human reviews.

`curate` handles both creation and ongoing maintenance:

- **First run:** discover sources, establish goals and structure, initialize the wiki and its operating instructions, and curate the first batch.
- **Subsequent runs:** read the configured knowledge-base location and saved checkpoint, resume unfinished ingestion, process new inbox submissions, update affected pages and relationships, and prepare a compact human review packet. It does not restart initialization when a knowledge base already exists.

`submit` adds useful findings and evidence to the configured inbox. `audit` checks existing knowledge and reports issues without modifying it; it does not ingest the inbox.

Try from an agent with the skills loaded:

```text
Use $curate to initialize this project's knowledge base.
Use $submit to capture the useful findings from this task.
Use $audit to review current goals and their supporting evidence without changing files.
```

For local Claude testing without installing or publishing:

```sh
claude --plugin-dir /absolute/path/to/devai-plugin-marketplace/plugins/wiki
```

Then invoke `/wiki:curate`, `/wiki:submit`, or `/wiki:audit`.

For selected OpenCode/Codex projects, copy the complete selected canonical skill directories into that project's `.agents/skills/`, preserving `references/`, `assets/`, and `agents/` when present. Do not copy a discovery symlink without its target. Alternatively, link directly to the absolute canonical directory on the same machine. No global installation is needed. The knowledge-base destination comes from the consuming project's instructions, not this marketplace.

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
