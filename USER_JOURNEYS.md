# User Journeys

These journeys are **Proposed** and depend on confirmation of the product hypothesis and roles.

## Journey 1 — Create and approve the initial baseline

**Actor:** Editor, then Approver  
**Precondition:** The actor can access a project workspace.

1. Editor creates a project.
2. Editor adds structured scope items and estimate inputs.
3. The backend validates inputs and returns deterministic totals plus validation findings.
4. Editor corrects blocking findings and submits the draft.
5. Submission captures a candidate snapshot; later draft edits must not alter what the approver sees.
6. Approver reviews scope, totals, rule-set version, and any optional grounded explanation.
7. Approver explicitly approves or rejects, optionally/mandatorily giving a rationale (unresolved).
8. Approval atomically creates baseline version 1 and an audit event. Rejection returns the candidate to a defined state (unresolved).

**Guardrails:** AI cannot submit or approve. A calculation failure blocks submission. Approval acts on an exact version, not “latest” mutable data.

## Journey 2 — Propose a scope change

**Actor:** Editor  
**Precondition:** An approved current baseline exists.

1. Editor starts a change request pinned to the current baseline version.
2. Editor adds, changes, or marks scope items for removal in the proposal.
3. The backend builds a deterministic before/after comparison.
4. The backend calculates revised totals and deltas using the approved rule-set version policy (policy unresolved).
5. The UI displays changed fields, impact findings, and calculation metadata separately from generated explanation.
6. Editor submits the exact proposal version for approval.

**Failure paths:** Invalid values return field errors. If the base baseline is no longer current, submission or approval fails with a stale-baseline conflict until the rebase policy is resolved.

## Journey 3 — Decide a change request

**Actor:** Approver

1. Approver opens a submitted request.
2. The UI shows the pinned baseline, proposal, deterministic delta, and any warnings.
3. Approver may request an AI explanation. The request includes only allow-listed stored facts and findings.
4. The explanation is labeled non-authoritative and cites finding identifiers; absence/failure does not block the decision.
5. Approver approves or rejects the exact submitted revision.
6. Approval atomically creates the next baseline version, makes it current, closes the request, and records the decision. Rejection records the decision without changing the baseline.

**Guardrails:** No AI output can invoke the decision endpoint. A stale revision returns HTTP 409. The actor and timestamp come from trusted server context, not client fields.

## Journey 4 — Inspect history and reproduce a finding

**Actor:** Viewer

1. Viewer opens project history.
2. Viewer selects a baseline or change-request version.
3. The system shows immutable input snapshots, decision history, calculation outputs, and rule-set version.
4. An authorized user may request recalculation for diagnosis, but historical recorded results are not overwritten; comparison behavior is unresolved.

## Journey 5 — Work without AI

**Actor:** Any user

1. AI is disabled, unconfigured, or unavailable.
2. All project, scope, calculation, comparison, submission, approval, rejection, and history functions continue.
3. Explanation controls are absent or show a non-blocking unavailable state.

## Cross-journey UX requirements — Proposed

- Always distinguish draft, submitted, approved, rejected, superseded, and stale states.
- Display authoritative numeric findings before explanatory prose.
- Confirm consequential actions and describe their effects.
- Disable decisions when data is invalid, stale, or still calculating.
- Never imply that AI has approved, verified, or guaranteed a result.
- Preserve user-entered drafts after recoverable validation errors.

## Unresolved journey questions

- Is there a separate project owner or administrator?
- Can the author approve their own submission?
- Can multiple open change requests target the same baseline, and how are they rebased?
- Can a submitted request be withdrawn or edited, or must a new revision be created?
- Is rejection rationale required? Can a rejected request be resubmitted?
- What does project archival/deletion do to history?
- Are notifications, export, and comment threads excluded from V1.0?

