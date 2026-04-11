# Business Process Kit — Playbook

This playbook defines the end-to-end process for the Business Process Kit (Layer 15). It covers how to move from a frozen SAD/TDD through process impact assessment, transition planning, and readiness confirmation.

---

## Artifact Flow

```
Trigger: SAD or TDD frozen (EEK, Layer 4)
         │ Solution shape is clear enough to identify process impacts
         ▼
Step 1: Process Impact Assessment (PIA) — generated
         │ Validate → Freeze
         ▼
Step 2: Transition Plan (TP) — generated
         │ Validate → Freeze
         ▼
Step 3: Readiness Confirmation (RC) — collected
         │ Validate → Freeze
         ▼
Output: RC readiness declaration informs REK entry decision
```

---

## Upstream Interface

**Upstream:** Engineering Execution Kit (EEK), Layer 4
**Input:** Frozen SAD (system architecture) and/or frozen TDD (technical design)

BPK is triggered when EEK artifacts reveal changes that affect business processes, user workflows, or operational procedures. See `docs/entry-from-eek.md` for the boundary contract.

The SAD provides component boundaries that map to process boundaries, integration points that imply process handoffs, and new/changed system capabilities. The TDD provides detailed behavior changes, UI changes, API changes that affect user workflows, and data model changes that affect data entry or reporting processes.

### Decision: Is BPK Needed?

Not every initiative affects business processes. Ask: "Does this change how someone does their job?"

- Backend performance optimization → probably no
- New user-facing workflow → yes
- API redesign with downstream manual consumers → yes
- Infrastructure migration with no user-visible changes → probably no

If the answer is no, document the decision explicitly in the ER: "BPK not adopted — no process-affecting changes identified in SAD/TDD."

---

## Step 1 — Process Impact Assessment (PIA)

**Artifact:** Process Impact Assessment (PIA)
**Type:** Generated
**Spec:** `docs/specs/pia-spec.md` (5 hard gates)
**Template:** `docs/artifacts/pia-template.md`
**Prompt:** `docs/prompts/pia-prompt.md`
**Validator:** `docs/validators/pia-validator.md`

### Purpose

Identify every business process affected by the initiative, classify the nature of each impact, and map which roles are affected.

### Inputs

- Frozen SAD from EEK
- Frozen TDD from EEK (if available — PIA can start after SAD alone)
- Frozen DPRD from PIK (recommended, for user context)
- Existing process documentation from the consuming project (if available)

### Process

1. Open a new AI session.
2. Provide: frozen SAD + frozen TDD (if available) + DPRD (if available) + existing process docs (if available) + `pia-spec.md` + `pia-template.md`. Use the PIA prompt.
3. Review the generated PIA. Confirm every impact is traceable to a SAD component or TDD decision.
4. Validate in a separate session using `pia-validator.md` and the spec.
5. On PASS: review and freeze the PIA.
6. On FAIL: correct and re-validate (see convergence loop in `aieos-governance-foundation/docs/review-convergence-loop.md`).

### Special Case: No Process Impact

If the initiative has no process implications, the PIA must contain an explicit "no process impact" declaration with justification referencing the SAD/TDD scope. This is a valid PIA that passes all hard gates. No TP or RC is required.

### PIA Re-Entry After TDD

If the PIA was generated after SAD freeze but before TDD freeze, review the PIA after TDD freezes. If the TDD reveals additional process impacts not covered in the PIA, issue a new PIA version via re-entry.

---

## Step 2 — Transition Plan (TP)

**Artifact:** Transition Plan (TP)
**Type:** Generated
**Spec:** `docs/specs/tp-spec.md` (5 hard gates)
**Template:** `docs/artifacts/tp-template.md`
**Prompt:** `docs/prompts/tp-prompt.md`
**Validator:** `docs/validators/tp-validator.md`

### Purpose

Define how affected users and teams move from current-state to future-state processes.

### Inputs

- Frozen PIA from BPK
- Frozen SAD from EEK (recommended)
- Frozen TDD from EEK (recommended)
- Release timeline from REK (if available, for schedule alignment)

### Process

1. Open a new AI session.
2. Provide: frozen PIA + SAD + TDD (recommended) + release timeline (if available) + `tp-spec.md` + `tp-template.md`. Use the TP prompt.
3. Review the generated TP. Confirm every affected process and role from the PIA is addressed.
4. Validate in a separate session using `tp-validator.md` and the spec.
5. On PASS: review and freeze the TP.
6. On FAIL: correct and re-validate.

