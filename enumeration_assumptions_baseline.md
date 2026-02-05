# Enumeration Baseline Assumptions  
PowerCenter → Target Platform (Phase-1 Migration Analysis)

This document defines the "baseline assumptions" used when enumerating
Informatica PowerCenter workflows and mappings into target-platform JSON
definitions for migration analysis.

These assumptions apply "globally" to all workflows unless explicitly
overridden in a workflow-specific `enumeration_assumptions.md`.

This baseline is "not a commitment to execution correctness" and is intended
solely to support feasibility analysis, gap identification, and planning.

---

1. Scope & Intent

- The purpose of enumeration is "migration readiness assessment", not final execution.
- Enumerated JSONs represent "best-effort intent alignment" with source workflows.
- Successful enumeration does "not guarantee" runtime equivalence on the target platform.
- Platform behavior, adapter logic, and runtime semantics will be validated separately.

---

2. Workflow-Level Assumptions

- One PowerCenter workflow is mapped to one target pipeline.
- Session execution order is the primary source of task dependency inference.
- Workflow task links and conditions define the logical execution DAG.
- Conditional and decision-based transitions are:
  - Preserved as intent where possible
  - Flagged as gaps if not directly expressible in the target platform
- Non-data tasks (email, decision, command, timer) are:
  - Documented as gaps unless explicitly supported by the platform.

---

3. Mapping-Level Assumptions

- One PowerCenter mapping corresponds to one logical transformation task.
- Source Qualifier SQL is treated as "extraction logic".
- Expression transformations are:
  - Mapped only if expressible as scalar or deterministic functions.
- Joiner, Aggregator, Rank, and Lookup transformations are:
  - Represented at an **intent level** only.
  - Detailed execution semantics are deferred to validation phases.

---

4. Data Semantics Assumptions

- Update Strategy is treated as:
  - INSERT/OVERWRITE unless explicitly detectable.
- Reject rows and error rows:
  - Are out of scope for Phase-1 unless explicitly modeled.
- Null handling follows PowerCenter defaults unless overridden.

---

5. Connection & Dataset Assumptions

- Connection objects are assumed to exist or be migratable independently.
- Dataset definitions reference logical source/target identifiers.
- Physical connection properties (host, port, credentials):
  - Are not validated during enumeration.

---

6. Runtime & Execution Assumptions

- All tasks execute using Spark unless explicitly unsupported.
- Default workload profile is assumed as "balanced".
- Retry counts, retry delays, and timeouts:
  - Use platform defaults unless specified in source metadata.
- Parallelism and partitioning:
  - Are not inferred unless explicitly defined.

---

7. Parameterization Assumptions

- Workflow and mapping parameters are:
  - Documented but not dynamically resolved.
- Parameter files and overrides:
  - Are treated as external dependencies.

---

8. Out-of-Scope Items (Phase-1)

The following are intentionally excluded from enumeration:

- Advanced error handling
- Session recovery logic
- Pushdown optimization semantics
- Pre/Post SQL execution order guarantees
- Custom scripts and command tasks
- Scheduler-specific behavior

---

9. Validation & Gaps

- Any behavior that cannot be confidently inferred is flagged as:
  - Gap
  - Assumption
  - Unsupported Pattern
- Gaps do not imply failure, they inform feasibility and design decisions.

---

10. Change Control

- This baseline may evolve as platform understanding improves.
- Changes to this baseline must be versioned and communicated.
- Workflow-specific deviations must NOT modify this file.

---
