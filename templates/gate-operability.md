# Operability gate checklist

**Question:** can the Run side operate this without its authors?
**Accountable decider:** DataOps (Run) lead (GATE-04). If the Run side does not accept, the Build side keeps the pager (GATE-05).

- [ ] Owner, escalation path and on-call defined
- [ ] Runbook covers each known failure class
- [ ] Alerts fire end to end into the correct queue; noise within budget (OPS-05)
- [ ] Run-agent skills triage a seeded failure correctly, using only the provided skills
- [ ] Historical incidents replayed, or a test alert fired end to end
- [ ] Operator access verified against the access scenario
- [ ] Rollback plan tested; automatic rollback criteria defined (PHS-08)
- [ ] Contract, classification and license attached (OPS-02)
- [ ] Expected capacity and cost stated
- [ ] Early-life support window agreed - 30 days or one full event cycle, whichever is longer (PHS-07)

**Outcomes:** accepted / accepted with dated gaps / accepted for specific failure classes only / not accepted (Build keeps the pager).

Decision record (GATE-03): decider, outcome, evidence version, date.

---
*Template: Apache-2.0.*
