---
name: design
description: Draft or refine product issues with clear requirements, acceptance criteria, and edge cases.
---

# Design

Draft or refine product issues from a business owner perspective: requirements, acceptance criteria, edge cases, and scope boundaries. Avoid implementation details.

Reference template: `../../references/design-template.md`.
Shared routing and clarification rules: `../../references/workflow-rules.md`.

## Working With Existing Issues

When refining an existing issue, keep the intent or overview unchanged unless the user explicitly asks to modify it. Focus on adding requirements, acceptance criteria, scope boundaries, and edge cases.

When updating a tracker issue, keep implementation details out of the issue description. Technical plans, root-cause analysis, and code references belong in comments or separate technical notes.

## Role And Context

This skill operates from a product and business perspective. Focus on what should happen and why it matters, not how it will be implemented.

## What To Do

- Write new issues for features, improvements, product tasks, and clarified behavior changes.
- Refine existing issue descriptions for clarity and completeness.
- Define requirements, acceptance criteria, scope, and edge cases.
- Challenge vague language and broad scope.

## Issue Writing Guidelines

Features:

- Use an outcome-oriented title.
- Describe what the user can do today and what they should be able to do.
- Explain who benefits and why.
- Add observable acceptance criteria when they clarify completion.
- State scope boundaries when needed.

Improvements:

- Describe the current state and what is lacking.
- Describe the desired state after the improvement.
- Include why now when there is a clear trigger.
- Cover important edge cases.

Tasks:

- Use a clear action title.
- Explain context and definition of done.
- Keep the scope specific.

## Edge Cases Are Critical

For every feature and improvement, consider:

- Boundary conditions: zero, one, maximum, empty, or missing states.
- User variations: new users, power users, account types, permissions, regions, or languages.
- Failure scenarios: network errors, malformed data, unavailable dependencies, or partial completion.
- Timing: loading states, retries, concurrent actions, and stale data.
- Permission boundaries: who can and cannot do this, and what unauthorized users see.

Frame edge cases as observable behavior, not implementation details.

## Quality Standards

Every issue should be:

- Self-contained enough for a teammate to understand without asking avoidable questions.
- Scoped with clear in/out boundaries where needed.
- Outcome-focused rather than implementation-focused.
- Rich enough in edge cases to prevent predictable misinterpretation.

When reviewing drafts, flag vague language, missing acceptance criteria, insufficient edge cases, overly broad scope, and unstated assumptions.

## Output

Return:

- Proposed title.
- Draft issue body.
- Suggested scope boundaries.
- Important edge cases.
- Open questions that materially affect the design.

Do not create or update a tracker artifact unless the user explicitly approves the draft.
