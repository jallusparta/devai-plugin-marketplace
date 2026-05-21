# Intent Template

Intent clarifies why the work matters. It does not define detailed requirements or implementation.

## Small Or Medium Issue Intent

Use for one coherent problem with limited scope.

```md
# <outcome-oriented title>

## Overview

<2-3 sentences: the problem, why it matters, desired outcome. No bullets.>

## Success signal

<One line: the observable outcome or metric that tells us this worked.>
```

That is enough for most issues.

## Large Issue / Epic / Project Intent

Use for larger work that spans multiple flows, teams, platforms, or releases.

```md
# <outcome-oriented title>

## Intent

**Problem**: <Who has what problem, in what context?>

**Business context**: <Why this matters now. Priority signal, opportunity, customer pain, risk, or strategic connection.>

**Desired outcome**: <What should be better after this work?>

## Success signals

- <Metric or observable signal>
```

Optional sections for large intent:

- `## Scope` when boundaries are needed for prioritization.
- `## Open questions` when decisions block design.
- `## Candidate issue breakdown` when obvious child issues are already known.
- `## References` only for essential source artifacts.

## Writing Rules

- Prefer an issue intent unless larger scope is clearly needed.
- Keep the language understandable for business, product, design, and technical readers.
- Name the problem before the solution.
- Include one success signal, even if qualitative.
- Use product-provided metrics directly. Mark inferred metrics as proposed.
- Do not include tasks, file paths, classes, implementation phases, or detailed acceptance criteria.
- If the output feels complete enough to implement from, it is too detailed for intent.
