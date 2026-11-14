# Domain Rules

## Rule status

Rules directly derived from project guardrails are **Approved principles**. Operational rules are **Proposed**. Formula-specific rules remain **Unresolved**.

## A. Authority and calculations

- **DR-001 — Approved:** Deterministic backend calculations are authoritative.
- **DR-002 — Proposed:** The same normalized input and rule-set version must produce the same structured result.
- **DR-003 — Proposed:** Authoritative calculations use decimal arithmetic with explicit precision and rounding at defined boundaries.
- **DR-004 — Proposed:** Every stored result identifies its rule-set version and canonical input fingerprint.
- **DR-005 — Proposed:** Client calculations, if any, are previews and cannot be submitted as authoritative results.
- **DR-006 — Proposed:** Invalid or incomplete calculation inputs produce structured validation findings and block submission/approval.
- **DR-007 — Unresolved:** Estimate dimensions, formula, aggregation, thresholds, units, rounding mode, and treatment of null/zero/negative values.
- **DR-008 — Unresolved:** Whether old proposals retain their original rule set or recalculate under a new one.

## B. Baselines and changes

- **DR-101 — Proposed:** A baseline becomes effective only through explicit human approval.
- **DR-102 — Proposed:** Approved baseline snapshots are immutable and versioned per project.
- **DR-103 — Proposed:** Draft edits never mutate an approved baseline.
- **DR-104 — Proposed:** A change request pins an exact base baseline and an exact submitted revision.
- **DR-105 — Proposed:** An approved change creates a new baseline version; it does not edit the prior version.
- **DR-106 — Proposed:** Rejection changes no baseline.
- **DR-107 — Proposed:** Approval is atomic with the resulting baseline and audit event.
- **DR-108 — Unresolved:** Definition of consequential versus non-consequential changes. Safe default: treat every baseline-affecting change as consequential.
- **DR-109 — Unresolved:** Multiple concurrent requests, rebase, merge, withdrawal, and supersession behavior.

## C. Approval and identity

- **DR-201 — Approved principle:** Consequential changes require human approval.
- **DR-202 — Proposed:** The backend derives the actor from authenticated server context; it never trusts actor IDs in command payloads.
- **DR-203 — Proposed:** A decision names the exact target version and fails on version/state mismatch.
- **DR-204 — Proposed:** Decisions are terminal and append-only; corrections use a new compensating workflow rather than record edits.
- **DR-205 — Unresolved:** Who may submit/approve, self-approval, separation of duties, rationale requirements, and delegated approval.
- **DR-206 — Unresolved:** Authentication mechanism and whether attribution-only mode is acceptable in V1.0.

## D. AI explanations

- **DR-301 — Approved:** AI may explain grounded findings only.
- **DR-302 — Approved:** AI is not authoritative for calculations.
- **DR-303 — Approved principle:** AI cannot make or apply consequential decisions.
- **DR-304 — Proposed:** AI receives an allow-listed evidence envelope, not unrestricted database or conversation context.
- **DR-305 — Proposed:** Explanation claims must reference supplied finding IDs or clearly be labeled general wording; unsupported numeric claims are rejected or omitted.
- **DR-306 — Proposed:** AI output is stored/rendered separately from authoritative findings and labeled non-authoritative.
- **DR-307 — Proposed:** AI failure, absence, or refusal cannot block deterministic workflows.
- **DR-308 — Proposed:** Generating an explanation is read-only with respect to domain state.
- **DR-309 — Unresolved:** Whether AI is included, which free/local provider/model is approved, what data may be sent, and whether outputs are retained.

## E. Audit and time

- **DR-401 — Proposed:** Submission, approval, rejection, baseline activation, archival, and relevant policy changes emit append-only audit events.
- **DR-402 — Proposed:** Server time in UTC is authoritative for event ordering; display timezone does not change stored timestamps.
- **DR-403 — Proposed:** Audit records contain necessary attribution and references, not full sensitive payloads by default.
- **DR-404 — Unresolved:** Retention, deletion, legal/privacy obligations, and administrator access.

## Lifecycle proposals

```text
Initial scope: draft → submitted → approved
                          └──────→ rejected

Change request: draft → submitted → approved
                      │           └→ rejected
                      └→ withdrawn (unresolved)
```

Illegal transitions return a conflict, not a silent no-op. Editing a submitted target should create a new revision or require withdrawal; the choice is unresolved.

## Required formula specification template

Before calculation implementation, product ownership must provide:

1. named inputs, data types, units, valid ranges, and missing-value rules;
2. normalization and per-item formula;
3. aggregation and dependency/hierarchy behavior;
4. precision, rounding mode, and when rounding occurs;
5. delta and percentage behavior, including zero denominators;
6. severity/threshold rules;
7. at least one normal and boundary example for every rule;
8. rule-set version and change/migration policy.

