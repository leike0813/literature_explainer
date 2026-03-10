# evidence-traceability Specification

## Purpose
TBD - created by syncing change refine-evidence-traceability-v1. Update Purpose after archive.

## Requirements
### Requirement: Q&A answers must include explicit evidence items
For every Q&A answer in state S3, the agent SHALL include a structured evidence array in the response, and each item SHALL contain `source_type`, `source`, `keywords`, and `claim`.

#### Scenario: Agent outputs answer with evidence array
- **WHEN** a user asks a question in the Q&A loop
- **THEN** the answer includes an explicit evidence array with all required fields for every evidence item

### Requirement: QA memory must preserve raw evidence entries
When writing `stage=qa` memory, the system SHALL store `evidence_items` as structured entries and SHALL preserve each `source` exactly as provided in the answer payload.

#### Scenario: Memory update stores unchanged evidence sources
- **WHEN** the agent updates memory after a Q&A answer
- **THEN** the saved record includes `evidence_items`
- **AND** each evidence `source` is stored in original text form without rewriting

### Requirement: Study note Q&A section must list evidence sources verbatim
When generating the study note, the `问答` section SHALL list evidence sources for each Q&A turn one by one from memory records, preserving original order and original source text.

#### Scenario: Note generation renders per-turn evidence sources
- **WHEN** the user requests study note generation
- **THEN** each Q&A block contains a per-item evidence source list from that turn
- **AND** sources are not paraphrased, compressed, or merged away

### Requirement: Post-answer operation order is fixed
For each Q&A turn, the system SHALL execute this order: answer with evidence array -> run verifier `verify` -> echo verifier result -> run memory `update` -> continue next turn.

#### Scenario: Turn completion follows deterministic sequence
- **WHEN** a Q&A answer is produced
- **THEN** verifier execution and echo happen before memory update
- **AND** the next turn does not start until memory update completes
