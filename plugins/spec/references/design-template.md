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

- `## Acceptance criteria` only when done checks are clearer than requirements.
- `## Scenario` only when one example clarifies non-obvious behavior.
- `## Constraints` only when there is a real guardrail.
- `## References` when a link or artifact is needed to understand, implement, or review the issue.

## Medium Or Large Design

Use when there are several behaviors, edge cases, platforms, systems, or high-risk assumptions.

```md
# <outcome-oriented title>

## Overview

<One short paragraph: problem, selected behavior, and scope.>

## Requirements

- The system MUST ...
- The system SHOULD ...
- The system MAY ...
```

Optional sections for medium or large design:

- `## Success metrics` only when not already captured in intent, or when the design changes the measurable outcome.
- `## Acceptance criteria` when completion checks are clearer outside requirements.
- `## Scenarios` when 1-2 examples clarify behavior, edge cases, or errors.
- `## Non-functional requirements` when performance, accessibility, security, reliability, observability, or compliance requirements materially affect product behavior.
- `## Constraints` for guardrails that narrow valid solutions.
- `## Out of scope` when scope boundaries matter.
- `## References` when links or artifacts are needed to understand, implement, or review the issue.

## Requirements Vs Acceptance Criteria

- Requirements define what the system must do.
- Acceptance criteria define how reviewers decide the issue is done.
- Omit acceptance criteria when they only repeat requirements.
- Include product-relevant testing or monitoring expectations only when they describe observable behavior, review expectations, or user/business risk.

## Writing Rules

- Use plain bullets for small issues.
- Use MUST/SHOULD/MAY for medium and large issues only when strictness matters.
- If every requirement is a MUST, remove the keyword unless it adds real prioritization signal.
- Use product-provided metrics directly. Mark inferred metrics as proposed.
- Prefer a short useful issue over a complete-looking issue.
- Keep implementation details out of the design body.
