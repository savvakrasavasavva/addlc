# ADDLC metrics

Four families (MET-02), always reported **per change class and autonomy level**, against a pre-agent baseline (MET-01). Autonomy decisions are made from these numbers (MET-03).

## Flow

| Metric | Definition |
|---|---|
| Lead time for data | Intent gate to data in production, broken down by phase |
| Human effort per change | Hours by role: owner, steward, engineer, operator |
| Throughput | Changes or integrations released per period, per team |

## Stability and trust

| Metric | Definition |
|---|---|
| Change failure rate | Share of releases causing an incident, rollback or correction |
| Data downtime | Incidents x (time to detection + time to resolution) |
| Consumer-detected share | Share of incidents first reported by consumers rather than monitoring |
| Escaped defects per gate | Defects found after the gate that should have caught them |

## Agent effectiveness

| Metric | Definition |
|---|---|
| First-pass yield per gate | Share of agent-produced packages passing Meaning / Evidence / Operability without rework |
| Human review minutes per change | Read together with escaped defects: minutes trending to zero with a flat defect rate is rubber-stamping |
| Escalation rate and quality | Did the agent ask the right questions, with evidence |
| Cost per change | Tokens + compute + human time |

## Context health

| Metric | Definition |
|---|---|
| Coverage | Share of assets with an owner, a contract and glossary-linked semantics |
| Freshness | Age of skills and standards relative to the last relevant incident |
| Learning rate | Share of incidents and rejected gates that produced a context update (CTX-09) |

## Reporting table

| Period | Change class | Level | Lead time | Effort h | Throughput | CFR | Downtime | Consumer-detected | Escapes | First-pass | Review min | Cost | Coverage |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| | | | | | | | | | | | | | |

**Not success metrics** (MET-04): generated lines of code, pipelines created, share of code written by AI. They reward sprawl.

---
*Template: Apache-2.0.*
