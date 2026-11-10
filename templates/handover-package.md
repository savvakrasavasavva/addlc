# Handover package

What makes Build and Run separable (OPS-02). Assembled by agents in Release, accepted by the DataOps lead at the Operability gate.

| Section | Content | Done |
|---|---|---|
| Ownership | Product owner, change-class owner, escalation path, on-call | [ ] |
| Data flow | Sources, layers, consumers; lineage reference | [ ] |
| Runbook | One entry per known failure class: symptoms, diagnosis, fix path | [ ] |
| Alerts | Each known failure mode mapped to an alert, routed to the right queue; noise budget | [ ] |
| Operational skills | Instructions that let run agents triage this product (read-mostly, OPS-04) | [ ] |
| Operator access | Roles and credentials the Run side needs, verified | [ ] |
| Quality rules and tests | Expectations with thresholds and severities; where they run | [ ] |
| Contract, classification, license | Versioned contract; data classification; license and entitlements (LIC-01) | [ ] |
| Rollback | Tested rollback plan and automatic rollback criteria (PHS-08) | [ ] |
| Capacity and cost | Expected volumes, compute and spend | [ ] |
| Early-life support | Window agreed: 30 days or one full event cycle, whichever is longer (PHS-07) | [ ] |

## Operational test (run at the Operability gate)

- [ ] Replay one or more historical incidents
- [ ] Fire a test alert end to end into the queue
- [ ] Walk through the access scenario
- [ ] Let a run agent triage a seeded failure using only the provided skills

## Incident fix paths (OPS-03)

| Class | Meaning | Path |
|---|---|---|
| Defect | Implementation is wrong | Back to the Delivery loop as a change |
| Data correction | Code right, data wrong | Stewarded change channel |
| Decision | Guard fired on a legitimate event | Human call on agent-prepared evidence |
| Spec gap | Reality the spec never described | Reopen Specify |

---
*Template: Apache-2.0.*
