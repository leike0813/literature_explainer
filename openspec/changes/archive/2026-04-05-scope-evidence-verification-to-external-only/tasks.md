# Tasks: Evidence Verification Scope Refinement

## Implementation Tasks

### [x] 1. Modify evidence_verifier.py

- [x] 1.1 Add `"paper_text"` to `VALID_SOURCE_TYPES`
- [x] 1.2 Modify `_validate_evidence_item` function:
  - [x] Return `skipped` status for `paper_text` type
  - [x] Return pre-formatted result dictionary
- [x] 1.3 Modify `handle_verify` function:
  - [x] Skip items marked as `skipped` in verification loop
  - [x] Modify verdict determination logic to exclude `skipped` status
- [x] 1.4 Update `instructions` output:
  - [x] Add `paper_text` to `valid_source_types`
  - [x] Document `paper_text` skip verification in `verification` rules

### [x] 2. Modify memory_engine.py

- [x] 2.1 Add `"paper_text"` to `VALID_SOURCE_TYPES`
- [x] 2.2 Verification test: Ensure `paper_text` type evidence can be successfully written to memory

### [x] 3. Modify SKILL.md

- [x] 3.1 Update Section 5 "Evidence Answer Rules":
  - [x] Clarify `paper_text` (internal evidence) is exempt from network verification
  - [x] Clarify external evidence requires network verification
- [x] 3.2 Update Section 7.1 memory script invocation examples:
  - [x] Add `paper_text` type description in `evidence_items` example
- [x] 3.3 Update evidence array field description

### [x] 4. Testing

- [x] 4.1 Unit tests:
  - [x] Verification result for `paper_text` evidence only
  - [x] Verification result for mixed evidence types
- [x] 4.2 Integration tests:
  - [x] Complete Q&A workflow test

## File Checklist

| File | Change Type |
|------|-------------|
| `literature-explainer/scripts/evidence_verifier.py` | Modified |
| `literature-explainer/scripts/memory_engine.py` | Modified |
| `literature-explainer/SKILL.md` | Modified |

## Acceptance Criteria

- [x] `paper_text` evidence passed to verifier returns status `skipped`
- [x] Final verdict is `pass` when only `paper_text` evidence is present
- [x] For mixed evidence types, verdict is determined by external evidence verification results
- [x] `memory_engine.py` accepts `paper_text` type and successfully writes to memory
- [x] `SKILL.md` clearly explains the distinction between internal and external evidence and their verification handling
