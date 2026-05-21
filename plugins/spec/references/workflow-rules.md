# Workflow Rules

Shared routing and clarification rules for the spec plugin.

## Tracker And Repository Context

Use the tracker, repository, and collaboration tools available in the current project. Do not assume a specific tracker unless the user or repository clearly indicates one.

Before drafting any artifact:

- Read the provided issue, document, screenshot, logs, or notes.
- Inspect relevant code when the user asks for repository-aware output or when current behavior matters.
- Ask before creating issues, updating descriptions, posting comments, changing labels, or marking duplicates.
- Do not pull, rebase, change branches, or update remote tracker state silently.

## Issue Content Placement

Keep tracker content in the right place:

- Issue description: intent, design, and bug-report content that explains the user-facing problem, desired behavior, scope, and acceptance.
- Issue comment or technical note: context findings, root-cause notes, implementation analysis, and implementation plans.
- Draft first, then ask before creating or updating a tracker artifact.

## Investigate Current Behavior First

Before drafting or asking clarifying questions, inspect available context to understand current behavior.

When starting from an issue or ticket:

- Read the full description and relevant comments.
- Review screenshots, recordings, logs, or attachments when available.
- Check for reproduction steps, environment details, and prior clarifications.

When using codebase context:

- Search for relevant screens, components, API calls, copy, and flows.
- Read the actual implementation enough to understand current behavior.
- Check translations, error handling, and edge cases when relevant.

Use this investigation to answer your own questions before asking the user.

## Route Bugs Before Intent Or Design

Recommend `/spec:bug` before `/spec:intent` or `/spec:design` when the user describes an existing flow violating its intended behavior.

Common bug signals:

- Raw translation keys shown to users.
- Missing localization or fallback copy.
- Regression from previous behavior.
- Unexpected error, crash, or broken state.
- Existing CTA, form, API, notification, or screen does not behave as intended.
- Known edge case handled inconsistently across paths.

## Ask Clarifying Questions

Each stage should ask for user input when a missing answer would materially change the artifact.

Good clarification questions are:

- Specific.
- Limited to decisions that affect the output.
- Grouped into one short round when possible.
- Phrased with clear options when options are known.

Avoid open-ended interviews. If the missing detail is minor, draft with an explicit assumption instead.

## Stage-Specific Clarification Focus

- Intent: problem owner, business context, artifact target, success signal.
- Design: scope, expected behavior, edge cases, acceptance, essential references.
- Bug: symptom, impact, reproduction, expected behavior, affected environment.
