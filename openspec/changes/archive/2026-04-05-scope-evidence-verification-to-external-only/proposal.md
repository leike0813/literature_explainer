# Proposal: Scope Evidence Verification to External Sources Only

## Why

The current evidence verifier script `evidence_verifier.py` executes network verification against all evidence items, including:
1. External evidence obtained from web searches (`web_url`)
2. Internal evidence directly quoted from the paper text

**Problems**:
- Internal evidence (paper text) is already a "verified" source; executing network verification is redundant
- Internal evidence cannot be validated through `web_url` or `reference_title` verification logic (source type mismatch)
- The verification boundary between "internal evidence" (paper statements) and "external evidence" (requires network lookup) is blurred

**Goals**:
- Distinguish between internal and external evidence types
- Internal evidence automatically skips verification when passed to the verifier
- External evidence continues to execute the original network verification flow

## What Changes

- Modify `evidence_verifier.py`:
  - Add `source_type` value `paper_text` for paper text evidence (internal evidence)
  - Mark `paper_text` items as `skipped` in the verification loop, no network verification
  - `skipped` items do not participate in `pass/fail/uncertain` verdict determination
- Modify `memory_engine.py`: Allow `paper_text` type in `evidence_items` for `qa` stage
- Modify `SKILL.md`: Clarify the distinction between internal and external evidence and the skip handling for internal evidence

## Capabilities

### Modified Capabilities
- `evidence-verification-guardrail`: Internal evidence is exempt from network verification; verification scope is limited to external evidence

## Impact

- Affected files:
  - `literature-explainer/scripts/evidence_verifier.py`
  - `literature-explainer/scripts/memory_engine.py`
  - `literature-explainer/SKILL.md`
- Backward compatible: existing `web_url` and `reference_title` verification logic remains unchanged
