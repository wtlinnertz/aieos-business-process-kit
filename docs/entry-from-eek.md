# Boundary Briefing: EEK → BPK

## What You Receive

From the Engineering Execution Kit (Layer 4), BPK receives:

| Artifact | Required | What It Provides |
|----------|----------|-----------------|
| Frozen SAD | Yes (at least one of SAD or TDD) | Component boundaries, integration points, system capabilities — used to identify which business processes are affected |
| Frozen TDD | Yes (at least one of SAD or TDD) | Behavior changes, UI changes, API changes, data model changes — used to identify workflow-level process impacts |
| Frozen DPRD | Recommended | User context, problem framing — helps identify affected user groups and process contexts |

## Trigger Condition

BPK is triggered when a SAD or TDD is frozen **and** the solution introduces changes that affect business processes, user workflows, or operational procedures.

The decision to engage BPK is made by the initiative operator. The question is: "Does this change how someone does their job?" If the answer is uncertain, generate a PIA — a "no process impact" PIA is a valid and lightweight outcome.

## What You Need to Check Before Starting

1. The SAD and/or TDD is frozen (not just validated — frozen).
2. You have access to any existing process documentation for the affected domain.
3. You have identified the process owner(s) for the affected area — they will need to be consulted during PIA generation and acknowledged during RC.

## What BPK Produces

BPK artifacts do not flow back to EEK. They flow forward to inform REK:

- **PIA** — identifies affected processes and roles
- **TP** — defines the transition strategy, communication, training, and cutover schedule
- **RC** — confirms readiness, informing the REK release entry decision

## Relationship to Other Cross-Cutting Kits

BPK operates independently of other cross-cutting kits but may share timing:

- **DKK (Layer 13)** — DKK governs technical documentation (UDR, ARR). BPK governs process change documentation. They have different audiences but may reference each other (e.g., UDR may link to updated SOPs identified in the TP).
- **SCK (Layer 10)** — Compliance mandates may drive process changes. If the initiative is compliance-driven (Preset 3), the PIA should reference CER compliance requirements as context.
