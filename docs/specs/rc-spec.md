# Readiness Confirmation — Spec

**Artifact type:** Readiness Confirmation (RC)
**Kit:** Business Process Kit (BPK), Layer 15
Version: v1.0

---

## Purpose

The Readiness Confirmation captures evidence that affected teams are actually prepared for the process changes defined in the PIA and planned in the TP. It is evidence-based, not aspirational — it records what has been done, not what is planned.

---

## Artifact ID Format

`RC-{INITIATIVE}-{NNN}`

Example: `RC-TASKFLOW-001`

---

## Trigger

Generate an RC when the TP is frozen and training, communication, and SOP updates have been executed. The RC should be completed before or parallel with REK entry.

---

## Inputs

| Input | Source | Required |
|-------|--------|----------|
| Frozen TP | BPK | Yes |
| Frozen PIA | BPK | Yes |
| Training completion records | Consuming project | Yes |
| Updated SOPs | Consuming project | If applicable |
| Stakeholder acknowledgments | Consuming project | Yes |

---

## Sections

### §1 Document Control

| Field | Value |
|-------|-------|
| RC ID | `RC-{INITIATIVE}-{NNN}` |
| Initiative | Full initiative name |
| Owner | Team or role responsible for readiness confirmation |
| Version | Document version |
| Status | Draft / Validated / Frozen |
| PIA Reference | PIA artifact ID |
| TP Reference | TP artifact ID |
| Governance Model Version | Version of governance model in effect |
| Prompt Version | Version of the prompt used to generate this artifact |
| Spec Version | v1.0 |
| Principles Version | business-process-principles v1.0 |

### §2 Training Completion Evidence

For every role with training requirements in the TP §4:

| Role | Required Training | Completion Date | Completion Rate | Evidence Reference |
|------|------------------|----------------|----------------|-------------------|
| {role} | {training content from TP} | {date completed} | {percentage of affected staff} | {certificate/quiz/sign-off reference} |

Completion rate is the percentage of affected staff who met the TP's completion criteria. A rate below 100% requires a note explaining the gap and remediation plan.

### §3 SOP Status

For every process classified as Modified or Added in the PIA:

| Process | SOP ID / Location | Status | Confirmed By |
|---------|------------------|--------|-------------|
| {name} | {SOP reference or location} | Updated / New / Not Applicable | {who confirmed} |

"Not Applicable" requires justification (e.g., "process is ad-hoc and does not have a formal SOP; team lead briefing substitutes").

### §4 Stakeholder Acknowledgment Log

For every process owner listed in the PIA §2:

| Process | Process Owner | Acknowledgment Date | Method | Reference |
|---------|-------------|-------------------|--------|-----------|
| {name} | {team/role} | {date} | {email/sign-off/meeting minutes} | {link or reference} |

Acknowledgment confirms the process owner understands the change, the timeline, and their responsibilities during transition.

### §5 Open Items

| Item | Severity | Owner | Resolution Plan | Target Date |
|------|----------|-------|----------------|-------------|
| {description} | Blocking / Non-blocking | {who} | {plan} | {date} |

If no open items exist, write "No open items" explicitly.

Blocking items prevent a "Ready" declaration. Non-blocking items with resolution plans allow "Ready-with-conditions."

### §6 Readiness Declaration

| Field | Value |
|-------|-------|
| Declaration | Ready / Ready-with-conditions / Not Ready |
| Justification | {brief rationale} |
| Conditions (if applicable) | {list of conditions that must be resolved} |

Declaration definitions:
- **Ready** — All training complete, SOPs updated, stakeholders acknowledged, no blocking open items.
- **Ready-with-conditions** — Core readiness achieved but non-blocking items remain with documented resolution plans. All conditions must have owners and target dates.
- **Not Ready** — Blocking gaps exist. Release entry (REK) should not proceed until resolved.

---

## Hard Gates

| # | Gate | Rule |
|---|------|------|
| 1 | `training_evidence` | Every role with training requirements in TP §4 has evidence in §2: completion date, completion rate, and evidence reference. No role with training requirements lacks evidence. |
| 2 | `sop_update_evidence` | Every Modified or Added process has an SOP entry in §3 with status and confirmation. "Not Applicable" entries have justification. |
| 3 | `stakeholder_acknowledgment` | Every process owner from PIA §2 has an acknowledgment entry in §4 with date, method, and reference. No process owner is unacknowledged. |
| 4 | `open_items` | All open items in §5 have an owner, resolution plan, and target date. Blocking items prevent a "Ready" declaration. If no open items exist, "No open items" is stated explicitly. |

---

## Scope Boundaries

- RC is evidence-based. It captures what has actually been done, not what is planned. Planning is the TP's scope.
- RC does not repeat PIA or TP content. It references them and provides evidence of execution.
- RC does not assess technical readiness (that is REK's scope via ORD and RER).
- "Ready-with-conditions" requires all conditions to be non-blocking with documented resolution plans and target dates.
- "Not Ready" informs the REK entry decision. It does not automatically block release — the release owner makes the final call with the RC findings as input. However, proceeding with a "Not Ready" RC is a risk acceptance decision that should be documented in the ER.
