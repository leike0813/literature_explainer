## Design Decisions

### Decision 1: Contract-first reinforcement in `SKILL.md`
This change strengthens execution by fixing the external shape of S3 answers and by adding mandatory exit checklists in `SKILL.md`. The main document remains the place where stage flow, hard constraints, and user-facing execution order are defined.

### Decision 2: No runtime or schema expansion
The change does not add new scripts, new modes, or new persisted fields. `memory_engine.py` and `evidence_verifier.py` only gain richer `instructions` guidance so that the Agent can retrieve detailed execution rules without changing `verify/update/read` behavior.

### Decision 3: Verification failure must repair, not only warn
The most important behavioral gap is after `verify=fail`. The design therefore requires a repair sequence: identify the unsupported part, withdraw it, and restate the answer using only confirmed facts. This stays as a natural-language contract plus script guidance, rather than introducing new enforcement machinery.

### Decision 4: Clarification and multi-question handling remain Agent-level policies
Question splitting, minimal clarification, and language inheritance are kept as instruction-level rules. They are not encoded into deterministic Python logic because they depend on semantic interpretation and should stay in the LLM-controlled flow.
