# skill-instruction-architecture Specification

## Purpose
TBD - created by syncing change refactor-skill-instructions-v1. Update Purpose after archive.

## Requirements
### Requirement: SKILL document must use a main-flow-first structure
The published `SKILL.md` SHALL organize instructions around the primary execution flow first, so an agent can identify goals, constraints, states, and output expectations before reading script-specific details.

#### Scenario: Agent reads the skill document in execution order
- **WHEN** an agent opens `literature-explainer/SKILL.md`
- **THEN** it can identify task goals, hard constraints, state transitions, and final note requirements without scanning protocol details first

### Requirement: Detailed field rules must be delegated to script instructions
The `SKILL.md` document SHALL keep only primary rules, hard constraints, and script invocation timing, while stage-specific field rules and protocol details SHALL be provided by script `instructions` outputs.

#### Scenario: Field-level details are retrieved from scripts
- **WHEN** the agent needs stage-specific memory or verification details
- **THEN** it uses the relevant script `instructions` output instead of relying on duplicated field explanations in `SKILL.md`

### Requirement: Script instructions must use a unified top-level schema
`memory_engine.py` and `evidence_verifier.py` SHALL return `instructions` payloads with a unified top-level schema that includes `ok`, `mode`, `stage` or `trigger_scope`, `required_fields`, `rules`, and `output_contract`.

#### Scenario: Both scripts expose parallel instruction shapes
- **WHEN** the agent calls either script in `instructions` mode
- **THEN** the response uses the same top-level structure and clearly exposes required fields, behavioral rules, and output expectations

### Requirement: Existing core capabilities must remain executable
The refactor SHALL preserve the existing executable capabilities for initial paper analysis, evidence-backed Q&A, post-answer verification echo, memory updates, and study-note generation.

#### Scenario: Refactor preserves current skill behavior
- **WHEN** the agent follows the refactored skill and scripts
- **THEN** it can still complete analysis, Q&A, verification, memory update, and note generation without relying on removed behaviors
