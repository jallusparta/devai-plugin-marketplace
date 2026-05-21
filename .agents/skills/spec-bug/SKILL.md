---
name: spec-bug
description: Draft a high-signal bug report with impact, reproduction, expected behavior, environment, and fix constraints.
compatibility: opencode,codex
---

# Spec Bug

Use this skill when the user wants to capture a defect with impact, reproduction, expected behavior, environment, and useful fix guardrails.

Load and follow the canonical instructions in `../../../plugins/spec/skills/bug/SKILL.md`.

Keep shared references reachable from `../../../plugins/spec/references/`, especially:

- `bug-template.md`
- `workflow-rules.md`

When the host tool does not support namespaced slash commands, treat `spec-bug` as equivalent to `/spec:bug`.
