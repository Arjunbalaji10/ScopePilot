# ScopePilot V1.0 Scope

## Scope authority

Only the technology choices and guardrails in the project brief are approved. The feature boundary below implements the product hypothesis in [PRD.md](PRD.md) and is **Proposed** pending owner confirmation.

## Proposed V1.0 inclusions

- Project creation, viewing, updating, and archival (archive semantics unresolved).
- Structured scope items with title, description, category, estimate input, and ordering.
- Draft validation and deterministic project totals.
- Submission, approval, and rejection of an initial baseline.
- Immutable, versioned approved baseline snapshots.
- Change requests that add, modify, or remove scope items against the current baseline.
- Field-level before/after comparison.
- Deterministic recalculation of total and delta findings.
- Human approval or rejection with an audit record.
- New baseline creation after an approved change.
- Optional on-demand AI explanation of an already-computed finding.
- History views for baselines, change requests, decisions, and calculation metadata.
- Responsive web UI for desktop and tablet; mobile expectations unresolved.

## Approved exclusions and inferred exclusions

The brief references “agreed V1.0 exclusions” but does not enumerate them, and the repository has no source document. Therefore no detailed exclusion can honestly be labeled agreed. The following are **Proposed exclusions** consistent with the guardrails:

- Automated approval or application of consequential changes.
- AI-generated authoritative estimates, risk scores, scope changes, or decisions.
- Autonomous agents or background AI workflows.
- Paid AI, authentication, analytics, hosting, storage, or observability dependencies.
- Multiple backend services, event brokers, service mesh, Kubernetes, distributed cache, search cluster, or vector database.
- Native mobile applications.
- Real-time collaborative editing, comments/chat, notifications, email, or calendar integrations.
- Billing, subscriptions, marketplace, or public API ecosystem.
- Import/export and third-party project-management integrations unless specifically approved.
- Custom formula builder, workflow builder, or tenant-specific rule engine.
- Offline mode and multi-region/high-availability deployment.
- File attachments and document ingestion.

These exclusions must be reconciled against the actual agreed list when supplied.

## Definition of a V1.0 release candidate — Proposed

- All approved in-scope journeys have acceptance tests.
- Calculation examples are approved and pass at boundary and rounding cases.
- Approval transitions are transactional and audit records are immutable to ordinary users.
- The system is fully usable with AI disabled.
- AI output, if enabled, is grounded, labeled, and cannot trigger writes.
- Security, accessibility, migration, backup/restore, and local setup checks are documented and performed.
- No release-blocking decision below remains unresolved.

## Unresolved release decisions

| ID | Decision | Why it blocks implementation |
|---|---|---|
| U-01 | Confirm or replace the product hypothesis. | Determines every feature and entity. |
| U-02 | Supply the agreed V1.0 inclusion and exclusion list. | Prevents silent scope expansion or omission. |
| U-03 | Define target user, organization/tenant boundaries, roles, and authentication. | Determines data ownership and authorization. |
| U-04 | Define scope-item fields and allowed hierarchy/dependencies. | Determines schema and editing experience. |
| U-05 | Define estimate unit, input model, formula, aggregation, rounding, and rule versioning. | Deterministic calculation cannot be implemented safely without it. |
| U-06 | Define which changes are “consequential.” | Determines mandatory approval boundaries. |
| U-07 | Define who may approve, whether self-approval is allowed, and rationale requirements. | Determines workflow enforcement. |
| U-08 | Define concurrent edit/change behavior and stale-request handling. | Prevents approval against an obsolete baseline. |
| U-09 | Decide whether AI ships in V1.0; if so, approve a free/local provider, model, privacy policy, and failure behavior. | No paid services are allowed and project data may be sensitive. |
| U-10 | Define retention, deletion, archive, and audit-data policies. | Affects integrity, privacy, and API behavior. |
| U-11 | Define expected scale, deployment target, browser support, accessibility target, and performance SLOs. | Needed for measurable acceptance. |
| U-12 | Decide whether exports/imports or integrations are genuinely excluded. | The referenced agreed exclusions were unavailable. |

## Scope change control

Any addition to V1.0 must state the user outcome, affected requirements, data/API changes, migration impact, new dependencies, validation plan, and whether an exclusion changes. Product ownership approves scope; architecture review confirms guardrail compliance.

