# Implementation Plan

No application implementation is authorized by this Phase 0 document. This plan begins only after the relevant decision gates are approved.

## Guiding sequence

Build one vertical slice at a time through the modular monolith. Establish deterministic rules and approval integrity before optional AI. Do not create infrastructure for hypothetical scale.

## Phase 0 — Product and architecture decisions

**Deliverables:** the ten Phase 0 documents, approved product definition/scope, formula specification with golden examples, identity/approval policy, initial ADRs, and measurable acceptance criteria.

**Exit gate:** U-01 through U-08 and U-10 are resolved; AI may remain excluded/disabled if U-09 is unresolved. Product and technical owners explicitly approve proposed requirements promoted to approved.

## Phase 1 — Engineering foundation

- Create `frontend/` and `backend/` with selected free/open-source toolchains.
- Add environment validation, formatting, linting, type checks, tests, and migration tooling.
- Add local PostgreSQL orchestration and documented configuration.
- Establish API error envelope, request IDs, health endpoints, and CI.
- Record ADRs for authentication, persistence stack, package managers, and API concurrency/idempotency.

**Exit gate:** clean checkout setup works; empty app health/readiness and one database migration are actually verified; no business behavior is claimed.

## Phase 2 — Projects, scope drafts, and calculation engine

- Implement project access boundary and project metadata.
- Implement draft scope editing and validation.
- Implement pure, versioned deterministic calculation rules from approved examples.
- Add unit/property/boundary tests and backend contract tests.
- Render authoritative findings in the frontend.

**Exit gate:** every approved golden example passes; invalid input and rounding boundaries are covered; frontend does not become the authority.

## Phase 3 — Baseline submission and approval

- Freeze exact submission snapshots.
- Implement permission checks, optimistic concurrency, transactional decisions, immutable baseline versions, and audit events.
- Add integration tests for approve/reject, retry/idempotency, unauthorized access, stale versions, and rollback.

**Exit gate:** baseline cannot become effective without a valid human decision; audit/baseline consistency is demonstrated by tests.

## Phase 4 — Change requests and impact comparison

- Implement proposal editing and immutable submitted revisions.
- Produce field-level diff, recalculation, delta findings, and stale-baseline detection.
- Apply approved concurrency/rebase policy.
- Create new baseline atomically on approval.

**Exit gate:** add/modify/remove cases and concurrent-change scenarios meet approved examples and lifecycle rules.

## Phase 5 — History and release hardening

- Add baseline/change/decision history views.
- Complete authorization review, accessibility checks, browser checks, performance measurement, migration rehearsal, and backup/restore procedure for the selected deployment.
- Finalize operations, deployment, and incident documentation.

**Exit gate:** release checklist evidence exists; unresolved decisions affecting shipped behavior are zero.

## Phase 6 — Optional grounded explanations

This phase is skipped unless U-09 is approved.

- Start with deterministic template explanations if they meet the user need.
- If a model is justified, implement only the evidence adapter, output validation, labeling, logging policy, timeouts, and graceful fallback.
- Evaluate against a reviewed fixture set for unsupported numbers, missing/incorrect finding references, prompt injection in user fields, privacy leakage, and availability failure.

**Exit gate:** disabling AI changes no authoritative result or decision workflow; evaluated output meets an owner-approved threshold.

## Validation strategy

- **Domain unit tests:** pure calculations and lifecycle policies.
- **Property/boundary tests:** determinism, numeric ranges, rounding, and aggregation invariants.
- **Database integration tests:** constraints, migrations, transactions, concurrency, and rollback using PostgreSQL (not an incompatible substitute).
- **API contract tests:** OpenAPI shapes, error codes, authorization, idempotency.
- **Frontend tests:** critical state rendering and user interactions.
- **End-to-end tests:** create → calculate → submit → approve; propose → compare → decide; AI unavailable.
- **Manual checks:** accessibility, content clarity, consequential-action confirmation, and recovery instructions.

Tests must be reported as passing only when run in the stated environment. A checklist or planned test is not evidence.

## Work-item completion definition — Proposed

A work item is done when approved acceptance criteria are met, automated tests are added and run, formatting/lint/type checks pass, migrations and API changes are documented, guardrails are reviewed, and no new unresolved product decision is silently encoded.

