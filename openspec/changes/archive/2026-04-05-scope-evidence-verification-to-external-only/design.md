# Design: Evidence Verification Scope Refinement

## Overview

Limit the evidence verification scope to external evidence (from web searches) only; paper text evidence is automatically skipped when passed to the verifier.

## Architecture

### Evidence Type Classification

```
┌─────────────────────────────────────────────────────────┐
│                    Evidence Item                        │
├─────────────────────────────────────────────────────────┤
│  ┌─────────────────┐  ┌────────────────────────────────┐│
│  │  Internal       │  │  External                      ││
│  │  Evidence       │  │  Evidence                      ││
│  │                 │  │                                ││
│  │ source_type:    │  │ source_type:                   ││
│  │ - paper_text    │  │ - web_url                      ││
│  │                 │  │ - reference_title              ││
│  │ Verification:   │  │                                ││
│  │ Skipped         │  │ Verification:                  ││
│  │                 │  │ - Web scraping                 ││
│  │ Reason:         │  │ - Academic API query           ││
│  │ Paper text is   │  │                                ││
│  │ already verified│  │ Reason:                        ││
│  │ source          │  │ Need to verify source          ││
│  │                 │  │ authenticity and               ││
│  │                 │  │ keyword match                  ││
│  └─────────────────┘  └────────────────────────────────┘│
└─────────────────────────────────────────────────────────┘
```

## Component Changes

### evidence_verifier.py

#### 1. Add VALID_SOURCE_TYPES

```python
VALID_SOURCE_TYPES = {"web_url", "reference_title", "paper_text"}
```

#### 2. Modify _validate_evidence_item

```python
def _validate_evidence_item(item: Any, index: int) -> tuple[bool, dict[str, Any]]:
    # ... existing field validation ...
    
    source_type = str(item["source_type"])
    if source_type not in VALID_SOURCE_TYPES:
        return False, {
            "index": index,
            "status": "fail",
            "reason": "invalid_source_type",
            "valid_source_types": sorted(VALID_SOURCE_TYPES),
        }
    
    # paper_text type returns skip result directly
    if source_type == "paper_text":
        return True, {
            "index": index,
            "status": "skipped",
            "reason": "internal_evidence_no_verification_needed",
            "source_type": source_type,
            "source": str(item["source"]),
            "claim": str(item["claim"]),
            "keywords": [str(k) for k in item["keywords"]],
        }
    
    # ... other types continue with existing verification flow ...
```

#### 3. Modify handle_verify verification loop

```python
def handle_verify(evidence_json: str) -> None:
    # ... parsing and validation ...
    
    results: list[dict[str, Any]] = []
    statuses: list[str] = []
    for idx, item in enumerate(evidence):
        valid, invalid_result = _validate_evidence_item(item, idx)
        if not valid:
            # Handle invalid evidence
            ...
            continue
        
        # paper_text type already returned skipped in _validate_evidence_item
        if item["source_type"] == "paper_text":
            # Already handled above, this code path is not reached
            ...
        
        source_type = str(item["source_type"])
        source = str(item["source"])
        keywords = [str(keyword) for keyword in item["keywords"]]
        claim = str(item["claim"])
        
        # Execute verification only for external evidence
        if source_type == "web_url":
            verification = _verify_web_url(source, keywords)
        elif source_type == "reference_title":
            verification = _verify_reference_title(source)
        else:
            # Should not reach here
            continue
        
        results.append({
            "index": idx,
            "source_type": source_type,
            "source": source,
            "claim": claim,
            "keywords": keywords,
            "status": verification.status,
            **verification.detail,
        })
        statuses.append(verification.status)
```

#### 4. Modify verdict determination logic

```python
# Determine verdict after excluding skipped items
verifiable_statuses = [
    s for s, r in zip(statuses, results) 
    if r.get("status") != "skipped"
]

if not verifiable_statuses:
    verdict = "pass"  # No items requiring verification, default to pass
elif "fail" in verifiable_statuses:
    verdict = "fail"
elif "uncertain" in verifiable_statuses:
    verdict = "uncertain"
else:
    verdict = "pass"
```

### memory_engine.py

#### Modify VALID_SOURCE_TYPES

```python
VALID_SOURCE_TYPES = {"web_url", "reference_title", "paper_text"}
```

### SKILL.md

#### Modify Section 5: Evidence Answer Rules

```markdown
## 5. 证据回答规则

- **必须** 优先使用用户提供论文中的直接证据。
- **必须** 在需要补充外部知识时，先在可访问范围检索，再决定是否联网检索。
- **必须** 保证每次 Q&A 回答中证据列表的来源真实、可查证。
- **必须** 在回答后执行验证脚本，并在当前会话回显验证结果。
  - Paper text evidence (`paper_text`) is internal evidence, automatically skipped by verifier
  - External evidence (`web_url`, `reference_title`) requires network verification
- **不得** 把无法追溯来源的外部信息当作确定性结论。
```

#### Modify Evidence Array Field Description

```markdown
"evidence_items":[
  {
    "source_type": "paper_text | web_url | reference_title",
    "source": "<original text quote or URL or reference title>",
    "keywords": ["<keyword>"],
    "claim": "<assertion supported by evidence>"
  }
]
```

## Testing Strategy

### Unit Tests

1. **paper_text evidence skips verification**
   - Input: Array containing only `paper_text` evidence
   - Expected: All items status `skipped`, final verdict `pass`

2. **Mixed evidence types**
   - Input: Mixed array of `paper_text` and `web_url`
   - Expected: `paper_text` skipped, `web_url` verified normally, verdict determined by `web_url` results

3. **User message when only paper_text is present**
   - Expected: Echo "证据验证通过" (no items requiring verification, default pass)

### Integration Tests

1. Complete Q&A workflow using only paper text evidence
2. Complete Q&A workflow using mixed paper text and web evidence

## Migration Plan

No data migration required; `paper_text` is an optional new type.

## Rollback Plan

To rollback:
1. Remove `paper_text` from `VALID_SOURCE_TYPES`
2. Restore original SKILL.md description
