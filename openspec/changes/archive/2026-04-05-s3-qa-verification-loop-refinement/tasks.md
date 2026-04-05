# Tasks: S3 QA Verification Loop Refinement

## Implementation Tasks

## 1. Modify SKILL.md S3 Section

- [x] 1.1 Update "操作步骤" to describe embedded verification loop pattern
- [x] 1.2 Replace linear "固定顺序执行" with loop-based execution flow
- [x] 1.3 Add draft → verify → repair → final workflow description
- [x] 1.4 Update output contract to specify merged answer + guidance message

## 2. Update S3 Verification and Retry Logic

- [x] 2.1 Add maximum 3-retry limit for verification failures
- [x] 2.2 Define fallback behavior when retry limit exceeded
- [x] 2.3 Clarify handling of `uncertain` verdict (continue with notification)

## 3. Update S3 Exit Criteria

- [x] 3.1 Update "离开本阶段前必须确认" to reflect verified-final answer requirement
- [x] 3.2 Add confirmation that output is merged answer + guidance

## 4. Testing

- [x] 4.1 Manual test: Verify loop behavior with a sample QA turn
- [x] 4.2 Manual test: Test retry limit with failing verification scenario
- [x] 4.3 Confirm merged output format

## File Checklist

| File | Change Type |
|------|-------------|
| `literature-explainer/SKILL.md` | Modified |

## Acceptance Criteria

- [x] S3 execution flow describes embedded verification loop (not linear sequence)
- [x] Draft → verify → repair → final pattern is clearly documented
- [x] Maximum 3-retry limit is specified
- [x] Output contract requires merged answer + guidance message
- [x] Exit criteria updated to reflect new workflow
