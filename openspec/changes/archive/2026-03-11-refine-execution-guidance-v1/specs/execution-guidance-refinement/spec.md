## ADDED Requirements

### Requirement: SKILL must emphasize critical constraints explicitly
The `SKILL.md` document SHALL mark critical constraints using explicit emphasis so that mandatory rules are visually prominent and easy to follow during execution.

#### Scenario: Critical constraints are visually prominent
- **WHEN** an agent reads `literature-explainer/SKILL.md`
- **THEN** rules that are mandatory or prohibited are explicitly emphasized
- **AND** those rules are distinguishable from general guidance

### Requirement: Every state must include steps, risks, and user-query triggers
For each execution state S0 through S5, the `SKILL.md` document SHALL include `操作步骤`, `问题与考量`, and `何时询问用户`.

#### Scenario: Agent can execute any state with detailed guidance
- **WHEN** the agent enters any state from S0 to S5
- **THEN** it can identify what to do, what may go wrong, and when it must ask the user before proceeding

### Requirement: Script instructions must include operational guidance
`memory_engine.py` and `evidence_verifier.py` SHALL keep their existing instruction output shape and SHALL augment `rules` with execution steps, caution points, failure conditions, or next-step reminders.

#### Scenario: Script instructions provide execution-oriented guidance
- **WHEN** the agent calls a script in `instructions` mode
- **THEN** the response contains not only field contracts but also practical execution guidance for that stage or trigger

### Requirement: Guidance refinement must preserve current workflow and script responsibilities
The refinement SHALL NOT remove existing core workflow behavior or change the primary responsibilities of `update`, `read`, or `verify`.

#### Scenario: Existing skill flow remains executable
- **WHEN** the agent follows the refined skill and scripts
- **THEN** the existing analysis, Q&A, verification, memory update, note generation, and completion flow remains intact
