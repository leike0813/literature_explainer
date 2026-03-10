## 1. OpenSpec Artifacts

- [x] 1.1 Create proposal for execution-guidance refinement scope and motivation
- [x] 1.2 Create `execution-guidance-refinement` spec with scenarios
- [x] 1.3 Create design for stage-detail structure and emphasis strategy
- [x] 1.4 Create implementation and validation checklist

## 2. Skill Guidance Refinement

- [x] 2.1 Rewrite `literature-explainer/SKILL.md` to strengthen critical constraints with explicit emphasis
- [x] 2.2 Add `操作步骤` / `问题与考量` / `何时询问用户` to every state S0-S5
- [x] 2.3 Preserve existing workflow while making stage guidance more concrete and enforceable

## 3. Script Instruction Guidance Enhancement

- [x] 3.1 Enhance `memory_engine.py` instructions with execution steps, caution points, and stop conditions
- [x] 3.2 Enhance `evidence_verifier.py` instructions with execution steps, invalid-input failures, and post-verdict reminders
- [x] 3.3 Preserve existing `update/read/verify` behavior and instruction top-level shape

## 4. Validation and Finish

- [x] 4.1 Verify OpenSpec readiness (`status` and `instructions apply`)
- [x] 4.2 Validate change (`openspec validate`)
- [x] 4.3 Check instructions output for both scripts and all memory stages
- [x] 4.4 Run type checking for Python scripts
