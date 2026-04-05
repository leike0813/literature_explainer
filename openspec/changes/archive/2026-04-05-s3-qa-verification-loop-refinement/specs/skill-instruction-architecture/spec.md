# skill-instruction-architecture Specification Delta

## MODIFIED Requirements

### Requirement: S3 QA execution flow must use an embedded verification loop

The `SKILL.md` document SHALL define the S3 QA cycle execution flow as an embedded verification loop pattern instead of a linear sequence. The agent SHALL follow this workflow:

1. Organize an answer draft with structured evidence array
2. Execute `verify` script
3. Evaluate verdict:
   - `pass`: Promote draft to final answer
   - `fail`: Withdraw unverified assertions, repair draft, return to step 2
   - `uncertain`: Mark uncertainty, promote draft to final answer with explicit user notification
4. Output final answer merged with next-action guidance as a single message
5. Execute `memory update`

#### Scenario: Agent executes embedded verification loop for a QA turn
- **WHEN** the agent produces an answer draft
- **THEN** it calls `verify` before outputting to the user
- **AND** if verdict is `fail`, the agent repairs the draft internally and retries verification
- **AND** only the verified final answer is output to the user

#### Scenario: Final answer is merged with next-action guidance
- **WHEN** verification passes and final answer is ready
- **THEN** the agent outputs a single message containing both the answer and next-action guidance
- **AND** the next-action guidance asks about user's intent for the following turn

#### Scenario: Maximum retry limit on verification failure
- **WHEN** verification returns `fail` for 3 consecutive retries
- **THEN** the agent outputs the verifiable portion of the answer
- **AND** explicitly informs the user which assertions could not be verified
- **AND** marks the turn as requiring user clarification or additional material

### Requirement: S3 output contract must combine answer and guidance

The S3 QA cycle output SHALL consist of two parts delivered in a single message:
1. **Answer content**: The fixed response template (问题理解，事实，证据，推断，不确定点，证据列表，验证结果)
2. **Next-action guidance**: A brief question about user intent (clarification if needed, or confirmation to continue)

#### Scenario: User receives combined answer and guidance
- **WHEN** the S3 cycle completes
- **THEN** the user receives both the verified answer and the next-action question in one message
- **AND** the message does not require a separate follow-up for guidance
