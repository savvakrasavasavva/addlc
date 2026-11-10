# ADDLC Specification

**The Agentic Data Development Lifecycle - normative specification**

| | |
|---|---|
| Version | 1.0.0 |
| Status | Current version, released 2026-11-10 |
| Editor | Savva Lukhnev |
| Narrative companion | [The Agentic Data Development Lifecycle (ADDLC)](https://medium.com/@savvakrasava/agentic-data-development-lifecycle-addlc-d40122a46e2c) |
| License | [CC BY 4.0](../LICENSES/CC-BY-4.0.txt) |

---

## 1. Status of this document

This document is the normative specification of ADDLC. It defines the requirements so that a team can adopt the model, claim conformance and be audited against the claim. The narrative rationale, worked examples and mapping to the data management canon live in the companion article and are informative.

Feedback is invited through the issue tracker of this repository. Material improvements are folded into the next revision, with credit. Versioning and the change process are defined in [GOVERNANCE.md](../GOVERNANCE.md).

## 2. Scope

This specification applies to the development and operation of data products - ingestion, integration, transformation, master and reference data, and data operations - in organizations where AI agents perform a substantial share of the execution and humans retain decision rights over intent, meaning and acceptance.

It defines:

- decision rights between humans, agents and controls;
- a lifecycle of seven phases with mandatory exit artifacts;
- four gates with evidence criteria and accountable deciders;
- an autonomy policy assigned per change class;
- segregation requirements for Build and Run;
- additional requirements for master and reference data (the MRD profile);
- metrics and conformance levels.

It does not prescribe tools, platforms or architectures. Any stack can implement it. It is not an ISO standard; it is designed to sit alongside ISO/IEC 5338, ISO/IEC 42001, the ISO/IEC 5259 series and ISO 8000, covering what they leave open: how data products are built and run when agents do most of the execution.

## 3. Normative language

The key words MUST, MUST NOT, REQUIRED, SHALL, SHALL NOT, SHOULD, SHOULD NOT, RECOMMENDED, NOT RECOMMENDED, MAY, and OPTIONAL in this document are to be interpreted as described in BCP 14 (RFC 2119, RFC 8174) when, and only when, they appear in all capitals.

**Comply or explain.** A conforming implementation that deviates from a SHOULD or SHOULD NOT requirement MUST record the deviation in a deviation register that is available to auditors of the conformance claim. Each register entry MUST record the requirement ID, the deviation, the rationale, the date and the accountable owner.

## 4. Terms and definitions

The definitions in [terminology.md](terminology.md) are normative and part of this specification.

## 5. The model (informative)

ADDLC is built from 3 actors, 3 loops, 7 phases and 4 gates (Figure 1 in [figures/](../figures/)).

- **Actors:** humans decide (intent, meaning, acceptance, exceptions); agents propose (draft, build, test, document, triage); controls enforce (CI, contract validation, policy as code, access control, promotion rules).
- **Loops and phases:** the Intent loop (Frame, Specify), the Delivery loop (Build, Verify, Release) and the Run loop (Operate, Evolve & Retire).
- **Gates:** Intent, Meaning, Evidence, Operability.

The operating rule in one line: **agents propose, controls enforce, humans decide.** The specification is the hinge between the loops: Delivery cannot start without an approved spec, and Run reopens the spec when reality disagrees with it.

## 6. Conformance

### 6.1 Conformance levels

| Level | Name | Meaning |
|---|---|---|
| 1 | **Assisted** | Agents draft under full human review, with shared context, agent attribution and human decision rights. |
| 2 | **Spec-driven** | Specifications are the system of record; all four gates operate with evidence packs; Build and Run identities are segregated; a baseline exists. Includes Level 1. |
| 3 | **Governed autonomy** | Autonomy is assigned per change class and moves on evidence; run agents triage; context is owned and tested; metrics drive autonomy decisions. Includes Level 2. |
| MRD | **MRD profile** | Additive profile, mandatory for any conformance scope at Level 2 or higher that contains master or reference data. |

The maturity level *Self-organizing* described in the companion article is out of the scope of conformance in this version.

### 6.2 Conformance claims

- The unit of a conformance claim is a **scope**: a team, a domain or a set of data products - not an entire company by default. A claim MUST name its scope.
- A scope conforms to a level when it satisfies every MUST and MUST NOT requirement tagged at that level and below, and treats every SHOULD/SHOULD NOT per the comply-or-explain rule (section 3).
- A claim at Level 2 or higher whose scope includes master or reference data MUST also satisfy the MRD profile.
- Claim format: `Conforms to ADDLC v1.0.0, Level 2 (Spec-driven), MRD profile; deviations: <register reference>.` A claim MUST name the exact version assessed against.

### 6.3 Self-assessment

[conformance/self-assessment.md](../conformance/self-assessment.md) provides a yes/no questionnaire mapped to requirement IDs. It is informative; the requirements in section 7 govern.

## 7. Requirements

Each requirement has an identifier, a keyword and the level at which it first applies. Requirements apply at the level shown and at all higher levels.

### 7.1 Actors and decision rights (ACT)

- **ACT-01** (MUST, L1) Decision rights over intent, meaning, acceptance and exceptions MUST be held by identified humans. An agent MUST NOT be the accountable decider at any gate.
- **ACT-02** (MUST, L1) Every change MUST have exactly one accountable human owner: the data product owner or the change-class owner.
- **ACT-03** (MUST, L1) No actor may certify its own work. The actor that built a change MUST NOT be the sole source of the evidence used to accept it.
- **ACT-04** (MUST, L1) Every agent action MUST be attributable (which agent identity, on whose behalf), explainable (which spec or decision it traces to) and reconstructable (inputs, tool calls, outputs).
- **ACT-05** (MUST, L2) Controls MUST be deterministic. A gate decision MUST NOT rest on the judgment of a non-deterministic component alone.

### 7.2 Specification and context (CTX)

- **CTX-01** (MUST, L1) Agents MUST work from shared, versioned instruction files and standards, not from ad hoc prompts alone.
- **CTX-02** (MUST, L2) A specification package MUST be approved at the Meaning gate before implementation of a change begins. For low-risk change classes the package MAY be the minimum viable form: a filled spec template and acceptance examples.
- **CTX-03** (MUST, L2) Except as permitted by CTX-02 for low-risk change classes, the specification package MUST include: a data contract; semantic definitions linked to glossary terms, or fields explicitly marked local; the mapping to the canonical model where one exists; quality expectations with thresholds and severities per dimension; and acceptance examples - concrete input-output cases any correct implementation must reproduce.
- **CTX-04** (MUST, L2) The specification is the system of record. When implementation and specification disagree, one of them MUST be formally changed; neither wins silently.
- **CTX-05** (SHOULD, L2) The data contract SHOULD use an open, machine-validatable format (for example the Open Data Contract Standard).
- **CTX-06** (MUST, L2) Every artifact MUST have exactly one authoritative source. Regeneration MUST NOT silently overwrite human edits.
- **CTX-07** (SHOULD, L1) Before a new asset is created, an agent or human SHOULD search for existing assets that fulfill the need and record why building new is justified (reuse before you generate).
- **CTX-08** (MUST, L3) The context layer - glossary, domain model, contracts, standards, instruction files, skills - MUST have named owners and version control, and SHOULD be tested like a product.
- **CTX-09** (MUST, L3) Every escaped defect and every rejected gate MUST produce either a context update (skill, standard, glossary entry, test template) or a recorded decision not to update.
- **CTX-10** (MUST, L2) A new asset MUST NOT pass the Intent gate without a recorded reuse search: the existing assets that could fulfill the need, and why extending them is worse than building new. The reuse report MUST be part of the Meaning gate evidence.

### 7.3 Phases and exit artifacts (PHS)

- **PHS-01** (MUST, L2) The lifecycle MUST cover the seven phases: Frame, Specify, Build, Verify, Release, Operate, Evolve & Retire. Local names MAY differ; the mapping MUST be documented.
- **PHS-02** (MUST, L1) A risk tier MUST be assigned at Frame for every work item, derived from data criticality, reversibility and blast radius. The tier sets the strictness of every later gate.
- **PHS-03** (MUST, L2) Each phase MUST produce its exit artifacts: intent brief (Frame); approved specification package (Specify); change set with spec-derived tests, documentation and lineage, linked to a spec version (Build); evidence pack (Verify); released versioned product and accepted handover package (Release); incident and decision records plus context updates (Operate); consolidation and retirement decisions and new contract versions (Evolve & Retire).
- **PHS-04** (MUST, L2) Build MUST take place outside production. Build data SHOULD be sampled, masked or synthetic.
- **PHS-05** (SHOULD, L2) Certify, don't delete: quality rules SHOULD decide what is published, not what exists. Conformed records that fail quality checks stay one layer below the published layer with quality flags and go to the steward queue with evidence, instead of being discarded.
- **PHS-06** (MUST, L2) Any change originating in the Run loop - a consolidation, a contract version, a fix - MUST re-enter the Delivery loop under Build identities. Run proposes; Build implements.
- **PHS-07** (SHOULD, L2) Early-life support: the authors SHOULD remain on call for an agreed window after release - 30 days or one full event cycle of the domain, whichever is longer.
- **PHS-08** (MUST, L2) Every release MUST have a tested rollback plan and defined automatic rollback criteria. Consumer cutover SHOULD be atomic: consumers are switched only if no contract changed during verification.
- **PHS-09** (MUST, L2) Schema evolution and retirement MUST be governed by contract versioning, deprecation windows and consumer impact analysis from lineage.

### 7.4 Gates (GATE)

- **GATE-01** (MUST, L2) Four gates MUST operate: Intent (after Frame), Meaning (after Specify), Evidence (after Verify) and Operability (at Release). Gates MAY ride on existing mechanics - a spec pull request, required CI checks, a production-readiness review - provided the requirements below hold.
- **GATE-02** (MUST, L2) Each gate MUST have exactly one accountable decider, a defined evidence pack, automated checks that run before any human review, and explicit outcomes.
- **GATE-03** (MUST, L2) A gate MUST be passed on evidence, and every gate decision - pass or rejection - MUST be recorded: outcome, decider, evidence version, date.
- **GATE-04** (MUST, L2) Accountable deciders: Intent gate - the data product owner; Meaning gate - the data product owner, and for master and reference data additionally the data steward, whose approval is required; Evidence gate - for medium and high tiers, a release approver who did not author the change, for low tiers the change-class owner; Operability gate - the DataOps (Run) lead.
- **GATE-05** (MUST, L2) The Operability gate MUST verify that the Run side can operate the product without its authors, using the handover package and an operational test. If the Run side does not accept, the Build side MUST keep operational responsibility (the pager).
- **GATE-06** (MUST, L3) For change classes at the Delegated level, controls MUST enforce the Evidence gate automatically, and the change-class owner MUST audit delegated changes after the fact.
- **GATE-07** (SHOULD, L3) Gates SHOULD have quality control of their own: approval rate and review depth tracked per gate, and a periodic re-review of a sample of approved packs, to detect rubber-stamping.
- **GATE-08** (SHOULD, L2) For low-risk change classes the lifecycle SHOULD collapse to a minimum viable form - spec template, spec-derived tests, automated checks at the Evidence gate, a named change-class owner as decider. If gates cost more human time than the work they protect, the risk tiering is wrong. Unattended release remains subject to AUT-01.

### 7.5 Verification and evidence (VER)

- **VER-01** (MUST, L2) Verification MUST produce an evidence pack: test results with coverage against the spec's expectations, reconciliation report, verifier findings (if a verifier agent is used), sample sign-off where required, and the cost of the run.
- **VER-02** (MUST, L2) Tests used as acceptance evidence MUST be derived from the specification in a context that does not see the implementation, and MUST NOT be authored by the same agent context that authored the implementation.
- **VER-03** (MUST, L2) Acceptance examples from the specification MUST run unchanged against the implementation.
- **VER-04** (SHOULD, L2) Verification SHOULD include reconciliation against an independent source or a known invariant (totals, counts, identities, temporal rules). For identity-touching releases in the MRD profile this becomes MRD-04 (MUST).
- **VER-05** (MAY, L2) An independent verifier agent MAY be used: its own instructions, ideally a different model; it sees the spec and the output, never the builder's reasoning. If a verifier agent is used, its findings MUST NOT replace deterministic checks or reconciliation - they supplement them.
- **VER-06** (MUST, L2) For medium and high risk tiers, a human MUST accept the result on a sample: the consumer, or the steward for master and reference data.

### 7.6 Autonomy (AUT)

- **AUT-01** (MUST, L1) Every agent-produced change MUST be reviewed by a human before it reaches production, unless its change class holds the Delegated level granted under the full autonomy machinery of this specification (AUT-02..AUT-05 and GATE-06). In practice this means unattended release is available only at Level 3.
- **AUT-02** (MUST, L3) Autonomy MUST be assigned per change class - never to an agent, a team or an organization as a whole. The six levels are Manual, Assist, Draft, Supervised, Delegated, Self-organizing; local names MAY differ if the semantics map one-to-one.
- **AUT-03** (MUST, L3) Every change class MUST have a documented autonomy ceiling derived from reversibility, blast radius and data criticality.
- **AUT-04** (MUST, L3) Promotion rules MUST be written down: a class moves up one level only after an agreed run of consecutive changes that passed every gate first time with no escaped defects. The length of the run MUST scale with the risk of the class.
- **AUT-05** (MUST, L3) Demotion MUST be automatic: an escaped defect above an agreed severity demotes the class by one level and resets the promotion count.
- **AUT-06** (MUST, L2) Changes to the controls themselves - CI rules, test thresholds, policy as code, agent permissions - MUST be capped at Assist. An agent MUST NOT be able to modify its own gates or permissions.

### 7.7 Identities and segregation (SEG)

- **SEG-01** (MUST, L1) Agents MUST run under their own identities, not under personal human credentials. Agent credentials SHOULD be scoped and short-lived.
- **SEG-02** (MUST, L1) It MUST be possible to tell which changes were produced by agents.
- **SEG-03** (MUST, L2) Build and Run MUST be segregated for humans and agents alike: separate identities, separate credentials, separate queues. This separates permissions, not accountability - a team that builds and runs its own product still uses separate Build and Run identities.
- **SEG-04** (MUST, L2) Build agents MUST NOT have write access to production data. Run agents MUST NOT change code or models.
- **SEG-05** (MUST, L2) Production credentials MUST NOT be available in build environments.
- **SEG-06** (MUST, L2) An agent that reads untrusted content (vendor emails, web pages, tickets) MUST NOT simultaneously hold access to private or licensed data and the ability to communicate externally, unless a deterministic control breaks the combination: untrusted content is sanitized or quarantined before the agent reads it, or external communication is blocked or held for human approval (the lethal trifecta rule).

### 7.8 Licensing and entitlements (LIC)

- **LIC-01** (MUST, L2) License terms and entitlements MUST travel with the data as metadata, and agents MUST read and propagate them.
- **LIC-02** (MUST, L2) Moving licensed data to a new consumer is a Meaning-gate decision. A model provider that processes licensed data is itself a consumer of that data: licensed fields MUST NOT reach a model outside the organization's perimeter without a license and entitlement check at the Meaning gate.
- **LIC-03** (SHOULD, L2) Deployments where the model provider neither retains nor trains on inputs SHOULD be preferred for licensed data.

### 7.9 Operations (OPS)

- **OPS-01** (MUST, L2) Released products MUST be observable across freshness, volume, distribution, schema and lineage, with alerts routed to a defined queue.
- **OPS-02** (MUST, L2) The handover package MUST contain: ownership and escalation path; data flow; runbook; alerts mapped to each known failure mode and routed to the right queue; operational skills that let run agents triage the product, where run agents are used; operator access; quality rules and tests; contract, classification and license; expected capacity and cost.
- **OPS-03** (MUST, L3) Incidents MUST be classified - defect, data correction, decision, or spec gap - and each class MUST follow its own fix path: defects re-enter the Delivery loop; data corrections go through the stewarded change channel; decisions are made by a human on agent-prepared evidence; spec gaps reopen Specify.
- **OPS-04** (SHOULD, L3) Run agents SHOULD operate read-mostly: deduplicate alerts, gather evidence, run root-cause analysis, classify incidents and draft fixes - while fixes themselves follow OPS-03 paths.
- **OPS-05** (MUST, L2) Alert suppression rules MUST have expiry dates. Alert noise SHOULD be managed against an explicit budget.

### 7.10 Metrics (MET)

- **MET-01** (MUST, L2) A baseline for lead time, human effort per change and the incident profile MUST be measured before any change class is granted a level above Draft. Where pre-agent historical data exists, it MUST be used as the baseline.
- **MET-02** (MUST, L3) Metrics MUST be reported per change class and autonomy level, covering four families: flow (lead time for data, human effort per change by role, throughput); stability and trust (change failure rate, data downtime, consumer-detected share, escaped defects per gate); agent effectiveness (first-pass yield per gate, human review minutes per change, escalation rate and quality, cost per change); context health (coverage, freshness, learning rate).
- **MET-03** (MUST, L3) Autonomy promotion and demotion decisions MUST be made from these metrics, not from opinions or demos.
- **MET-04** (SHOULD NOT, L1) Generated lines of code, the number of pipelines created and the share of code written by AI SHOULD NOT be used as success metrics. They reward sprawl.

### 7.11 MRD profile - master and reference data (MRD)

Mandatory for any conformance scope at Level 2 or higher that contains master or reference data (section 6.2).

- **MRD-01** (MUST) Matching, survivorship and identifier-mapping rules are meaning: they MUST be decided at the Meaning gate with steward approval, and the change class that modifies them MUST be capped at Draft - a hard ceiling that no promotion run can lift.
- **MRD-02** (MUST) Corrections of master records in production MUST go only through a stewarded change channel that is: isolated from code deployment; validated by the same contracts as the pipeline; attributable (who, what, why, on whose request); reversible (versioned or bitemporal storage, so any correction can be undone and any past state reconstructed); and subject to four-eyes approval for high-criticality entities. Nobody - human or agent - edits master data through a code path or an ad hoc SQL session.
- **MRD-03** (MUST) The change class for master-record corrections MUST be capped at Assist: agents prepare corrections with evidence; humans approve them.
- **MRD-04** (MUST) Every release that touches identity MUST be reconciled against at least one independent source before cutover.
- **MRD-05** (MUST) Agent-proposed candidate matches MUST carry confidence scores; matches above the steward-approved threshold MAY be applied under the approved rules; everything below MUST go to the steward queue with evidence. Candidate matches stay in the layer below the published (Gold) layer until survivorship produces the golden record.

## 8. Requirement index by level

| Level | MUST / MUST NOT | SHOULD / SHOULD NOT / MAY |
|---|---|---|
| **1 - Assisted** | ACT-01..04, CTX-01, PHS-02, AUT-01, SEG-01, SEG-02 | CTX-07, MET-04, SEG-01 (credential scoping) |
| **2 - Spec-driven** (adds) | ACT-05, CTX-02..04, CTX-06, CTX-10, PHS-01, PHS-03, PHS-04 (outside production), PHS-06, PHS-08 (rollback), PHS-09, GATE-01..05, VER-01..03, VER-05 (no replacement, when used), VER-06, AUT-06, SEG-03..06, LIC-01, LIC-02, OPS-01, OPS-02, OPS-05 (expiry), MET-01 | CTX-05, PHS-04 (data form), PHS-05, PHS-07, PHS-08 (atomic cutover), GATE-08, VER-04, VER-05 (MAY, use of a verifier), LIC-03, OPS-05 (budget) |
| **3 - Governed autonomy** (adds) | CTX-08 (ownership, versioning), CTX-09, GATE-06, AUT-02..05, OPS-03, MET-02, MET-03 | CTX-08 (testing), GATE-07, OPS-04 |
| **MRD profile** (adds, mandatory at Level 2+ for master/reference data scopes) | MRD-01..05 | - |

## 9. References

**Normative**

1. RFC 2119, RFC 8174 (BCP 14). Key words for use in RFCs to indicate requirement levels.
2. [terminology.md](terminology.md) - terms and definitions of this specification.

**Informative**

3. Lukhnev, S. "The Agentic Data Development Lifecycle (ADDLC)". Medium, November 2026 - the narrative companion, with rationale, prior art review, anti-patterns, the 90-day adoption path and the mapping to DAMA-DMBOK, Data Mesh, Data Management at Scale, Fundamentals of Data Engineering, Data Quality Fundamentals and Designing Data-Intensive Applications.
4. Bitol (LF AI & Data). Open Data Contract Standard.
5. SAE International. J3016_202104 - the levels-of-automation shape borrowed for autonomy levels.
6. ISO/IEC 5338:2023; ISO/IEC 42001:2023; ISO/IEC 5259 series; ISO 8000 series.
7. Willison, S. "The lethal trifecta for AI agents". June 2025.
8. Dengsøe, M. "The Agentic Data Development Lifecycle in Practice". Coalesce, October 2026 - prior use of the name, for a workflow anchored in one product; the companion article's prior-art review (section 2) credits it and explains how this specification differs.

---

*Text of this specification: (c) Savva Lukhnev, licensed under [CC BY 4.0](../LICENSES/CC-BY-4.0.txt).*
