# Process Impact Assessment — Spec

**Artifact type:** Process Impact Assessment (PIA)
**Kit:** Business Process Kit (BPK), Layer 15
Version: v1.0

---

## Purpose

The Process Impact Assessment identifies every business process affected by a technical change, classifies the nature of each impact, and maps which roles are affected. It is the foundation for transition planning and readiness confirmation.

---

## Artifact ID Format

`PIA-{INITIATIVE}-{NNN}`

Example: `PIA-TASKFLOW-001`

---

## Trigger

Generate a PIA when a SAD or TDD is frozen in EEK and the solution introduces changes that affect business processes, user workflows, or operational procedures.

If the SAD and TDD do not reveal process-affecting changes, BPK artifacts are not required for that initiative. However, the decision to skip BPK must be an explicit declaration, not a silent omission.

---

## Inputs

| Input | Source | Required |
|-------|--------|----------|
| Frozen SAD | EEK | Yes (at least one of SAD or TDD) |
| Frozen TDD | EEK | Yes (at least one of SAD or TDD) |
| Frozen DPRD | PIK | Recommended (provides user context) |
| Existing process documentation | Consuming project | If available |

---

## Sections

### §1 Document Control

| Field | Value |
|-------|-------|
| PIA ID | `PIA-{INITIATIVE}-{NNN}` |
| Initiative | Full initiative name |
| Owner | Team or role responsible for process change governance |
| Version | Document version |
| Status | Draft / Validated / Frozen |
| SAD Reference | SAD artifact ID |
| TDD Reference | TDD artifact ID (if available) |
| Governance Model Version | Version of governance model in effect |
| Prompt Version | Version of the prompt used to generate this artifact |
| Spec Version | v1.0 |
| Principles Version | business-process-principles v1.0 |

The Owner field must be a team or role, not an individual name.

### §2 Process Inventory

A table listing every business process affected by this initiative.

| Process Name | Process Owner | Frequency | Current Description |
|-------------|--------------|-----------|-------------------|
| {name} | {team/role} | {daily/weekly/per-event/etc.} | {brief description of current-state process} |

Every process referenced anywhere else in the PIA must appear in this inventory. No process may be mentioned in §3–§5 that is absent from this table.

### §3 Impact Classification

A table classifying the impact on each inventoried process.

| Process | Classification | Source Reference |
|---------|---------------|-----------------|
| {name} | Added / Modified / Removed / Unchanged-Dependent | {SAD/TDD section reference} |

Classification definitions:
- **Added** — A new process that does not exist today. Created by the solution.
- **Modified** — An existing process whose steps, roles, tools, or triggers change.
- **Removed** — An existing process that is eliminated by the solution.
- **Unchanged-Dependent** — An existing process that is not changed but depends on a system or data source that is changing. May require awareness, not workflow change.

Every classification must cite a specific SAD component or TDD design decision as the source. No impact is asserted without a traceable source reference.

### §4 Impact Detail

For each process classified as Added, Modified, or Removed, provide:

- **Current steps** (Modified/Removed only) — numbered list of current workflow steps
- **Future steps** (Added/Modified only) — numbered list of future workflow steps
- **Changed roles** — which roles gain, lose, or change responsibilities for this process
- **Changed tools/systems** — which tools or systems are introduced, replaced, or removed
- **Dependencies** — upstream/downstream processes that feed into or consume from this process

For Unchanged-Dependent processes, document what is changing in the upstream system and why the process owner should be aware.

### §5 Role Impact Summary

An aggregated view by role, across all processes.

| Role | Processes Gained | Processes Changed | Processes Lost | Net Impact |
|------|-----------------|------------------|---------------|------------|
| {role} | {list} | {list} | {list} | {brief summary} |

This section enables stakeholder-centric communication planning in the Transition Plan.

### §6 Risk and Mitigation

Identify risks specific to the process change:

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| {description} | High / Medium / Low | {what goes wrong} | {mitigation approach} |

Common process change risks include: parallel system confusion (users operating old and new simultaneously), training gaps (insufficient preparation time), role ambiguity (unclear who owns the new process), and data migration errors (process depends on data that is being migrated).

---

## Hard Gates

| # | Gate | Rule |
|---|------|------|
| 1 | `process_inventory` | Every affected business process is listed in §2 with process owner, frequency, and current description. No process referenced in §3–§5 is absent from §2. |
| 2 | `impact_classification` | Every process in §2 has a classification in §3: Added, Modified, Removed, or Unchanged-Dependent. No process is unclassified. |
| 3 | `role_mapping` | Every affected process has at least one role identified in §4 (who performs it today, who performs it after the change). Roles are teams or job functions, not individuals. |
| 4 | `change_scope` | For each Modified or Removed process: specific changed steps are identified in §4. For each Added process: full workflow steps are defined. No "TBD" entries without a resolution plan and target date. |
| 5 | `upstream_traceability` | Every impact classification in §3 cites a specific SAD component or TDD design decision. No impact is asserted without a source reference. |

---

## Scope Boundaries

- PIA scope is bounded by the SAD/TDD. Do not include speculative process impacts beyond what the solution defines.
- "No process impact" is a valid PIA outcome. If the initiative has no process implications, the PIA must contain an explicit "no process impact" declaration with justification referencing the SAD/TDD scope. This passes all hard gates.
- PIA does not define how to transition users (that is the Transition Plan's scope).
- PIA does not collect evidence of readiness (that is the Readiness Confirmation's scope).
