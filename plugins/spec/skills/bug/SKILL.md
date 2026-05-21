---
name: bug
description: Draft a high-signal bug report with impact, reproduction, expected behavior, environment, and fix constraints.
---

# Bug

Use this to draft a bug report that helps triage, reproduce, and fix the issue.

Reference template: `../../references/bug-template.md`.
Shared routing and clarification rules: `../../references/workflow-rules.md`.

## Workflow

1. Investigate available context first. If starting from an issue, ticket, logs, screenshot, recording, or codebase, read the relevant context before asking questions.
2. Capture the observable symptom, not a suspected internal cause.
3. Ask clarifying questions only for things you cannot determine from the provided context or code.
4. Capture impact: who is affected, severity, frequency, and business/customer effect.
5. Capture deterministic reproduction steps when possible. If reproduction is flaky, state the frequency and known conditions.
6. Capture expected behavior as the violated contract.
7. Include environment only when relevant.
8. Include constraints only when the fix has real guardrails.
9. References are for external artifacts such as logs, screenshots, recordings, related issues, or pull/merge requests. Avoid code paths, line numbers, root-cause analysis, or internal implementation details in the bug report body unless the user asks for technical notes.
10. If a duplicate issue is suspected, ask before marking it as duplicate or commenting with a canonical issue link.

## Updating Existing Issues

When editing an existing tracker issue rather than creating a new one:

- Put user-facing problem, impact, reproduction, and expected behavior in the issue body.
- Put technical analysis, root cause, code references, and implementation notes in comments or separate technical notes.
- Ask before changing labels, duplicates, issue state, or ownership.

Do not create or update a tracker artifact unless the user explicitly approves the draft.
