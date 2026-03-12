## ADDED Requirements

### Requirement: Dispatcher must derive a stable paper key
The system SHALL derive a stable `paper_key` from `input_hash`, and dispatcher outputs SHALL be isolated under a paper-specific subdirectory.

#### Scenario: Dispatcher normalizes one paper into a unique subdirectory
- **WHEN** the dispatcher reads one source file
- **THEN** it computes `input_hash`
- **AND** derives a stable `paper_key`
- **AND** writes `source.md` and `source_meta.json` under a `<tmp>/<paper_key>/` subdirectory

### Requirement: Memory persistence must be isolated per paper
The memory engine SHALL persist each paper into its own memory file instead of a single shared JSONL file.

#### Scenario: Two papers in one working directory stay isolated
- **GIVEN** two different paper inputs are processed in the same working directory
- **WHEN** their memory records are written
- **THEN** each paper writes to a different memory file
- **AND** records do not mix across papers by default

### Requirement: Note content must not be written back to memory
Within a paper's memory file, note snapshots SHALL NOT be stored as memory records; memory remains limited to initial-analysis and QA records.

#### Scenario: Regenerating note does not change memory stages
- **GIVEN** a paper has initial-analysis and QA memory records
- **WHEN** the agent generates or regenerates a note for that paper
- **THEN** no `stage=note` memory record is written
- **AND** memory stage set remains constrained to analysis and QA

### Requirement: Note file must be unique per paper
The final study note file SHALL use a paper-specific filename and SHALL be overwritten on regeneration for the same paper.

#### Scenario: Repeated note generation updates one paper-specific file
- **GIVEN** the agent has already written a note file for one paper
- **WHEN** note generation runs again for that same paper
- **THEN** it writes to the same paper-specific path
- **AND** no second note file is created for that paper

### Requirement: Note source scope must reuse paper-global analysis and session-local QA
When generating a note, the system SHALL use initial-analysis records across the active paper and SHALL use QA records only from the current session.

#### Scenario: Note generation reuses analysis but limits QA to current session
- **GIVEN** one paper has records from multiple sessions
- **WHEN** the current session generates a note
- **THEN** paper-level initial-analysis records remain available
- **AND** QA records are limited to the current `session_key`
