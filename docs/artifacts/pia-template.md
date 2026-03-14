# Process Impact Assessment

## §1 Document Control

| Field | Value |
|-------|-------|
| PIA ID | PIA-{INITIATIVE}-{NNN} |
| Initiative | {full initiative name} |
| Owner | {team or role — not an individual name} |
| Version | v1.0 |
| Status | Draft |
| SAD Reference | {SAD artifact ID} |
| TDD Reference | {TDD artifact ID, or N/A if not yet frozen} |
| Governance Model Version | {version from §15 of governance-model.md} |
| Prompt Version | {prompt file version used} |
| Spec Version | v1.0 |
| Principles Version | business-process-principles v1.0 |

---

## §2 Process Inventory

| Process Name | Process Owner | Frequency | Current Description |
|-------------|--------------|-----------|-------------------|
| {process name} | {team/role} | {daily/weekly/per-event/etc.} | {brief description of current-state process} |

---

## §3 Impact Classification

| Process | Classification | Source Reference |
|---------|---------------|-----------------|
| {process name} | Added / Modified / Removed / Unchanged-Dependent | {SAD §X / TDD §Y} |

---

## §4 Impact Detail

### {Process Name}

**Classification:** {Added / Modified / Removed / Unchanged-Dependent}

**Current steps** (Modified/Removed only):
1. {step}
2. {step}

**Future steps** (Added/Modified only):
1. {step}
2. {step}

**Changed roles:** {which roles gain, lose, or change responsibilities}

**Changed tools/systems:** {tools or systems introduced, replaced, or removed}

**Dependencies:** {upstream/downstream processes affected}

*(Repeat for each affected process)*

---

## §5 Role Impact Summary

| Role | Processes Gained | Processes Changed | Processes Lost | Net Impact |
|------|-----------------|------------------|---------------|------------|
| {role} | {list or "none"} | {list or "none"} | {list or "none"} | {brief summary} |

---

## §6 Risk and Mitigation

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| {description} | High / Medium / Low | {what goes wrong} | {mitigation approach} |
