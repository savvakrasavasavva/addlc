# ADDLC self-assessment

Answer yes or no for one scope (a team, a domain or a set of data products). Your level is the highest one for which every answer at that level and below is yes. If any Assisted answer is no, you are at Ad hoc. Requirement IDs refer to [the specification](../spec/addlc-spec.md).

## Level 1 - Assisted

| # | Question | Req |
|---|---|---|
| 1.1 | Do agents work from shared, versioned instruction files and standards? | CTX-01 |
| 1.2 | Is every agent-produced change either reviewed by a human before production, or released under a change class holding the Delegated level granted per AUT-02..05? | AUT-01 |
| 1.3 | Can you tell which changes were produced by agents? | SEG-02 |
| 1.4 | Do agents run under their own identities, not personal human credentials? | SEG-01 |
| 1.5 | Does every change have one accountable human owner, do humans hold all gate decisions, and is every agent action attributable and reconstructable? | ACT-01, ACT-02, ACT-04 |
| 1.6 | Is a risk tier assigned to every work item at Frame? | PHS-02 |
| 1.7 | Is the actor that built a change never the sole source of the evidence used to accept it? | ACT-03 |

## Level 2 - Spec-driven

| # | Question | Req |
|---|---|---|
| 2.1 | Is a specification (contract, semantics, expectations, acceptance examples) approved before building starts? | CTX-02, CTX-03 |
| 2.2 | Are all four gates defined, each with one accountable decider, deterministic automated checks before human review, and recorded decisions? | GATE-01..04, ACT-05 |
| 2.3 | Do build and run agents use separate identities, with no shared human credentials, and no production credentials or write access in Build? | SEG-03..05 |
| 2.4 | Are acceptance tests derived from the spec, outside the builder's context, and does no actor certify its own work? | VER-02, ACT-03 |
| 2.5 | Do licensed fields reach external models only after a license and entitlement check at the Meaning gate? | LIC-01, LIC-02 |
| 2.6 | Is there a handover package, and does the Build side keep the pager until Run accepts? | OPS-02, GATE-05 |
| 2.7 | Do you have a pre-agent baseline for lead time, effort and incidents? | MET-01 |
| 2.8 | Are changes to CI rules, thresholds, policy as code and agent permissions capped at Assist? | AUT-06 |
| 2.9 | Does build happen outside production? | PHS-04 |
| 2.10 | Is a reuse search recorded before the Intent gate, with the reuse report part of the Meaning gate evidence? | CTX-07, CTX-10 |
| 2.11 | Does every release have a tested rollback plan, and are schema evolution and retirement governed by contract versioning and deprecation windows? | PHS-08, PHS-09 |
| 2.12 | Is the specification the system of record, with one authoritative source per artifact and no silent overwriting of human edits by regeneration? | CTX-04, CTX-06 |
| 2.13 | Does the lifecycle cover all seven phases with their exit artifacts, and does every change originating in Run re-enter the Delivery loop under Build identities? | PHS-01, PHS-03, PHS-06 |
| 2.14 | Does verification produce an evidence pack, do acceptance examples run unchanged, and does a human accept medium- and high-tier results on a sample? | VER-01, VER-03, VER-06 |
| 2.15 | Is an agent that reads untrusted content prevented, by a deterministic control, from also holding private-data access and the ability to communicate externally? | SEG-06 |
| 2.16 | Are released products observable across freshness, volume, distribution, schema and lineage, with alerts routed to a defined queue and every suppression rule carrying an expiry date? | OPS-01, OPS-05 |

## Level 3 - Governed autonomy

| # | Question | Req |
|---|---|---|
| 3.1 | Is autonomy assigned per change class, with written promotion rules and automatic demotion on escapes? | AUT-02..05 |
| 3.2 | Do run agents triage incidents, and are incidents classified as defect, data correction, decision or spec gap, each on its own fix path? | OPS-03, OPS-04 |
| 3.3 | Does every escaped defect or rejected gate produce a context update (or a recorded decision not to)? | CTX-09 |
| 3.4 | Is the context layer owned and versioned? | CTX-08 |
| 3.5 | Are autonomy decisions made from per-class metrics rather than opinions? | MET-02, MET-03 |
| 3.6 | For change classes at the Delegated level, do controls enforce the Evidence gate automatically, and does the change-class owner audit delegated changes after the fact? | GATE-06 |

## MRD profile (required at Level 2 and above if the scope contains master or reference data)

| # | Question | Req |
|---|---|---|
| M.1 | Are matching, survivorship and identifier-mapping rules decided at the Meaning gate with steward approval, and capped at Draft as a hard ceiling? | MRD-01 |
| M.2 | Do master-data corrections go only through an auditable, reversible stewarded channel, with four-eyes approval for high-criticality entities? | MRD-02, MRD-03 |
| M.3 | Is every identity-touching release reconciled against at least one independent source before cutover? | MRD-04 |
| M.4 | Do candidate matches stay below the published layer until survivorship produces the golden record, with sub-threshold matches routed to the steward queue? | MRD-05 |

## Scoring

- **Below Level 1** (the article's "Ad hoc") - any Level 1 answer is no.
- **Level N** - every answer at level N and below is yes, SHOULD-deviations are in the deviation register.
- Record the result as: `ADDLC v1.0.0 self-assessment: Level 2 (Spec-driven), MRD profile: satisfied, date, scope`.

---

*Template: Apache-2.0. The normative requirements in [the specification](../spec/addlc-spec.md) govern.*
