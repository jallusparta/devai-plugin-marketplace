# Initialize or resume

## Discover before asking

Read the project instructions, current brief and relevant indexes, and checkpoint. Do not load the entire existing wiki. Establish which source collections are in scope before reading unrelated accounts or vaults. Inventory names, types, approximate volume, date range, access limits, and likely topics; inventorying a file does not mean its contents were processed.

Infer what the existing material answers and present it for correction. Ask in small rounds about unresolved high-impact inputs:

- Purpose, intended agents and humans, decisions/tasks to support, goals, success measures, and excluded uses.
- Project stage, target users, customer problems, market, experiments, and constraints.
- Solo owner or team; topic owners, source experts, challengers, and who can authorize decisions. One person can hold several separately recorded roles.
- Sources and topic coverage: repository and schemas, earlier wikis, documentation sites, GitHub issues/ADRs, research exports, analytics, support records, meeting notes, interviews, and previous agent sessions. Suggest relevant possibilities without assuming access or blanket ingestion permission.
- Knowledge location, privacy boundaries, language, review budget, machine-confirmation policy, and maintenance triggers. Keep execution in the existing issue tracker; link goals and rationale to work items.

Challenge unsupported business assumptions through concrete questions about users, value, evidence, and success. Offer to skip this discovery mode; unanswered strategy stays unknown, not agent-invented. Avoid asking all inputs upfront if existing sources can answer them.

## Establish the first edition

Propose a structure and scoped initial source batch. For a small corpus, inspect all relevant sources; for a large corpus, inventory first and sample across topic, recency, authority, and disagreement. Prioritize sources connected to current goals. Record sampled, processed, inaccessible, deferred, and failed sources separately. Sampling must not imply complete coverage.

The usual structure is:

```text
llm-wiki/
  AGENTS.md
  inbox/
  sources/
  claims/
  wiki/
    index.md
    project-brief.md
    product/
    engineering/
    decisions/
  reviews/
  operations/
```

`wiki/` is the OKF document bundle; raw sources and operational artifacts sit outside its conformance boundary. Use UTF-8 Markdown and ordinary relative Markdown links for Obsidian and other tools. Preserve legacy wikilinks in immutable originals. Avoid duplicate curated basenames and record aliases/mappings for renamed concepts.

Create documents where evidence supports them: purpose and verified goals; customers and market; hypotheses and experiments; architecture and current implementation; domain model/ERD; technical ADRs and business decisions. An ERD may describe a conceptual domain when no database exists, but must say so. Do not invent architecture, decision history, or market validation to fill a template. Keep proposed future behavior separate from observed code and verified deployed behavior.

The brief should usually fit roughly 500–800 words: purpose, current goals, constraints, key decisions, strategic uncertainty, and links. Topic indexes route to detail without loading the whole corpus. Use stable typed relationships from the knowledge model to connect goals, decisions, assumptions, and evidence.

## Migration

When asked to move a vault, first inventory files, attachments, configuration, links, and size. Prepare a copy in the target, compare content hashes and counts, and verify attachment and note resolution before removing or retiring the original. Keep raw hierarchy and original bytes as an import snapshot. Separate Obsidian UI state from evidence; avoid versioning workspace state or secrets. Account for where Obsidian opens the relocated vault. Deleting the old copy requires the requested move scope and filesystem authority; do not silently stop at a copy while reporting a move.

## Checkpoint and acceptance

Save `operations/checkpoint.md` with scope, completed batches, source IDs/versions processed, next batch, unresolved questions, reviewer decisions, deferred items, and reproducible checks. Reuse source hashes and submission IDs to resume without duplicate claims or review packets.

The first edition is ready when the owner has reviewed the structure and the specifically presented knowledge, the brief links to relevant evidence, unknowns and conflicts are visible, and maintenance can resume. Record approval scope precisely. If practical, ask a fresh agent to perform a representative read-only project task from the entry point and report missing context or unsupported answers. This supplements the owner's acceptance; it does not replace it.
