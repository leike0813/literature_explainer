## 1. OpenSpec Artifacts

- [x] 1.1 Create proposal with guardrail motivation and impact
- [x] 1.2 Create evidence-verification capability spec with scenarios
- [x] 1.3 Create design documenting two-mode script and verdict policy
- [x] 1.4 Create trackable tasks with implementation and validation steps

## 2. Verifier Implementation

- [x] 2.1 Add `literature-explainer/scripts/evidence_verifier.py` with modes `instructions` and `verify`
- [x] 2.2 Implement web URL validation with keyword hit checks
- [x] 2.3 Implement reference title validation via Crossref/arXiv/Semantic Scholar
- [x] 2.4 Implement verdict aggregation and JSON output contract

## 3. Skill Integration and Validation

- [x] 3.1 Update `literature-explainer/SKILL.md` with post-Q&A verification sequence
- [x] 3.2 Add hallucination fail handling and fixed user warning text requirement
- [x] 3.3 Verify change readiness and validation (`status`/`apply`/`validate`)
- [x] 3.4 Run script behavior checks for pass/fail/uncertain and run mypy
