# Bug Template

Bugs should capture impact, reproduction, expected behavior, and useful fix guardrails without becoming an implementation plan.

```md
# Bug: <symptom-oriented title>

## Describe the bug

<Observable symptom. Describe what the user or system sees, not the suspected cause.>

## Impact

<Who is affected, how badly, how often, and why it matters.>

## To reproduce

1. ...
2. ...
3. ...

## Expected behavior

<The behavior contract being violated.>

## Environment

- Version / commit:
- Platform / browser / OS:
- Relevant config:

## Constraints

- ...

## References

- Logs / errors:
- Related tickets:
- Screenshots / recordings:
```

Optional sections:

- `## Environment` only when version, platform, browser, OS, or config matters.
- `## Constraints` only when the fix has a real guardrail.
- `## References` only when external links or artifacts exist.

## Writing Rules

- Title starts with "Bug:" and names the symptom, not the suspected cause.
- Impact is mandatory for prioritization.
- Reproduction steps should be deterministic when possible.
- If reproduction is intermittent, state frequency and known conditions.
- Expected behavior should be concrete.
- If expected behavior is unclear, the issue may need design clarification before it can be fixed confidently.
