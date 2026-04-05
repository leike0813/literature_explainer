# evidence-verification-scope Specification

## Purpose

Clarify the scope of the evidence verification script: network verification is executed only for external evidence; paper text evidence (internal evidence) is automatically skipped when passed to the verifier.

## Requirements

### Requirement: Evidence types MUST distinguish internal and external evidence

The evidence verification script SHALL support the following evidence types:

| source_type | Type Category | Verification Method |
|-------------|---------------|---------------------|
| `paper_text` | Internal | Skip verification (`skipped`) |
| `web_url` | External | Fetch web page, verify keyword match |
| `reference_title` | External | Query Crossref/arXiv/Semantic Scholar |

#### Scenario: Verifier correctly handles three evidence types
- **WHEN** the verifier receives a `paper_text` evidence item
- **THEN** the item status is marked as `skipped` without network verification
- **AND** the `skipped` status does not affect the final `pass/fail/uncertain` verdict

### Requirement: Verdict determination logic MUST exclude skipped items

Final verdict determination SHALL follow:
- `pass`: All evidence items requiring verification pass (no `fail` items)
- `fail`: At least one evidence item requiring verification explicitly fails
- `uncertain`: No `fail` but at least one evidence item requiring verification cannot be determined due to network/backend issues

**Note**: `skipped` items do not participate in any of the above determinations.

#### Scenario: Verification passes when only paper_text evidence is present
- **WHEN** all evidence in a turn is of `paper_text` type
- **THEN** the verdict is `pass` (no items requiring verification, defaults to pass)

### Requirement: SKILL.md MUST clarify distinction between internal and external evidence

`SKILL.md` SHALL clarify in the evidence answer rules:
- Paper text evidence (`paper_text`) is internal evidence, exempt from network verification
- External evidence (`web_url`, `reference_title`) requires network verification
- When calling `verify`, all evidence may be passed (verifier automatically skips `paper_text`), or only external evidence may be passed

#### Scenario: Agent follows correct verification workflow
- **WHEN** the Agent completes a Q&A answer
- **THEN** the Agent may pass all evidence to the `verify` script; the verifier automatically skips `paper_text` types

### Requirement: memory_engine MUST allow paper_text evidence type

`memory_engine.py` SHALL allow `paper_text` as a valid `source_type` value during `evidence_items` validation for the `qa` stage.

#### Scenario: Writing memory accepts paper_text evidence
- **WHEN** the Agent calls `memory_engine.py --mode update` to write a QA record containing `paper_text` evidence
- **THEN** validation passes and the record is successfully written

## Output Contract

### verify mode output

For `paper_text` type evidence, the verification result item format:

```json
{
  "index": 0,
  "source_type": "paper_text",
  "source": "...",
  "claim": "...",
  "keywords": ["..."],
  "status": "skipped",
  "reason": "internal_evidence_no_verification_needed"
}
```

### Final verdict determination

```python
# Determine verdict after excluding skipped items
verifiable_results = [r for r in results if r["status"] != "skipped"]
if not verifiable_results:
    verdict = "pass"  # No items requiring verification, default to pass
elif "fail" in statuses:
    verdict = "fail"
elif "uncertain" in statuses:
    verdict = "uncertain"
else:
    verdict = "pass"
```

## Migration Notes

- Existing evidence items using `web_url` and `reference_title` are unaffected
- The new `paper_text` type is optional; no forced migration of existing records
- It is recommended to use `paper_text` type for paper text evidence in newly generated QA memories
