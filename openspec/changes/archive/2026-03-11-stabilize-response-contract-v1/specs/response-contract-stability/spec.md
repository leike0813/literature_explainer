## ADDED Requirements

### Requirement: S3 fixed response contract
The Skill SHALL require every S3 Q&A turn to follow a fixed output template and SHALL include verifier echo as part of the same turn contract.

#### Scenario: Standard QA turn
- **GIVEN** the Agent is answering a user question in S3
- **WHEN** the answer is produced
- **THEN** the output includes `问题理解`、`事实`、`证据`、`推断`、`不确定点`、`证据数组`、`验证结果`
- **AND** `验证结果` is echoed before the workflow can move to memory update or the next turn

### Requirement: Multi-question handling
The Skill SHALL require multi-question inputs to be split before answering and SHALL require the Agent to either answer in order or ask the user to narrow scope.

#### Scenario: Multiple sub-questions fit one turn
- **GIVEN** the user sends one message containing multiple related sub-questions
- **WHEN** the full set can be answered clearly in one turn
- **THEN** the Agent answers them in explicit sub-question order within the fixed response contract

#### Scenario: Multiple sub-questions exceed one turn
- **GIVEN** the user sends one message containing multiple broad or conflicting sub-questions
- **WHEN** answering all of them in one turn would reduce clarity or evidence quality
- **THEN** the Agent asks the user to set priority or narrow scope before continuing

### Requirement: Minimal clarification principle
The Skill SHALL require clarification to be minimal and SHALL prevent repeated clarification-only turns without progress.

#### Scenario: Partial answer is possible
- **GIVEN** the user question is partly clear and partly ambiguous
- **WHEN** at least one part can already be answered with available evidence
- **THEN** the Agent answers the clear part first
- **AND** asks only one most critical clarification question for the remaining ambiguous part

#### Scenario: Clarification drift
- **GIVEN** the Agent has already asked for clarification in the previous turn
- **WHEN** the next turn would otherwise be another clarification-only message
- **THEN** the Agent must provide whatever factual progress is already supportable instead of continuing pure clarification drift

### Requirement: Verification failure repair
The Skill SHALL require a failed verification result to trigger a repair sequence, not just a warning.

#### Scenario: Evidence verification fails
- **GIVEN** `verify` returns `fail`
- **WHEN** the current turn is corrected
- **THEN** the Agent explicitly identifies the unsupported part of the previous answer
- **AND** withdraws the unsupported assertion
- **AND** re-answers using only still-supported facts
- **AND** echoes the fixed hallucination warning in the current session

### Requirement: Stage exit checklists
The Skill SHALL require explicit exit checklists for S1, S3, and S4 before leaving those stages.

#### Scenario: Leaving S1
- **GIVEN** the Agent is ready to leave initial analysis
- **WHEN** it checks stage-exit conditions
- **THEN** it confirms that a stable first-pass understanding exists
- **AND** the initial-analysis memory write has completed

#### Scenario: Leaving S3
- **GIVEN** the Agent is ready to leave a QA turn
- **WHEN** it checks stage-exit conditions
- **THEN** it confirms that the fixed answer template was followed
- **AND** verification ran and was echoed
- **AND** the QA memory write used the finalized turn result

#### Scenario: Leaving S4
- **GIVEN** the Agent is ready to leave note generation
- **WHEN** it checks stage-exit conditions
- **THEN** it confirms that the user explicitly requested note generation
- **AND** only structured memory records were used
- **AND** the `stage=note` record write completed
