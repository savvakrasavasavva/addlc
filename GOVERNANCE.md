# Governance

## Current model

The specification has a single editor, Savva Lukhnev, who decides what is folded into each revision. Material contributions are credited in the changelog and the article's next revision. If the model attracts independent implementers, governance moves to a small steering group of practitioners who have actually run it, with the editor as one voice.

## Versioning

The specification uses semantic versioning:

- **Major** - a MUST or MUST NOT requirement added, removed or materially changed, a conformance level redefined, or any other change that alters what an existing conformance claim means.
- **Minor** - new SHOULD or MAY requirements, new informative material, clarifications that do not change the outcome of any MUST-level conformance assessment.
- **Patch** - editorial fixes.

Conformance claims must name the exact version assessed against.

## Changing the specification

1. Open an issue describing the problem: a requirement that failed in practice, an ambiguity, a missing case. Evidence from a real team beats argument.
2. Discussion happens in the issue. Significant proposals may be asked to include: the requirement text proposed, its level, and what evidence would show it working.
3. The editor merges accepted changes, updates the requirement index and the changelog, and bumps the version.

## Out of scope for changes

- Making the model vendor-specific. ADDLC stays implementable on any stack.
- Removing human decision rights over intent, meaning and acceptance. That split is the model.
