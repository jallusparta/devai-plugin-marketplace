# Design the project's operating workflows

Initialization produces both the knowledge and the instructions for maintaining it. Generate a concrete `llm-wiki/AGENTS.md` from the contract template, plus `operations/workflows.md` recording selected workflows, owners, triggers, inputs/outputs, current implementation status, and useful next improvements.

Use discovered project tools and existing user decisions. Do not create new skills, integrations, hooks, or schedules merely because they are possible. Recommend them with the problem they solve and distinguish proposed from actually configured behavior. Existing authorization may include their implementation; otherwise finish the knowledge setup and report the proposed next step without implying it is installed.

## Choose the smallest useful mechanism

| Need | Initial mechanism | When a separate capability helps |
|---|---|---|
| Retrieve project context | Root agent instruction pointing to the brief, indexes, and retrieval policy | A read-only query skill if retrieval becomes complex or needs a distinct access boundary |
| Submit findings after work | Inbox submission contract in project instructions | `submit` when many agents/tools need consistent capture and deduplication |
| Initialize, interview, integrate, refresh | `curate` with explicit operation and checkpoint | Keep these together while they share the same evidence and authority model |
| Check integrity and retrieval quality | Checks during curation, recording limits honestly | `audit` for independent periodic or on-demand reports; add deterministic validators for mechanical invariants |
| Check new inbox material | On-demand curator run initially; recommend an optional daily check | Scheduler invokes bounded intake curation when the user selects a supported environment |
| Human review | Session-end packet, prioritized backlog | Weekly or on-demand review if session cadence proves unsuitable |

Do not require future skills by name in generated project instructions unless they exist. Describe the executable current workflow and list missing capabilities separately. Prefer existing available skills/tools before proposing a duplicate. A schedule is a trigger for a workflow, not a new skill by itself.

## Companion skill contracts

This plugin includes `submit` and `audit`. They are independently usable skills; confirm availability in the target host before referencing them as installed capabilities. The descriptions below summarize their boundaries; their canonical SKILL.md files define execution.

**submit** is the working agent's bounded write entry point. It captures material new findings, corrections, decisions explicitly made by humans, experiment outcomes, or known gaps at task end or on request. Input is the relevant task context plus inspectable artifacts. Output is an inbox submission with ID, submitting actor/time, task/issue link, exact evidence references and source versions, scoped observations, clearly separate interpretations, suggested affected topics, and any claimed human decision with its actual record. Deduplicate retries, preserve access classification, and report the receipt/path. Do not publish claims, mark facts verified, invent transcripts, resolve conflicts, or change the curated wiki. Do not require a submission for every trivial task or reread. If original evidence is missing, explicitly submit an unsupported report for investigation. A later correction is a new linked submission.

**audit** is an independent read-only check by default. Select a bounded scope and report coverage. Check source integrity, evidence locators, link/ID consistency, current-version review validity, stale claims, unresolved contradictions, durable corrections, review backlog age, and representative retrieval against original evidence. Separate deterministic failures from semantic concerns and unavailable checks. Prioritize findings by strategic impact, consequence, and affected downstream documents. Return each finding with exact location, evidence, severity, impact, and suggested action. Do not silently rewrite sources, repair the wiki, advance verification, or approve knowledge. Saving an audit report or submitting findings to the inbox is a separate explicit output mode within the user's request; curation handles repairs. A second agent's audit remains machine review. Add deterministic validators for repeated mechanical checks, without claiming a model-only audit enforces invariants.

## Required project contract details

### Discover paths explicitly

Initialization records named knowledge-base routes in the repository's `AGENTS.md` (or its existing agent entry point), with paths relative to the repository root. For a single default knowledge base:

```text
Knowledge base: project
Scope: this software product
Root: llm-wiki/
Inbox: llm-wiki/inbox/
Contract: llm-wiki/AGENTS.md
```

These are example defaults, not permission to create an inbox during ordinary submission. Consumers, submitters, curators, and auditors read the same routing configuration and relevant contract. Resolve paths from the identified repository root, not a tool's incidental working directory, the plugin installation, or the user's home folder. Scheduled jobs receive an explicit repository working directory and knowledge-base name.

If multiple knowledge bases exist, record a name, scope, root, inbox, and contract for each. Route only when the task clearly matches one scope or explicitly names a destination. Missing or ambiguous configuration requires one concise destination question before writing; do not guess or silently create another inbox. A missing configured directory during maintenance is a condition to report, not a reason to reroute. Initialization may create the agreed directories. Preserve applicable access boundaries and resolve symlinks before writes so a path cannot silently target another collection.

Specify:

- Consumer entry point, progressive retrieval, status-aware use, and how to cite original evidence.
- Working-agent submission fields and expected task-end contribution behavior; ordinary question answering remains read-only.
- Curator ownership of shared integration; permitted factual updates versus human decisions; source preservation and conflict handling.
- Reviewer roles, packet budget, backlog priority/age, and exact approval scope.
- Source coverage, checkpoints, source-change and freshness triggers, actual validation commands, and limitations.
- Paths for each input/output and how a new session resumes.

Instructions inside `llm-wiki/AGENTS.md` may not be discovered by an agent doing work elsewhere in the repository. Add a concise pointer at the repository's agent entry point as part of authorized initialization. Preserve unrelated instructions and avoid requiring every agent to load the full knowledge base.

## Scheduling proposal

For any recommended scheduled workflow state trigger/cadence, working directory, required source access, bounded batch/time budget, no-op behavior, overlapping-run handling, failure/checkpoint behavior, output location, and human-review handoff. A daily inbox check should not refresh every source or create daily review obligations. Unanswered proposals remain pending across runs. Do not send messages to others or configure external automation without authorization.

Keep automation recommendations proportional to observed load. For a solo project, the first working version may need only the curator skill, project instructions, and inbox. Revisit when repeated friction demonstrates a useful additional skill or deterministic helper.
