---
name: design
description: Draft or refine behavior-focused issues with observable requirements, customer scenarios, edge cases, and scope boundaries.
---

# Design

Draft or refine behavior-focused issues using input from product, design, engineering, domain stakeholders, and available project evidence. Define what should happen without prescribing implementation.

Reference template: `../../references/design-template.md`.
Shared routing and clarification rules: `../../references/workflow-rules.md`.

## Working With Existing Issues

When refining an existing issue, preserve any existing intent or overview verbatim unless the user explicitly asks to change it or available evidence contradicts it. If evidence conflicts with the existing text, show the conflict and ask the user whether to correct it. Otherwise, add design content after the existing intent or overview and focus on requirements, acceptance criteria, scope boundaries, and edge cases. If no intent or overview exists, add a brief Overview that states the problem and desired outcome before the design content.

When updating a tracker issue, keep implementation details out of the issue description. Technical plans, root-cause analysis, and code references belong in comments or separate technical notes.

## Role And Context

This skill defines observable behavior. Different participants may own different decisions: product owns outcomes and business rules, design owns interaction decisions, domain stakeholders own authoritative source information, and engineering contributes current-system facts and constraints. Keep implementation planning separate.

## What To Do

- Write new issues for features, improvements, product tasks, and clarified behavior changes.
- Refine existing issue descriptions for clarity and completeness.
- Define requirements, acceptance criteria, scope, and edge cases.
- Challenge vague language and broad scope.
- Recommend smaller issues when the work contains independently implementable outcomes.

## Issue Writing Guidelines

Features:

- Use an outcome-oriented title.
- Describe what the user can do today and what they should be able to do.
- Explain who benefits and why.
- Add observable acceptance criteria when they clarify completion.
- Use Given / When / Then scenarios for important customer flows and non-obvious behavior.
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
- Flow coverage: entry points, exit points, back behavior, and alternative paths.
- Data and presentation variations: relevant statuses, languages, regions, and accessibility settings.

Frame edge cases as observable behavior, not implementation details.

## Quality Standards

Every issue should be:

- Self-contained enough for a teammate to understand without asking avoidable questions.
- Scoped with clear in/out boundaries where needed.
- Outcome-focused rather than implementation-focused.
- Rich enough in edge cases to prevent predictable misinterpretation.
- As concise as possible without dropping meaningful decisions.

When reviewing drafts, flag vague language, missing acceptance criteria, insufficient edge cases, overly broad scope, and unstated assumptions.

## Output

Return:

- Proposed title.
- One integrated draft issue body containing the relevant scope boundaries and edge cases.
- Open questions that materially affect the design, without repeating content already included in the draft.

Do not create or update a tracker artifact unless the user has reviewed the complete draft and explicitly approves it.
