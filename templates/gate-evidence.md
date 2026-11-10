# Evidence gate checklist

**Question:** does the implementation demonstrably satisfy the spec?
**Accountable decider:** medium/high tiers - a release approver who did not author the change; low tiers - the change-class owner. Delegated classes: controls enforce automatically, the change-class owner audits after the fact (GATE-04, GATE-06).

- [ ] All spec-derived tests pass; coverage of the spec's expectations reported (VER-01)
- [ ] Tests were derived from the spec outside the builder's context (VER-02)
- [ ] Acceptance examples ran unchanged against the implementation (VER-03)
- [ ] Reconciliation against an independent source or invariant (VER-04; MUST for identity-touching MRD releases, MRD-04)
- [ ] Independent verifier findings resolved or explicitly accepted (if used, VER-05)
- [ ] Consumer (or steward) sample sign-off for medium and high tiers (VER-06)
- [ ] Cost of build and verification recorded

**Outcomes:** pass / pass with dated exceptions / fail - back to Build with findings.

Decision record (GATE-03): decider, outcome, evidence version, date.

---
*Template: Apache-2.0.*
