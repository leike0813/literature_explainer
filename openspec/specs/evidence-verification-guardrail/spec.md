# evidence-verification-guardrail Specification

## Purpose
TBD - created by syncing change add-evidence-verification-guardrail-v1. Update Purpose after archive.

## Requirements
### Requirement: Q&A evidence payload requirement
For every Q&A answer, the agent MUST provide a structured evidence array where each item includes `source_type`, `source`, `keywords`, and `claim`, and every source MUST be verifiable.

#### Scenario: Agent emits structured evidence payload after Q&A
- **WHEN** a Q&A answer is produced
- **THEN** the answer includes a JSON evidence array with required fields for each evidence item

### Requirement: Post-answer script verification and mandatory echo
After every Q&A answer, the agent MUST execute the evidence verifier script in `verify` mode and MUST echo the script result in the current session.

#### Scenario: Verification result is echoed in-session
- **WHEN** script verification completes
- **THEN** the agent echoes the verifier verdict and summary details before proceeding

### Requirement: Hallucination failure handling
If verification result is `fail`, the system SHALL treat it as hallucination and SHALL enforce both directives: (1) instruct agent to answer with deterministic facts only in subsequent turns, and (2) force user-facing warning text `刚才的证据中可能存在虚假证据，请注意。`.

#### Scenario: Failed verification triggers hallucination directives
- **WHEN** verifier returns verdict `fail`
- **THEN** the agent outputs corrective directive and the fixed warning sentence in the same session

### Requirement: Uncertain verification handling
If verification result is `uncertain`, the system SHALL NOT label the turn as hallucination, but the agent MUST explicitly echo uncertainty in the current session.

#### Scenario: Uncertain verification is disclosed without hallucination label
- **WHEN** verifier returns verdict `uncertain`
- **THEN** the agent informs the user that evidence could not be fully verified and avoids hallucination warning text

### Requirement: Source validation backend and keyword matching rules
Verifier SHALL validate `web_url` sources by fetching page content and checking that at least one provided keyword matches; verifier SHALL validate `reference_title` sources via Crossref, arXiv, or Semantic Scholar where any positive match passes.

#### Scenario: Web source validation fails on reachable page without keyword hits
- **WHEN** a URL is reachable but none of its keywords are found in page text
- **THEN** that evidence item is marked `fail`

#### Scenario: Reference title passes when any backend confirms existence
- **WHEN** Crossref, arXiv, or Semantic Scholar returns a high-confidence title match
- **THEN** that evidence item is marked `pass`

### Requirement: Evidence types MUST distinguish internal and external evidence
The evidence verification script SHALL support the following evidence types:

| source_type | Type Category | Verification Method |
|-------------|---------------|---------------------|
| `paper_text` | Internal | Skip verification (`skipped`) |
| `web_url` | External | Fetch web page, verify keyword match |
| `reference_title` | External | Query Crossref/arXiv/Semantic Scholar |

#### Scenario: Verifier correctly handles three evidence types
- **WHEN** the verifier receives a `paper_text` evidence item
- **THEN** the item status is marked as `skipped` without network verification
- **AND** the `skipped` status does not affect the final `pass/fail/uncertain` verdict

### Requirement: Verdict determination logic MUST exclude skipped items
Final verdict determination SHALL follow:
- `pass`: All evidence items requiring verification pass (no `fail` items)
- `fail`: At least one evidence item requiring verification explicitly fails
- `uncertain`: No `fail` but at least one evidence item requiring verification cannot be determined due to network/backend issues

**Note**: `skipped` items do not participate in any of the above determinations.

#### Scenario: Verification passes when only paper_text evidence is present
- **WHEN** all evidence in a turn is of `paper_text` type
- **THEN** the verdict is `pass` (no items requiring verification, defaults to pass)

### Requirement: SKILL.md MUST clarify distinction between internal and external evidence
`SKILL.md` SHALL clarify in the evidence answer rules:
- Paper text evidence (`paper_text`) is internal evidence, exempt from network verification
- External evidence (`web_url`, `reference_title`) requires network verification
- When calling `verify`, all evidence may be passed (verifier automatically skips `paper_text`), or only external evidence may be passed

#### Scenario: Agent follows correct verification workflow
- **WHEN** the Agent completes a Q&A answer
- **THEN** the Agent may pass all evidence to the `verify` script; the verifier automatically skips `paper_text` types

### Requirement: memory_engine MUST allow paper_text evidence type
`memory_engine.py` SHALL allow `paper_text` as a valid `source_type` value during `evidence_items` validation for the `qa` stage.

#### Scenario: Writing memory accepts paper_text evidence
- **WHEN** the Agent calls `memory_engine.py --mode update` to write a QA record containing `paper_text` evidence
- **THEN** validation passes and the record is successfully written
