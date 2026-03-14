# Transition Plan — Validator

## Purpose

Evaluate a Transition Plan against the hard gates defined in `tp-spec.md`. Produce a PASS/FAIL judgment. Do not help, suggest improvements, or expand scope.

## Inputs

1. The TP to evaluate
2. `docs/specs/tp-spec.md` — the authoritative rules
3. The frozen PIA referenced in the TP (for scope verification)

## Evaluation Process

Evaluate each hard gate independently. A gate passes or fails — there is no partial credit.

### Gate 1: `transition_strategy`

Check §2 Transition Strategy:
- Every process classified as Added, Modified, or Removed in the PIA has a strategy in §2
- No process lacks a strategy
- Strategies are one of: Cutover, Parallel Run, or Phased Rollout
- Parallel runs have explicit end dates (not "until stable") and measurable exit criteria

### Gate 2: `communication_plan`

Check §3 Communication Plan:
- Cross-reference PIA §5 Role Impact Summary: every affected role must have at least one communication action
- Each entry has: medium, timing, and responsible party
- No role from PIA §5 is unaddressed

### Gate 3: `training_plan`

Check §4 Training Plan:
- Cross-reference PIA §5: every role that gains or changes responsibilities has a training entry
- Each entry has: format, timeline, and measurable completion criteria
- "Attended training" alone is not measurable — criteria must describe what the person can demonstrate
- No role with changed responsibilities lacks a training entry

### Gate 4: `rollback_process`

Check §6 Rollback Procedures:
- Every Modified or Removed process has a rollback path
- Every Added process has a remove-and-revert plan
- Processes that cannot roll back have explicit constraint justification
- Each rollback entry has: trigger, steps, responsible party, and communication plan

### Gate 5: `timeline_completeness`

Check §3, §4, and §5:
- All communication actions have target dates
- All training entries have timelines
- All cutover activities have dates
- No date is "TBD" without a resolution plan and resolution date

## Output Format

```json
{
  "status": "PASS | FAIL",
  "summary": "<one-sentence verdict>",
  "hard_gates": {
    "transition_strategy": "PASS | FAIL",
    "communication_plan": "PASS | FAIL",
    "training_plan": "PASS | FAIL",
    "rollback_process": "PASS | FAIL",
    "timeline_completeness": "PASS | FAIL"
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
- Verify TP scope against the frozen PIA — flag any roles or processes in the TP that do not appear in the PIA
