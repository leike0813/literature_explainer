## 1. OpenSpec Artifacts

- [x] 1.1 Create `proposal.md` with Why/What Changes/Capabilities/Impact
- [x] 1.2 Create `specs/memory-engine/spec.md` with ADDED requirements and scenarios
- [x] 1.3 Create `design.md` with three key technical decisions
- [x] 1.4 Create `tasks.md` with trackable checkbox tasks

## 2. Memory Engine Implementation

- [x] 2.1 Add `literature-explainer/scripts/memory_engine.py` with modes `instructions/update/read`
- [x] 2.2 Persist updates to `$PWD/.memory/literature-explainer.memory.jsonl` with lazy directory/file creation
- [x] 2.3 Validate update payload required fields and emit JSON error on invalid input
- [x] 2.4 Implement read filtering by `paper_key`, `session_key`, and `limit`

## 3. Skill Integration and Validation

- [x] 3.1 Update `literature-explainer/SKILL.md` with memory call timing and command contracts only
- [x] 3.2 Verify change readiness with `openspec status` and `openspec instructions apply`
- [x] 3.3 Validate change with `openspec validate add-memory-engine-v1 --type change --json`
- [x] 3.4 Run behavior checks for script modes and run Python type-check flow
