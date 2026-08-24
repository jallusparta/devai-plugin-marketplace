---
name: module
description: Create, edit, review, or explain a LoopKit module for a local workflow loop.
---

# LoopKit Module

Use this skill when the user wants to add a new workflow phase, quality gate, handoff step, report, or any other reusable module to a LoopKit configuration.

Reference files:

- `../../references/module-contract.md` for required module shape.
- `../../references/state.md` for where modules are referenced from config.
- `../../references/observability.md` for module logging expectations.

## Workflow

1. Determine whether the user wants to create, edit, review, or explain a module.
2. Locate the target LoopKit config.
3. For creation, ask only the missing essentials:
   - module purpose
   - module type
   - whether it may edit files
   - whether it may commit
   - commit policy override, if any
   - whether it produces external communication
   - pass criteria
   - agent, model, or isolation overrides, only if the user brings them up or the module clearly needs a different execution profile
4. Draft the module as a small Markdown file using `module-contract.md`.
5. Keep module instructions plain and tool-portable.
6. Update config module references only when the user wants the module enabled or registered.

## Design Rules

- Keep modules narrow.
- Leave `agent`, `model`, and `isolation` unset unless the module has a real reason to differ. Defaults keep modules portable across tools.
- Do not encode organization-specific assumptions unless the user wants them.
- Put communication expectations inside the module only when the module produces a handoff artifact or external update.
- Put observability requirements in the module so debug output is consistent.

## Output

Return:

- module id and title
- file path
- default enabled status
- edit/commit permissions
- communication behavior
- any open questions
