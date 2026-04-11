# Business Process Principles

**Version:** v1.0

These principles guide how AIEOS governs business process changes alongside technical solution delivery. They apply to all BPK artifacts (PIA, TP, RC).

---

## Principle 1: Process Change is a Deliverable

Process changes caused by a system change are part of the solution scope. A solution that ships without governing its process impacts is incomplete, not fast. Technical readiness without process readiness is a partial delivery.

---

## Principle 2: Affected Roles Must Be Identified Early

Identifying who is affected is not a post-release activity. Role impact analysis happens when the solution shape is known (SAD/TDD), not after go-live. Late discovery of process impacts creates emergency training, ad-hoc workarounds, and adoption failures.

---

## Principle 3: Training Must Be Measurable

"Sent a training email" is not training completion. "Attended a session" is awareness, not competence. Training effectiveness requires measurable completion criteria: quiz scores, demonstrated task execution, or supervisor sign-off. If you cannot verify someone can do the new thing, you have not trained them.

---

## Principle 4: Parallel Runs Have Explicit End Dates

Running old and new processes simultaneously is a transition strategy, not a permanent state. Parallel runs must have defined duration and measurable exit criteria. Without an end date, parallel runs become permanent dual maintenance — doubling the operational burden they were meant to eliminate.

---

## Principle 5: Readiness Is Evidence-Based

"The team says they are ready" is not readiness evidence. Readiness is demonstrated through documented training completion, updated SOPs, and stakeholder acknowledgment. The Readiness Confirmation captures what has been done, not what is planned or assumed.

---

## Principle 6: Rollback Must Be Planned

Process changes must have a reversion path. If the technical system rolls back, the process must be able to roll back too. If a process cannot revert to the previous state (regulatory mandate, one-way data migration), this must be explicitly documented as a constraint — not discovered during an incident.
