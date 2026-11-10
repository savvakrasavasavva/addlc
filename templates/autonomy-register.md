# Autonomy register

One row per change class (AUT-02, AUT-03). Levels: Manual, Assist, Draft, Supervised, Delegated, Self-organizing. A level is assigned to a change class, never to an agent.

## Register

| Change class | Owner | Risk factors (reversibility / blast radius / criticality) | Ceiling | Current level | Clean-run bar | Current streak |
|---|---|---|---|---|---|---|
| Descriptions and docs, Bronze/Silver | | high / low / low | Delegated | | e.g. 20 | |
| Descriptions of Gold and glossary-linked fields | | | Supervised (meaning) | | | |
| Incident triage and evidence gathering (read-only) | | | Delegated | | | |
| New Bronze ingestion, known source type and template | | | Supervised | | | |
| New or changed Silver transformation | | | Supervised | | | |
| Change to a certified Gold metric definition | | | Draft | | | |
| Matching / survivorship / identifier-mapping rules (MRD) | | | **Draft - hard ceiling** (MRD-01) | | | |
| Correction of master records in production (MRD) | | | **Assist - hard ceiling**, stewarded channel (MRD-03) | | | |
| Changes to controls: CI rules, thresholds, policy as code, agent permissions | | | **Assist - hard ceiling** (AUT-06) | | | |

## Promotion rule (AUT-04)

A class moves up one level only after `N` consecutive changes that passed every gate first time with no escaped defects. `N` scales with risk: 20 clean changes bound the failure rate only to about 15% - acceptable for documentation, far too weak for identity rules.

| Risk tier | Suggested N |
|---|---|
| low | 20 |
| medium | 50 |
| high | 100+, plus an explicit owner decision |

## Demotion rule (AUT-05)

Any escaped defect above severity `S` demotes the class by one level automatically and resets the streak.

## Promotion / demotion log (MET-03: decisions from metrics)

| Date | Change class | From -> To | Trigger (streak reached / escape id) | Metrics cited | Decider |
|---|---|---|---|---|---|
| | | | | | |

---
*Template: Apache-2.0. The example ceilings are illustrative; set your own per AUT-03.*
