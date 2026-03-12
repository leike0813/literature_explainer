## Design Decisions

### Decision 1: `paper_key` is derived from `input_hash`
The repository already exposes `provenance.input_hash` as a stable paper identity source. This change uses that value to derive a shorter `paper_key`, rather than introducing a second independent naming system.

### Decision 2: Isolation is done at the file-path level
The main failure mode is cross-paper collision in both temp artifacts and persistent memory. The design therefore isolates dispatcher outputs under `<tmp>/<paper_key>/` and memory under a paper-specific JSONL file, instead of trying to solve everything through logical filters alone.

### Decision 3: Note is a file artifact, not a memory stage
The final note is treated as a paper-scoped file artifact (`note.<paper_key>.md`), not as a `stage=note` memory record. Regenerating a note overwrites the existing note file while preserving analysis and QA memory records that feed later note regeneration.

### Decision 4: Note generation uses paper-global analysis and session-local QA
The note should carry forward stable paper understanding across sessions, but Q&A content should remain scoped to the current interaction thread. This prevents stale cross-session Q&A from polluting a later note while still avoiding redoing analysis.
