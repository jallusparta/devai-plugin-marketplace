# Design Template

Design defines behavior. It describes what the system should do, not how to implement it.

## Small Design

Use for one coherent change with a few behaviors and low ambiguity.

```md
# <outcome-oriented title>

## Overview

<One short paragraph: problem and selected behavior.>

## Requirements

- <Plain behavior requirement>
- <Plain behavior requirement>
- <Plain behavior requirement>
```

Optional sections for small design:

- `## Scenario` only when one example clarifies non-obvious behavior.
- `## Edge cases` when a boundary condition needs an explicit expected result.
- `## Constraints` only when there is a real guardrail.
- `## Out of scope` when a plausible interpretation needs to be excluded.
- `## References` directly after `## Overview` when a design, diagram, document, or other source helps people understand the issue.

## Medium Or Large Design

Use when there are several behaviors, edge cases, platforms, systems, or high-risk assumptions.

```md
# <outcome-oriented title>

## Overview

<One short paragraph: problem, selected behavior, and scope.>

## Requirements

- [ ] <Observable requirement>
- [ ] <Observable requirement>
```

Optional sections for medium or large design:

- `## Success metrics` only when not already captured in intent, or when the design changes the measurable outcome.
- `## Scenarios` when examples clarify important customer flows, behavior, edge cases, or errors.
- `## Edge cases` when boundary conditions need explicit expected results.
- `## Non-functional requirements` when performance, accessibility, security, reliability, observability, or compliance requirements materially affect product behavior.
- `## Constraints` for guardrails that narrow valid solutions.
- `## Out of scope` when scope boundaries matter.
- `## References` directly after `## Overview` when a design, diagram, document, or other source helps people understand the issue.

## Requirements And Acceptance

- Write requirements as observable checklist items that also define how reviewers decide the issue is done.
- Do not add a separate acceptance criteria section when it would repeat the requirements.
- Include product-relevant testing or monitoring expectations only when they describe observable behavior, review expectations, or user/business risk.

## Grouping

- Keep requirements in one flat list by default.
- Group requirements under descriptive behavior headings only when there are more than 12 criteria and at least three coherent groups.
- Do not create headings for groups containing only one or two criteria.

## Writing Rules

- Use plain bullets for small issues.
- Use product-provided metrics directly. Mark inferred metrics as proposed.
- Prefer a short useful issue over a complete-looking issue.
- Preserve every meaningful decision while removing repetition and filler.
- Keep implementation details out of the design body.