### Schedule Alignment with REK

The TP cutover schedule should align with the REK Release Plan timing. If the RP is not yet frozen when the TP is generated, note the dependency. Update the TP cutover schedule when RP timing is confirmed, if dates diverge.

---

## Step 3 — Readiness Confirmation (RC)

**Artifact:** Readiness Confirmation (RC)
**Type:** Collected (evidence-based, not generated from scratch)
**Spec:** `docs/specs/rc-spec.md` (4 hard gates)
**Template:** `docs/artifacts/rc-template.md`
**Prompt:** `docs/prompts/rc-prompt.md`
**Validator:** `docs/validators/rc-validator.md`

### Purpose

Capture evidence that affected teams are actually prepared for the process changes.

### Inputs

- Frozen TP from BPK
- Frozen PIA from BPK
- Training completion records from the consuming project
- Updated SOPs from the consuming project
- Stakeholder acknowledgments from the consuming project

### Process

1. Execute the transition activities defined in the TP (communication, training, SOP updates).
2. Collect evidence of completion: training records, SOP references, acknowledgment logs.
3. Open a new AI session. Provide: frozen PIA + frozen TP + collected evidence + `rc-spec.md` + `rc-template.md`. Use the RC prompt.
4. Review the generated RC. Confirm the readiness declaration matches the evidence.
5. Validate in a separate session using `rc-validator.md` and the spec.
6. On PASS: review and freeze the RC.
7. On FAIL: address gaps and re-validate.

### Timing

RC should be completed before or parallel with REK entry (RER generation). The RC readiness declaration informs the release entry decision:

- **Ready** — proceed to REK
- **Ready-with-conditions** — proceed to REK with documented conditions tracked as open items
- **Not Ready** — REK entry should wait until blocking gaps are resolved. Proceeding with a "Not Ready" RC is a risk acceptance decision that should be documented in the ER.

---

## Downstream Handoff

BPK does not formally gate REK entry via a hard dependency edge. Instead, the RC readiness declaration is an advisory input to the REK Release Entry Record. The release owner makes the final call.

The TP cutover schedule should be cross-referenced in the REK Release Plan to ensure process transition activities are coordinated with the technical release.

---

## Freeze Points

| Artifact | When Frozen | What It Gates |
|----------|------------|---------------|
| PIA | After PIA validation PASS | TP generation |
| TP | After TP validation PASS | RC collection |
| RC | After RC validation PASS | Informs REK entry decision |

---

## Session Discipline

| Rule | Why |
|------|-----|
| Separate generation and validation sessions | Prevents self-validation bias |
| Include full upstream artifacts | Do not summarize; the AI needs complete context |
| Include spec and template for generation | The AI generates against the spec, not from memory |
| Include spec and validator for validation | The validator judges against the spec |

---

## Re-Entry Protocol

### PIA Re-Entry

If the SAD or TDD is revised after PIA freeze, assess whether the revision affects process impacts:
- If yes: generate a new PIA version against the updated SAD/TDD. The old PIA is superseded.
- If no: no action required.

### TP Re-Entry

If the PIA is revised after TP freeze, the TP must be revised to reflect the updated process scope. Generate a new TP version.

### RC Re-Entry

If the TP is revised after RC freeze, the RC must be reassessed. New or changed training/communication/SOP requirements need fresh evidence.

---

## Maintaining the Engagement Record

The Engagement Record (ER) is a project-level artifact that lives in the consuming project at `docs/engagement/er-{initiative}.md`. It spans all AIEOS layers and is maintained by each kit's operators as work passes through. The ER spec and format are defined in `aieos-governance-foundation/docs/engagement-record-spec.md`.

**BPK maintains the Layer 15 section of the ER.**

### What to Update During Business Process Operations

| Trigger | ER Update |
|---------|-----------|
| BPK adoption decision | If not adopted, write "BPK not adopted — {justification}" in §15 |
| PIA frozen | Add PIA ID to §15 artifact table |
| TP frozen | Add TP ID to §15 artifact table |
| RC frozen | Add RC ID to §15 artifact table; note readiness declaration |
| Key decision: process impact re-entry | Record in §15 key decisions |
| Key decision: release with "Not Ready" RC | Record risk acceptance in §15 key decisions |
