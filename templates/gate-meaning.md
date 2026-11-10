# Meaning gate checklist

**Question:** do we agree on what this data means and what "good" looks like?
**Accountable decider:** data product owner. For master and reference data, the data steward's approval is also required (GATE-04, MRD-01).

- [ ] Contract validates against its schema; every field has a type, a description and a glossary link - or is explicitly marked local (CTX-03)
- [ ] Grain, keys and source precedence stated
- [ ] Survivorship rules stated and steward-approved (MRD scopes)
- [ ] Quality expectations: dimension, threshold, severity, owner - per expectation
- [ ] Acceptance examples cover normal, edge and known-bad cases (CTX-03)
- [ ] License and entitlement check done; new consumers of licensed data approved here (LIC-01, LIC-02)
- [ ] Canonical-model mapping present where a canonical model exists
- [ ] Reuse report attached (CTX-10)
- [ ] Open questions listed, each with an owner - they block release, not build

**Outcomes:** approved / approved with listed open questions (block release, not build) / rejected.

Decision record (GATE-03): decider, outcome, evidence version, date.

---
*Template: Apache-2.0.*
