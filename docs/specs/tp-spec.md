# Transition Plan — Spec

**Artifact type:** Transition Plan (TP)
**Kit:** Business Process Kit (BPK), Layer 15
Version: v1.0

---

## Purpose

The Transition Plan defines how affected users and teams move from current-state to future-state processes. It covers transition strategy, communication, training, scheduling, and rollback procedures.

---

## Artifact ID Format

`TP-{INITIATIVE}-{NNN}`

Example: `TP-TASKFLOW-001`

---

## Trigger

Generate a TP when the PIA is frozen and contains at least one process classified as Added, Modified, or Removed.

If the PIA concluded with "no process impact," no TP is required.

---

## Inputs

| Input | Source | Required |
|-------|--------|----------|
| Frozen PIA | BPK | Yes |
| Frozen SAD | EEK | Recommended (for system context) |
| Frozen TDD | EEK | Recommended (for behavioral detail) |
| Release timeline | REK (if available) | Recommended (for schedule alignment) |

---

## Sections

### §1 Document Control

| Field | Value |
|-------|-------|
| TP ID | `TP-{INITIATIVE}-{NNN}` |
| Initiative | Full initiative name |
| Owner | Team or role responsible for transition execution |
| Version | Document version |
| Status | Draft / Validated / Frozen |
| PIA Reference | PIA artifact ID |
| Governance Model Version | Version of governance model in effect |
| Prompt Version | Version of the prompt used to generate this artifact |
| Spec Version | v1.0 |
| Principles Version | business-process-principles v1.0 |

### §2 Transition Strategy

For each process classified as Added, Modified, or Removed in the PIA:

| Process | Strategy | Rationale | Duration |
|---------|----------|-----------|----------|
| {name} | Cutover / Parallel Run / Phased Rollout | {why this strategy} | {duration for parallel runs; N/A for cutover} |

Strategy definitions:
- **Cutover** — Hard switch from old process to new on a specific date. Old process ceases.
- **Parallel Run** — Both old and new processes operate simultaneously for a defined period. Requires explicit end date and exit criteria.
- **Phased Rollout** — Incremental migration by group, region, or cohort. Requires phase definitions with dates.

Parallel run durations must have explicit end dates, not "until stable." Exit criteria must be measurable.

### §3 Communication Plan

Every affected role identified in the PIA §5 must have at least one communication action.

| Role | Communication Action | Medium | Timing | Responsible Party |
|------|---------------------|--------|--------|------------------|
| {role} | {what is communicated} | {email/meeting/doc/etc.} | {date or relative timing} | {who sends it} |

Communication actions must include: what is changing, when it changes, what the recipient needs to do differently, and where to get help.

### §4 Training Plan

Every role that gains or changes responsibilities (per PIA §5) must have training identified.

| Role | Training Content | Format | Timeline | Completion Criteria |
|------|-----------------|--------|----------|-------------------|
| {role} | {what they need to learn} | {self-serve doc / live session / shadowing / workshop} | {date range} | {measurable criteria} |

Completion criteria must be measurable. Examples: "completed quiz with 80%+ score," "demonstrated 3 successful transactions," "supervisor sign-off after shadowed session." "Attended training" alone is not sufficient.

### §5 Cutover Schedule

A timeline of all transition activities with dates and owners.

| Phase | Activity | Date | Owner | Dependencies |
|-------|----------|------|-------|-------------|
| Pre-cutover | {activity} | {date} | {who} | {what must be done first} |
| Cutover | {activity} | {date} | {who} | {what must be done first} |
| Post-cutover | {activity} | {date} | {who} | {what must be done first} |

The cutover schedule must align with the REK Release Plan timing when available. If the RP is not yet frozen, note the dependency and update the TP when RP timing is known.

### §6 Rollback Procedures

For each Modified or Removed process, a rollback path is defined.

| Process | Rollback Trigger | Rollback Steps | Responsible Party | Rollback Communication |
|---------|-----------------|---------------|-------------------|----------------------|
| {name} | {what triggers a rollback} | {how to revert} | {who executes} | {how affected users are notified} |

For Added processes, define a "remove and revert" plan: how to deactivate the new process and what users do instead.

If a process cannot revert to the previous state (e.g., regulatory mandate, data migration is one-way), document this explicitly with the constraint justification. Not every process needs a rollback path, but the absence of one must be a deliberate decision.

---

## Hard Gates

| # | Gate | Rule |
|---|------|------|
| 1 | `transition_strategy` | Every process classified as Added, Modified, or Removed in the PIA has a strategy declared in §2. No process lacks a strategy. Parallel runs have explicit end dates and measurable exit criteria. |
| 2 | `communication_plan` | Every affected role from PIA §5 has at least one communication action in §3 with medium, timing, and responsible party. No role is unaddressed. |
| 3 | `training_plan` | Every role that gains or changes responsibilities has training identified in §4 with format, timeline, and measurable completion criteria. No role with changed responsibilities lacks a training entry. |
| 4 | `rollback_process` | For each Modified or Removed process, a rollback path is defined in §6. For Added processes, a remove-and-revert plan is defined. Processes that cannot roll back have explicit constraint justification. |
| 5 | `timeline_completeness` | All communication, training, and cutover activities in §3–§5 have target dates. No date is "TBD" without a resolution plan and resolution date. |

---

## Scope Boundaries

- TP scope is bounded by the frozen PIA. No roles or processes appear in the TP that are not in the PIA.
- TP does not define the technical release process (that is REK's scope).
- TP does not collect evidence of readiness (that is the Readiness Confirmation's scope).
- TP does not re-assess process impacts (that was done in the PIA). If new impacts are discovered during TP creation, the PIA must be revised first via re-entry.
