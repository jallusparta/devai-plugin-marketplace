# Spec Plugin

Lightweight specification skills for turning rough ideas, product requests, and bugs into clear team-readable artifacts.

The plugin keeps the workflow intentionally small:

- `/spec:intent` - clarify the problem, business context, desired outcome, and success signal.
- `/spec:design` - define product behavior, requirements, acceptance criteria, edge cases, and constraints.
- `/spec:bug` - capture bug impact, reproduction, expected behavior, environment, and useful fix guardrails.

## Workflow

Default flow:

```text
intent -> design
```

Bugs use `/spec:bug` directly. If the input describes an existing flow showing broken, regressed, raw-key, untranslated, or otherwise unexpected behavior, use `/spec:bug` before intent or design.

## How To Use

Start with the smallest useful command:

```text
/spec:intent <raw idea, customer problem, issue link, or product request>
```

Use `/spec:design` when the problem and direction are clear enough to define behavior:

```text
/spec:design <intent, issue link, Figma link, or product notes>
```

Use `/spec:bug` for defects:

```text
/spec:bug <symptom, issue link, logs, screenshot context, or reproduction notes>
```

## Output Style

- Keep small issues short.
- Ask clarifying questions when the missing answer changes the output.
- Do not force a long template when a short draft is enough.
- Include references only when they are needed to understand, implement, or review the issue.
- Keep implementation details out of intent and design.
- Keep root-cause analysis out of bug reports unless the user explicitly asks for technical notes.

## References

The durable templates live in [references/](references/). They define the expected shape for intent, design, and bug reports.
