# Data Model

## Status

This is a **conceptual, Proposed** model for the unconfirmed product hypothesis. Names and columns are not an instruction to create migrations until the domain decisions are approved.

## Relationship overview

```text
User ──< ProjectMembership >── Project
                               ├──< ScopeDraft ──< ScopeItemDraft
                               ├──< Baseline ──< BaselineItem
                               ├──< ChangeRequest ──< ChangeRevision ──< ChangeOperation
                               │                         └── CalculationRun ──< Finding
                               └──< AuditEvent

ApprovalDecision → one submitted baseline candidate or change revision
Explanation      → one CalculationRun and its evidence snapshot
```

Whether `User` and `ProjectMembership` exist in V1.0 depends on the authentication/tenancy decision.

## Core entities

### Project

- `id` UUID
- `name`, `description` (constraints unresolved)
- `status`: proposed `active | archived`
- `current_baseline_id` nullable FK
- timestamps and optimistic `version`

### ScopeDraft / ScopeItemDraft

Mutable working state for an initial baseline. Proposed item fields are `id`, `client_key`, `title`, `description`, `category`, `estimate_value`, `position`, timestamps, and version. Estimate type/unit, categories, hierarchy, dependencies, tags, acceptance criteria, and stable identity rules are unresolved.

### Baseline / BaselineItem

Immutable snapshot created only by an approval transition. `Baseline` includes project, monotonically increasing project-local `version`, source decision, rule-set version, calculated summary, input fingerprint, approver, approval time, and optional rationale. `BaselineItem` stores the complete item snapshot; it must not reference mutable draft values as its source of truth.

### ChangeRequest / ChangeRevision / ChangeOperation

- `ChangeRequest`: project, pinned base baseline, lifecycle state, author, title/rationale.
- `ChangeRevision`: immutable proposal revision number, creation metadata, submission metadata.
- `ChangeOperation`: proposed `add | modify | remove`, stable target item identity, and before/after snapshots or patch representation.

Store an immutable submitted revision. Whether editable drafts use full desired-state snapshots or operations is an implementation decision; full snapshots simplify recalculation, while operations make intent explicit. Select one after item identity and concurrency rules are approved.

### CalculationRun / Finding

`CalculationRun` records subject type/id/version, calculation kind, `rule_set_version`, canonical input fingerprint, structured input snapshot or durable reference, structured output summary, status, and timestamps. A `Finding` has a stable code, severity, message parameters, numeric values/units, and affected entity references. Presentation text is not the authoritative value.

### ApprovalDecision

Append-only record of target type/id/revision, `approved | rejected`, trusted actor, timestamp, rationale, and expected prior state/version. The effective baseline link is present only for an approved baseline-changing decision.

### Explanation

Optional derived artifact: calculation run, evidence version/fingerprint, provider/model or `template`, prompt/template version, output text, cited finding IDs, requester, creation time, and status. Explanations are never inputs to calculations or decisions.

### AuditEvent

Append-only business audit record: event ID, project, event type, trusted actor, timestamp, target reference, correlation ID, and minimal structured metadata. It complements operational logs and must avoid secret or unnecessary sensitive content.

## Integrity constraints — Proposed

- Baseline version is unique within a project; one current baseline at most.
- Approved baseline and item snapshots are immutable through ordinary application paths.
- Submitted revision number is unique within a change request.
- A change request references a baseline from the same project.
- One terminal decision per submitted target revision.
- An approved transition cannot target a superseded baseline unless a future explicit rebase rule allows it.
- Numeric authoritative fields use PostgreSQL `numeric`, with precision/scale approved alongside formula rules.
- Timestamps use UTC `timestamptz`; user-facing localization is presentation only.
- Foreign-key and check constraints enforce lifecycle consistency where practical.

## Deletion and retention

Unresolved. Hard deletion conflicts with auditability. A proposed default is to archive projects and restrict physical deletion to an administrative privacy process with an explicit audit/retention policy. Do not implement cascading deletion until policy is approved.

## Migration policy — Proposed

Use ordered, reviewed database migrations. Migrations are forward-safe, make data transformations explicit, and have a tested rollback or recovery plan appropriate to their risk. Seed data is for local/test environments only and must not encode product decisions disguised as fixtures.

