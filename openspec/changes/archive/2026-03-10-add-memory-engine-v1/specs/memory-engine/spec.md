## ADDED Requirements

### Requirement: Memory update triggers for analysis and Q&A turns
The system SHALL update memory exactly at two points: once after initial paper analysis and once after each completed Q&A turn.

#### Scenario: Initial analysis update is recorded
- **WHEN** the agent finishes the first paper-level analysis summary
- **THEN** it invokes memory update mode and appends one structured memory entry

#### Scenario: Q&A turn update is recorded
- **WHEN** the agent completes a Q&A response turn
- **THEN** it invokes memory update mode and appends one structured memory entry for that turn

### Requirement: Three-mode script contract
The memory engine SHALL expose three CLI modes: `instructions`, `update`, and `read`, where `instructions` returns structured JSON guidance, `update` persists memory, and `read` returns raw memory entries only.

#### Scenario: Instructions mode returns structured guidance
- **WHEN** the script is called with mode `instructions` and a valid stage
- **THEN** it outputs JSON containing `stage`, `required_fields`, `summary_rules`, and `update_constraints`

#### Scenario: Read mode returns raw entries
- **WHEN** the script is called with mode `read`
- **THEN** it returns original stored entries without generating summaries

### Requirement: Runtime persistence in working-directory memory store
The memory engine SHALL persist records in a single JSONL file at `$PWD/.memory/literature-explainer.memory.jsonl` and SHALL create the directory/file lazily if missing.

#### Scenario: Missing memory directory is auto-created
- **WHEN** update mode runs and `.memory` does not exist
- **THEN** the script creates `.memory` and appends the new record to the JSONL file

### Requirement: Study-note phase reads memory before note synthesis
Before generating final study notes, the system SHALL call read mode to fetch raw memory entries filtered by `paper_key` and/or `session_key`.

#### Scenario: Note generation obtains relevant memory entries
- **WHEN** the user asks to generate study notes
- **THEN** the agent reads memory entries for the active paper/session and uses them as source material
