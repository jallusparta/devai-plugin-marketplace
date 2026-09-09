# Workflow Rules

Shared routing and clarification rules for the spec plugin.

## Tracker And Repository Context

Use the tracker, repository, and collaboration tools available in the current project. Do not assume a specific tracker unless the user or repository clearly indicates one.

Before drafting any artifact:

- Read the provided issue, document, screenshot, logs, or notes.
- Use all relevant available inputs, including issue comments, code, documentation, designs, screenshots, analytics, and prior decisions.
- Inspect relevant code and documentation when current behavior, constraints, or existing terminology matter.
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

Use this investigation to answer factual questions before asking the user. Clearly distinguish verified facts, user decisions, and assumptions that remain unverified.

## Language And Terminology

Apply these rules to both clarification questions and tracker content:

- Follow any language, tone, and terminology defined in repository or project instructions.
- Reuse established terms found in issues, documentation, designs, the product interface, and other relevant context. Do not introduce synonyms for established concepts without a reason.
- When no project-specific guidance exists, use concise technical language appropriate for a reader with basic technical knowledge. Do not explain established technical terms unless the user asks.
- When writing in English, follow practical ASD-STE100 Simplified Technical English principles: prefer active voice, short direct sentences, one point per sentence, and consistent terms with one meaning. Do not claim formal ASD-STE100 compliance or restrict writing to its controlled dictionary.
- Write questions so that a person with basic technical knowledge can understand what is being decided and why it matters.

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

Each stage should ask for user input when a missing decision would materially change the artifact.

For larger or ambiguous work, clarify in rounds. Ask the questions that can be answered with the current information, then use those answers to identify the next material questions. Continue until no unresolved question would materially change the artifact at the current stage.

Good clarification questions are:

- Specific.
- Limited to decisions that affect the output.
- Grouped into one short round when possible for small or straightforward issues.
- Phrased with clear options when options are known.

Avoid open-ended interviews and questions whose answers can be found from available sources. If a missing detail is minor, draft with an explicit assumption instead.

## Concision And Final Review

- Preserve every meaningful decision, but remove repetition and filler.
- If an artifact becomes difficult to read or contains independently implementable outcomes, recommend splitting it into smaller issues.
- Before creating or updating a tracker artifact, ask the user to review the complete draft as the source of truth for the next stage and confirm or correct any remaining assumptions.

## Stage-Specific Clarification Focus

- Intent: problem owner, business context, artifact target, success signal.
- Design: scope, expected behavior, edge cases, acceptance, essential references.
- Bug: symptom, impact, reproduction, expected behavior, affected environment.
