# Process Impact Assessment — Validator

## Purpose

Evaluate a Process Impact Assessment against the hard gates defined in `pia-spec.md`. Produce a PASS/FAIL judgment. Do not help, suggest improvements, or expand scope.

## Inputs

1. The PIA to evaluate
2. `docs/specs/pia-spec.md` — the authoritative rules
3. The frozen SAD and/or TDD referenced in the PIA (for traceability verification)

## Evaluation Process

Evaluate each hard gate independently. A gate passes or fails — there is no partial credit.

### Gate 1: `process_inventory`

Check §2 Process Inventory:
- Every business process referenced anywhere in §3–§5 must appear in §2
- Each entry must have: process name, process owner (team/role, not individual), frequency, and current description
- No referenced process is missing from the inventory

### Gate 2: `impact_classification`

Check §3 Impact Classification:
- Every process listed in §2 has a classification: Added, Modified, Removed, or Unchanged-Dependent
- No process is unclassified
- Classifications are one of the four defined types (no custom categories)

### Gate 3: `role_mapping`

Check §4 Impact Detail:
- Every affected process has at least one role identified
- Roles are described as teams or job functions, not individual names
- Both current and future role assignments are identified where applicable

### Gate 4: `change_scope`

Check §4 Impact Detail:
- For each Modified or Removed process: specific steps that change are identified
- For each Added process: full workflow steps are defined
- No "TBD" entries exist without a resolution plan and target date

### Gate 5: `upstream_traceability`

Check §3 Impact Classification:
- Every impact classification cites a specific SAD component or TDD design decision
- Source references are specific (e.g., "SAD §4.2 Payment Gateway Component") not vague (e.g., "the architecture")
- No impact is asserted without a source reference

## Special Case: "No Process Impact" PIA

If the PIA declares no process impacts:
- The declaration must include explicit justification referencing the SAD/TDD scope
- The justification must explain why the technical changes do not affect any business processes
- All hard gates pass if the justification is present and references the source documents

## Output Format

```json
{
  "status": "PASS | FAIL",
  "summary": "<one-sentence verdict>",
  "hard_gates": {
    "process_inventory": "PASS | FAIL",
    "impact_classification": "PASS | FAIL",
    "role_mapping": "PASS | FAIL",
    "change_scope": "PASS | FAIL",
    "upstream_traceability": "PASS | FAIL"
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
- If a gate fails, describe what is missing or incorrect — do not prescribe how to fix it
