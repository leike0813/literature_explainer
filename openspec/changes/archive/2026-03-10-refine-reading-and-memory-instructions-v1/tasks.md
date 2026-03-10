## 1. OpenSpec Artifacts

- [x] 1.1 Create proposal for reading and memory instruction refinement
- [x] 1.2 Create spec for semi-fixed reading template and QA memory policy
- [x] 1.3 Create design with schema v2 and compression decisions
- [x] 1.4 Create execution tasks with verification checklist

## 2. SKILL Instruction Refinement

- [x] 2.1 Add semi-fixed initial analysis template requirements in `SKILL.md`
- [x] 2.2 Add QA memory rules for full question storage and answer length policy
- [x] 2.3 Add note-generation rule to avoid second compression and allow minor polish
- [x] 2.4 Update memory command examples to keep generic Python invocation convention

## 3. Memory Engine v2 Upgrade

- [x] 3.1 Update `instructions` output with `reading_template`, `qa_memory_policy`, `note_generation_policy`
- [x] 3.2 Upgrade `update` mode to schema v2 with stage-specific field constraints
- [x] 3.3 Enforce QA summary policy: `raw_below_threshold` vs `summarized_900_1200`
- [x] 3.4 Make `read` mode return schema v2 records by default

## 4. Validation

- [x] 4.1 Verify OpenSpec status/apply/validate for this change
- [x] 4.2 Run memory engine behavior checks for initial_analysis/qa/read paths
- [x] 4.3 Run mypy for scripts
