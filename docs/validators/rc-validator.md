# Readiness Confirmation — Validator

## Purpose

Evaluate a Readiness Confirmation against the hard gates defined in `rc-spec.md`. Produce a PASS/FAIL judgment. Do not help, suggest improvements, or expand scope.

## Inputs

1. The RC to evaluate
2. `docs/specs/rc-spec.md` — the authoritative rules
3. The frozen TP referenced in the RC (for training requirements cross-reference)
4. The frozen PIA referenced in the RC (for process owner cross-reference)

## Evaluation Process

Evaluate each hard gate independently. A gate passes or fails — there is no partial credit.

### Gate 1: `training_evidence`

Check §2 Training Completion Evidence:
- Cross-reference TP §4: every role with training requirements has an entry in §2
- Each entry has: completion date, completion rate (percentage), and evidence reference
- No role with training requirements in the TP lacks evidence in the RC
- Completion rates below 100% must have an explanation

### Gate 2: `sop_update_evidence`

Check §3 SOP Status:
- Cross-reference PIA §3: every process classified as Modified or Added has an entry in §3
- Each entry has: SOP ID/location, status (Updated/New/Not Applicable), and confirmation
- "Not Applicable" entries have justification

### Gate 3: `stakeholder_acknowledgment`

Check §4 Stakeholder Acknowledgment Log:
- Cross-reference PIA §2: every process owner has an acknowledgment entry
- Each entry has: acknowledgment date, method, and reference
- No process owner from the PIA is unacknowledged

### Gate 4: `open_items`

Check §5 Open Items:
- If open items exist: each has an owner, resolution plan, and target date
- If no open items exist: "No open items" is stated explicitly (not an empty section)
- Blocking items are flagged and consistent with the §6 readiness declaration
- A "Ready" declaration with blocking open items is a FAIL

## Consistency Check

Verify that §6 Readiness Declaration is consistent with the evidence:
- "Ready" — no blocking open items, all training evidence present, all SOPs addressed, all stakeholders acknowledged
- "Ready-with-conditions" — no blocking open items, but non-blocking gaps exist with resolution plans
- "Not Ready" — blocking gaps exist

A declaration that contradicts the evidence is a FAIL on the relevant gate.

## Output Format

```json
{
  "status": "PASS | FAIL",
  "summary": "<one-sentence verdict>",
  "hard_gates": {
    "training_evidence": "PASS | FAIL",
    "sop_update_evidence": "PASS | FAIL",
    "stakeholder_acknowledgment": "PASS | FAIL",
    "open_items": "PASS | FAIL"
  },
  "blocking_issues": [
    {
      "gate": "<gate_name>",
      "description": "<what is wrong>",
      "location": "<section reference>"
    }
  ],
  "warnings": [
    {
      "description": "<non-blocking observation>",
      "location": "<section reference>"
    }
  ],
  "completeness_score": "<0-100>"
}
```

## Rules

- Do not suggest fixes or improvements
- Do not expand scope beyond what the spec requires
- Do not evaluate quality of writing or presentation
- Evaluate only against the hard gates in the spec
- Evidence must be present, not promised — the RC captures what has been done, not what will be done
