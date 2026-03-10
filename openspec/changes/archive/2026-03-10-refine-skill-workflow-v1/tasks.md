## 1. OpenSpec Artifacts

- [x] 1.1 Create `proposal.md` with Why/What Changes/Capabilities/Impact
- [x] 1.2 Create `specs/skill-workflow-refinement/spec.md` with ADDED requirements and scenarios
- [x] 1.3 Create `design.md` with fixed decisions and trade-offs
- [x] 1.4 Create `tasks.md` with trackable checkboxes and grouped workstreams

## 2. SKILL.md Refinement

- [x] 2.1 Rewrite `literature-explainer/SKILL.md` into release-ready initial version
- [x] 2.2 Add explicit input/output contract and evidence-tiered answering rules
- [x] 2.3 Add state transition workflow and study-note template
- [x] 2.4 Keep no-script declaration and avoid creating optional directories

## 3. Validation and Completion

- [x] 3.1 Verify artifacts done with `openspec status --change "refine-skill-workflow-v1" --json`
- [x] 3.2 Verify apply readiness with `openspec instructions apply --change "refine-skill-workflow-v1" --json`
- [x] 3.3 Validate change with `openspec validate refine-skill-workflow-v1 --type change --json`
- [x] 3.4 Run Python type-check flow (discover files, run mypy if applicable, or record N/A)
