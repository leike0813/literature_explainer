## ADDED Requirements

### Requirement: Semi-fixed initial reading summary template
At skill start, the agent SHALL read and understand the paper and produce an initial summary using a semi-fixed structure that includes fixed core sections and dynamic per-section summaries based on actual paper chapters.

#### Scenario: Initial summary contains required core blocks
- **WHEN** initial paper analysis is completed
- **THEN** output contains TL;DR, research question and contributions, method points, key results, limitations/reproducibility clues, and dynamic chapter summaries

### Requirement: QA memory writing preserves question and controls answer compression
For each QA turn, memory record SHALL store `user_question` in full text without compression and SHALL store `agent_answer_summary` using length policy by `answer_original_length`.

#### Scenario: Short answer is stored without forced compression
- **WHEN** `answer_original_length` is less than or equal to 1200
- **THEN** record uses `summary_policy=raw_below_threshold` and stores answer text directly in summary field

#### Scenario: Long answer is summarized near threshold
- **WHEN** `answer_original_length` is greater than 1200
- **THEN** record uses `summary_policy=summarized_900_1200` and summary length is between 900 and 1200 characters

### Requirement: QA memory schema uses split fields in one record
QA memory SHALL use one JSONL record per turn and SHALL separate user question and agent answer into distinct fields.

#### Scenario: QA record contains split fields
- **WHEN** QA update is written
- **THEN** memory entry includes `user_question`, `agent_answer_summary`, and `answer_original_length`

### Requirement: Note generation avoids second compression
During final note generation, the system SHALL use stored memory fields directly and SHALL NOT perform second-stage summarization compression; minor wording polish is allowed if key information is preserved.

#### Scenario: Notes preserve stored memory density
- **WHEN** note generation runs from memory records
- **THEN** it uses stored summaries and questions as primary source and avoids additional compression passes

### Requirement: Memory read defaults to schema v2 only
Memory read mode SHALL ignore legacy records and return schema version 2 entries by default.

#### Scenario: Legacy records are ignored in read mode
- **WHEN** memory file contains mixed schema versions
- **THEN** read mode returns only records with `schema_version == 2` unless explicitly changed by future policy
