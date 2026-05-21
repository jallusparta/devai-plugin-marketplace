---
name: intent
description: Draft or improve a light intent brief for an issue, project, or existing tracker comment.
---

# Intent

Use this when the user wants to clarify why work matters before product requirements or implementation details are defined.

## Business Focus Only

Intent frames the problem and desired outcome. It does not define technical implementation.

- Do include the problem, who is affected, why it matters, desired outcome, and success signals.
- Do not include APIs, service names, database concerns, technical feasibility, or implementation approach.

Reference template: `../../references/intent-template.md`.
Shared routing and clarification rules: `../../references/workflow-rules.md`.

## Triage First

Stop and ask the user if the input looks like broken behavior. Intent frames new opportunities or unclear problems. If this is a defect, `/spec:bug` may be a better fit.

Bug signals include raw translation keys shown to users, missing localization, regression, crash, error, existing flow not behaving as intended, or an edge case handled inconsistently.

## Workflow

1. Confirm this is not a bug. If the user insists on intent for a bug-adjacent item, keep it as impact/context and suggest `/spec:bug` for the actual tracker body.
2. Investigate available context first. If starting from an issue, ticket, or document, read the description, comments, and attachments the user provides or authorizes. If working in a codebase, search for related screens, flows, and components so the intent reflects current behavior.
3. Ask for the success signal and time sensitivity when they are not already clear.
4. Decide the artifact target: standalone issue, larger project/epic, or comment/update for an existing artifact.
5. Choose the format based on scope. Use the short format for most issues and the extended format only when scope spans multiple flows, teams, platforms, or releases.
6. Do not write requirements, acceptance criteria, or implementation tasks in the intent stage.
7. Ask only for missing information that blocks a meaningful intent. Prefer drafting with explicit assumptions over over-interviewing.
8. If a metric comes from product/user input, use it directly. If you invent or infer a metric, label it as proposed.

## Brevity Rules

- Small to medium issues: Overview plus success signal. No extra sections unless truly needed.
- Large issues, epics, or projects: 8-15 lines total with problem, business context, desired outcome, and success signals.
- Cut anything that belongs in design or technical planning.

## Output

Return:

- Proposed title.
- Target artifact: standalone issue, larger project/epic, or existing artifact comment.
- Draft body.
- Open questions limited to business, scope, priority, and success criteria.

Do not create or update a tracker artifact unless the user explicitly asks you to do so after reviewing the draft.
