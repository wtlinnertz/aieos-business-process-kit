# How to use the business process kit with AI

This guide covers AI session setup for generating and validating BPK artifacts.

---

## General rules

1. **Separate generation and validation**. Never generate an artifact and validate it in the same AI session.
2. **Include full upstream artifacts**. Do not summarize the SAD, TDD, or PIA. Provide complete documents.
3. **Include the spec**. The AI generates and validates against the spec, not from memory.
4. **Include the template**. The AI follows the template structure for output.


## Session setup by artifact

### PIA generation session

Provide to the AI:
1. `docs/prompts/pia-prompt.md`
2. `docs/specs/pia-spec.md`
3. `docs/artifacts/pia-template.md`
4. `docs/principles/business-process-principles.md`
5. Frozen SAD (complete document)
6. Frozen TDD (complete document, if available)
7. Frozen DPRD (if available)
8. Existing process documentation (if available)

### PIA validation session

Provide to the AI:
1. `docs/validators/pia-validator.md`
2. `docs/specs/pia-spec.md`
3. The generated PIA
4. Frozen SAD and/or TDD (for traceability verification)

### TP generation session

Provide to the AI:
1. `docs/prompts/tp-prompt.md`
2. `docs/specs/tp-spec.md`
3. `docs/artifacts/tp-template.md`
4. `docs/principles/business-process-principles.md`
5. Frozen PIA (complete document)
6. Frozen SAD (recommended)
7. Frozen TDD (recommended)
8. Release timeline from REK (if available)

### TP validation session

Provide to the AI:
1. `docs/validators/tp-validator.md`
2. `docs/specs/tp-spec.md`
3. The generated TP
4. Frozen PIA (for scope cross-reference)

### RC generation session

Provide to the AI:
1. `docs/prompts/rc-prompt.md`
2. `docs/specs/rc-spec.md`
3. `docs/artifacts/rc-template.md`
4. `docs/principles/business-process-principles.md`
5. Frozen PIA (complete document)
6. Frozen TP (complete document)
7. Training completion records
8. Updated SOP references
9. Stakeholder acknowledgment records

### RC validation session

Provide to the AI:
1. `docs/validators/rc-validator.md`
2. `docs/specs/rc-spec.md`
3. The generated RC
4. Frozen TP (for training requirements cross-reference)
5. Frozen PIA (for process owner cross-reference)


## Tips

- **PIA is the foundation** - spend time getting the PIA right. The TP and RC are bounded by it.
- **Existing process docs help** - if you have current workflow documentation, SOPs, or process maps, provide them to the PIA session. The AI will produce better impact analysis with concrete current-state information.
- **RC is evidence collection, not generation** - the AI organizes evidence you provide, but the evidence itself (training records, acknowledgments) must come from real activities. The AI cannot fabricate readiness evidence.
