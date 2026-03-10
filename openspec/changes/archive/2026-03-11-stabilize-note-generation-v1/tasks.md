## 1. OpenSpec Artifacts

- [x] 1.1 Create proposal for note-generation stability scope and motivation
- [x] 1.2 Create `note-generation-stability` spec with scenarios
- [x] 1.3 Create design covering optional generation and Q&A-centered note structure
- [x] 1.4 Create implementation and validation checklist

## 2. Skill Note-Stage Stabilization

- [x] 2.1 Update `literature-explainer/SKILL.md` to make note generation optional and allow direct completion
- [x] 2.2 Update `literature-explainer/SKILL.md` to fix note structure as one-paragraph paper summary plus Q&A-centered body
- [x] 2.3 Update `literature-explainer/SKILL.md` to define deterministic note-stage execution order

## 3. Memory Note Protocol Stabilization

- [x] 3.1 Update `literature-explainer/scripts/memory_engine.py` note instructions with optional generation and fixed section rules
- [x] 3.2 Update note rules to require memory-only note generation and note write-back
- [x] 3.3 Preserve existing `update/read` operational behavior while clarifying `stage=note` semantics

## 4. Validation and Finish

- [x] 4.1 Verify OpenSpec readiness (`status` and `instructions apply`)
- [x] 4.2 Validate change (`openspec validate`)
- [x] 4.3 Check `instructions --stage note` output and note update behavior
- [x] 4.4 Run type checking for Python scripts
