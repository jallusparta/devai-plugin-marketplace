# Knowledge and verification model

Use OKF v0.2 vocabulary for `wiki/`: Markdown with YAML frontmatter, a required `type`, explicit `status` (`draft`, `stable`, `deprecated`), sources with stable IDs, source-keyed footnotes, and `generated` / `verified` events. Root `index.md` may declare `okf_version: "0.2"`; indexes and logs follow the format's reserved-file conventions. Other indexes have no frontmatter. Keep operational files and raw originals outside this bundle. Relative links may resolve to evidence outside the bundle in this repository; a standalone export must include/remap those dependencies.

Reviewed format reference: https://github.com/GoogleCloudPlatform/open-knowledge-format/blob/0b87c52c6ef999286c745e19998fdfcd03d5dbee/SPEC.md

This local profile adds stricter rules. Do not imply these are OKF requirements. OKF tiers are derived from verification actors: none = unverified; non-human only = machine-confirmed; `human:<id>` present = human-reviewed. It supplies advisory signals rather than evidence quality, authenticated approval, or access enforcement. Bind local reviews to claim versions and do not project obsolete approvals onto current pages.

## Sources

Give each source a stable ID and append-only versions with hash, original resource/path, source/event date when known, capture timestamp, type, collection method, access classification, and extraction details when applicable. Preserve exact originals; put normalization in separate artifacts with mappings to original locators. A link-only record is not a captured webpage and cannot claim snapshot integrity. Record inaccessible sources as inaccessible. Preserve interview questions and exact answers separately from summaries; never fabricate a transcript from recollection.

## Claims

Start with one Markdown record per material, independently reviewable claim; shard indexes by topic as needed. Avoid a separate record for every connective sentence. Records need:

| Field | Meaning |
|---|---|
| `claim_id`, `version`, `claim_text` | Stable identity and specific assertion |
| `claim_type` | Fact, observation, hypothesis, interpretation, goal, decision, policy, heuristic, or exception |
| `scope` | Applicable time, system/version, people, conditions, and exclusions |
| `evidence` | Source ID/version, exact locator, excerpt or artifact reference, supports/qualifies/refutes |
| `generated` | Actor, time, and derivation method |
| `verification` | Unverified, machine-confirmed, or human-reviewed; method and version-bound events |
| `authority` | Pending, authorized, or not-required under agreed factual-use policy |
| `lifecycle` | Candidate, active, stale, disputed, superseded, or archived |
| `owner`, `access_class` | Accountable role and permitted audience |
| `review_due`, `review_triggers` | Risk-based date when applicable and relevant change events |
| `relationships` | Typed edges to claims, sources, concepts, and goals |

Keep verification, authority, and lifecycle distinct. A human-reviewed claim can still be stale or disputed. Page-level human review requires review of the exact page version; approval of some claims must not label the entire synthesis reviewed.

Typed edges initially include `supports`, `qualifies`, `contradicts`, `depends_on`, `supersedes`, and `derived_from`. Give each meaningful edge a rationale or supporting claim and render a readable link. Maintain a rebuildable reverse-dependency index for impact analysis. The graph is an aid to finding affected material, not evidence that a causal inference is valid. Do not add a graph database unless scale demonstrates a need.

## Machine confirmation

First draft candidates. In a distinct checking pass, inspect original evidence for actual entailment, scope, date, and qualifications. Check for relevant contrary evidence within the processed corpus and state coverage limits. Record source independence; copied reports do not count as independent corroboration. Multiple sources can help but are neither sufficient nor universally required. A primary schema or reproducible artifact may directly establish a scoped implementation fact.

Record verifier, claim version/hash, check method, evidence versions, time, outcome, and limitations. Deterministic observations and model judgments must be distinguishable. A second model reading the draft alone is insufficient. Only factual claims that pass the agreed policy can automatically become active and machine-confirmed. Research interpretations, goals, strategic choices, and policy remain pending human confirmation. Confidence scores and source counts cannot promote them.

## Current retrieval

Default current guidance uses active claims with valid verification and required authority. Unverified candidates can be inspected for exploration if clearly labeled; they cannot become settled premises. Surface relevant disputes and staleness, exclude superseded material from current answers, and use it for explicitly historical questions. Abstain from unsupported conclusions while stating what is known. Restrict access at the storage/tool boundary where needed; metadata alone cannot prevent confidential source leakage, including through indexes and excerpts.
