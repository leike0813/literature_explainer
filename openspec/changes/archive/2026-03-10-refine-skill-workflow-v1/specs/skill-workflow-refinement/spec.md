## ADDED Requirements

### Requirement: Explicit input and output contract
The skill definition MUST specify accepted paper input forms (file path, full text, excerpt), required user intent fields, and output forms for summary, Q&A responses, and optional study-note artifact.

#### Scenario: Input and output sections are machine-checkable
- **WHEN** an agent reads `literature-explainer/SKILL.md`
- **THEN** it can identify input types and output deliverables without inferring missing fields

### Requirement: Evidence-tiered answering policy
The skill MUST enforce an evidence-tiered response policy that distinguishes facts, evidence sources, and inferences, and MUST define fallback behavior when evidence is insufficient.

#### Scenario: Insufficient evidence is handled deterministically
- **WHEN** the user asks a question that cannot be fully supported by available paper text and accessible evidence
- **THEN** the agent first attempts retrieval and then explicitly reports uncertainty boundaries instead of guessing

### Requirement: Stateful interaction workflow
The skill MUST define a stateful interaction flow with explicit transitions: environment check, paper analysis, intent confirmation, iterative Q&A, note-generation decision, and completion.

#### Scenario: Agent follows deterministic state transitions
- **WHEN** a session starts with paper material
- **THEN** the agent proceeds through the defined states and does not skip intent confirmation before answering

### Requirement: Study-note generation template
The skill MUST provide a study-note template with minimum required fields, including paper metadata, key claims, evidence notes, user Q&A digest, unresolved questions, and next actions.

#### Scenario: Study note has minimum required fields
- **WHEN** the user requests note generation
- **THEN** the generated Markdown includes all required sections from the template
