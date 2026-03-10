## ADDED Requirements

### Requirement: Study note generation must be optional
The system SHALL treat study-note generation as an explicit optional action, and the user SHALL be able to end the skill without generating notes.

#### Scenario: User declines note generation
- **WHEN** the agent reaches the point where note generation is available
- **THEN** the user may decline note generation
- **AND** the skill proceeds to completion without entering note generation

### Requirement: Study note structure must be fixed and Q&A-centered
When a study note is generated, it SHALL use a fixed structure centered on Q&A records, with sections for `论文摘要`, `问答摘要`, `未解决问题`, and `后续行动`.

#### Scenario: Generated note uses fixed high-level structure
- **WHEN** the user requests note generation
- **THEN** the note contains the fixed sections in deterministic order
- **AND** `问答摘要` is the core section of the document

### Requirement: Paper summary must be one expanded paragraph
The `论文摘要` section SHALL be a single expanded paragraph based on the paper abstract and the agent's overall understanding, and SHALL NOT expand into multi-section paper recaps.

#### Scenario: Paper summary remains concise
- **WHEN** the note is generated
- **THEN** the paper-level summary is rendered as one paragraph
- **AND** the note does not include large chapter-by-chapter paper summaries

### Requirement: Note generation must use structured memory only and write back final note
The note generation step SHALL use only structured records returned by `memory_engine read`, and after generating the final Markdown note it SHALL write back one `stage=note` record.

#### Scenario: Final note is generated from memory and persisted
- **WHEN** note generation runs
- **THEN** the agent consumes structured memory fields without relying on raw answer text
- **AND** the final Markdown note is persisted through `update` with `stage=note`

### Requirement: Each Q&A block must use a fixed four-part structure
Within `问答摘要`, each Q&A block SHALL contain `用户问题`, `回答要点`, `证据原文`, and `未解决点/后续动作`.

#### Scenario: Q&A block layout is deterministic
- **WHEN** a note includes one or more Q&A turns
- **THEN** each turn is rendered with the same four-part layout
- **AND** evidence sources are listed verbatim from memory
