# Contributing

Disagreement backed by practice is the most useful contribution. The fastest way to improve ADDLC is to tell where it broke in a real team.

## Most wanted

- Change classes and autonomy ceilings from your domain - what you capped, and why.
- Gate criteria that worked, or failed, in real teams.
- Metric baselines from before and after agents.
- Where the model breaks: streaming, unstructured data, ML features.

## How

- **Experience reports and disagreements:** open an issue. Say what you ran, what happened, what you would change.
- **Text changes:** a pull request against `spec/` or `templates/`. For normative changes, state the requirement ID, the proposed keyword (MUST/SHOULD/MAY) and level, and the evidence.
- **New templates:** pull request with a note on where it was used.

## Rules for normative text

- Requirements are testable: an auditor must be able to answer yes or no.
- RFC 2119 keywords in capitals, one requirement per ID, levels per spec section 6.
- Spec text stays vendor-neutral; product names appear only as examples, never in requirements.

## Credit and licensing

Material improvements are credited in the changelog and the next revision of the companion article. By contributing you agree your contribution is licensed under the repository's licenses (spec text CC BY 4.0, templates Apache-2.0).
