# ADDLC terminology

Normative terms and definitions. Part of the [ADDLC specification](addlc-spec.md).

## Actors

- **Human (actor)** - holder of decision rights: intent, meaning, acceptance, exceptions. Typical roles: data product owner, data steward, data engineer (architect and supervisor of agents), DataOps operator, consumer.
- **Agent** - an AI system holding execution rights only: it drafts, builds, tests, documents, triages and proposes. Build, verify and run agents are separate identities with separate permissions.
- **Controls** - deterministic enforcement: CI pipelines, contract validators, policy as code, access control, quality gates, promotion rules. Controls do not use judgment and cannot be persuaded.

## Lifecycle

- **Loop** - one of three cycles of the model: Intent (Frame, Specify), Delivery (Build, Verify, Release), Run (Operate, Evolve & Retire).
- **Phase** - one of the seven stages: Frame, Specify, Build, Verify, Release, Operate, Evolve & Retire.
- **Gate** - a decision point passed on evidence, with exactly one accountable decider: Intent, Meaning, Evidence, Operability.
- **Exit artifact** - the record a phase must leave behind (intent brief, specification package, change set, evidence pack, handover package, decision records).
- **Risk tier** - the risk class of a work item, derived from data criticality, reversibility and blast radius; sets the strictness of every gate.

## Specification and context

- **Specification package** - the system of record for a change: data contract, semantic definitions linked to glossary terms, canonical-model mapping, quality expectations with thresholds and severities, acceptance examples.
- **Acceptance examples** - concrete input-output cases that any correct implementation must reproduce.
- **Context layer** - everything an agent knows about the organization: glossary, domain and semantic models, contracts, standards, instruction files, skills.
- **Deviation register** - the record of SHOULD-level requirements a conforming scope deviates from, with rationale (comply or explain).

## Autonomy

- **Change class** - a category of change with a shared risk profile, such as "new Bronze ingestion from a known source type".
- **Change-class owner** - the person accountable for a change class: its autonomy level, its low-tier releases and the audits of delegated changes.
- **Autonomy level** - one of six: **Manual** (no agent involvement), **Assist** (agent suggests, human authors), **Draft** (agent authors, human reviews every change), **Supervised** (agent executes end to end, humans decide at gates and sample-review), **Delegated** (agent releases without a human, controls enforce, humans audit after the fact, rollback automatic), **Self-organizing** (agents reorganize the asset graph within policy; humans own meaning and policy).
- **Autonomy ceiling** - the highest level a change class may reach, set by reversibility, blast radius and criticality. A *hard ceiling* cannot be lifted by promotion runs.
- **Escaped defect (escape)** - a defect found after the gate that should have caught it.

## Verification and operations

- **Evidence pack** - the artifacts showing an implementation satisfies its spec: test results and coverage, reconciliation report, verifier findings, sample sign-off, cost.
- **First-pass yield** - the share of packages that pass a gate without rework.
- **Reconciliation** - comparison against an independent source or a known invariant (totals, counts, identities, temporal rules).
- **Verifier agent** - an independent agent with its own instructions (ideally a different model) that sees the spec and the output, never the builder's reasoning.
- **Handover package** - what the Run side needs to operate a product without its authors.
- **Incident classes** - defect (implementation wrong), data correction (code right, data wrong), decision (a guard fired on a legitimate event), spec gap (reality produced a case the spec never described).
- **Data downtime** - number of incidents x (time to detection + time to resolution).
- **Consumer-detected share** - the share of incidents first reported by consumers rather than monitoring.

## Master and reference data

- **Golden record** - the published, survivorship-resolved master record.
- **Survivorship** - the rules deciding which source values form the golden record.
- **Stewarded change channel** - the isolated, auditable and reversible path for correcting master and reference data, with four-eyes approval for high-criticality entities.
- **Steward queue** - the queue receiving sub-threshold candidate matches and failed records, with evidence.
- **Certify, don't delete** - the publication rule: quality rules decide what is published, not what exists; failing records stay below the published layer with quality flags.

---

*(c) Savva Lukhnev, [CC BY 4.0](../LICENSES/CC-BY-4.0.txt).*
