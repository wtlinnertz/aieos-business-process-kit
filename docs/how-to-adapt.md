# How to Adapt the Business Process Kit

This guide helps organizations adopt and customize BPK for their context.

---

## What to Customize

### Principles File

`docs/principles/business-process-principles.md` contains the organizational policy for business process governance. Customize this to reflect your organization's change management standards, training requirements, and stakeholder communication norms.

Common adaptations:
- Adjusting training completion criteria thresholds (e.g., "90% completion rate acceptable" vs. "100% required")
- Adding organization-specific SOP formats or locations
- Defining which roles count as "process owners" in your organization
- Adding industry-specific process change requirements (e.g., healthcare workflow validation, financial services audit trails)

### Hard Gate Thresholds

The specs define the structural requirements. If your organization needs stricter or lighter governance:
- Add hard gates for regulatory process change requirements (e.g., FDA process validation)
- Adjust the SOP requirement if your organization doesn't use formal SOPs

### Adoption Criteria

BPK is optional. Define your organization's criteria for when BPK should be adopted:
- Always for Preset 1 (New Feature) and Preset 3 (Compliance)
- Conditionally for Preset 2 (Enhancement) — only when user-facing behavior changes
- Rarely for Preset 4 (Performance Fix) — only when the fix changes operational procedures

---

## What Not to Customize

- **Four-file structure** — every artifact type must have exactly spec, template, prompt, validator
- **Hard gate evaluation format** — validators must produce standardized JSON output
- **Freeze-before-promote** — PIA must be frozen before TP; TP must be frozen before RC
- **Session separation** — generation and validation must be separate AI sessions
- **Governance model** — `docs/governance-model.md` is a synchronized copy; do not edit directly

---

## Integration with Existing Change Management

If your organization already has a change management process (ITIL CAB, SAFe change enablement, etc.), BPK artifacts can serve as the structured inputs to those processes:

- PIA maps to a change impact assessment
- TP maps to a change implementation plan
- RC maps to a change readiness review

BPK does not replace your change management process — it provides the structured, governed artifacts that feed into it.
