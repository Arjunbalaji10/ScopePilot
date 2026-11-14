# System Design

## 1. Architecture status

The modular-monolith style and primary technologies are **Approved**. Module boundaries, deployment details, and supporting libraries are **Proposed**.

## 2. Context and containers

```text
Browser
  └── React + TypeScript single-page application
        └── JSON/HTTP API
              └── FastAPI modular monolith
                    ├── PostgreSQL
                    └── Optional AI adapter (disabled by default; provider unresolved)
```

The browser never connects directly to PostgreSQL or an AI provider. The backend is the authority for validation, calculations, state transitions, authorization, and evidence construction.

## 3. Backend modules — Proposed

| Module | Responsibility | Must not own |
|---|---|---|
| Identity & Access | Trusted actor context, roles, authorization | Product calculations |
| Projects | Project lifecycle and membership boundary | Approval decisions |
| Scope | Draft scope items and validation | AI prompts |
| Baselines | Immutable approved snapshots and current-version pointer | Draft editing |
| Changes | Proposed diffs, revisions, submission lifecycle | Calculation formulas |
| Calculations | Pure deterministic rules, aggregation, findings, rule-set version | Database writes or AI |
| Approvals | Transition policy, optimistic concurrency, decisions | Rendering explanations |
| Explanations | Evidence payload and optional provider adapter | Authority or state transitions |
| Audit | Append-only business event record | Mutable operational logging |

Modules live in one codebase and one runtime. Each exposes application-level interfaces; API handlers do not reach into another module's database implementation. This is boundary discipline, not a mandate for elaborate dependency-injection frameworks.

## 4. Layers — Proposed

```text
API routes / schemas
        ↓
Application use cases and transaction boundaries
        ↓
Domain entities, policies, pure calculations
        ↓
PostgreSQL repositories and optional external adapters
```

- Pydantic request/response models are transport types, not database entities.
- Domain calculation functions accept explicit inputs and return results without I/O, current-time reads, random values, or model calls.
- Database constraints enforce invariants that must survive application defects.
- Cross-module state transitions run in a single PostgreSQL transaction.

## 5. Frontend structure — Proposed

Organize by feature (`projects`, `scope`, `baselines`, `changes`, `approvals`, `history`) with shared UI and API-client infrastructure. Server state is not duplicated into a global client store without a demonstrated need. The UI may preview calculations for responsiveness only if clearly labeled; backend results remain authoritative.

## 6. Authoritative calculation flow

1. API validates shape and type.
2. Application use case loads the exact version and checks access/state.
3. Domain validation normalizes approved inputs.
4. A pure calculation engine applies a named `rule_set_version`.
5. The backend stores or returns structured findings with input fingerprint and version.
6. The frontend renders those findings without recomputing authority.

An approved formula specification and golden examples are prerequisites. Hash algorithm and canonical serialization are unresolved.

## 7. Approval transaction

An approval request supplies the submitted revision/version. In one transaction the backend locks or conditionally updates the request, verifies its baseline is current, records the decision, creates the immutable baseline snapshot, advances the current-baseline pointer, and appends an audit event. Any failure rolls back all effects. Repeated requests use an idempotency strategy still to be selected.

## 8. AI boundary

AI is an optional adapter behind the `Explanations` module. Its input is a versioned evidence envelope containing only approved fields, structured diff, deterministic findings, and display-safe metadata. Its output is untrusted text.

Required controls before enabling it:

- approved free/local provider and model;
- data-handling and retention review;
- prompt/model version recording;
- schema or citation validation against supplied finding IDs;
- timeouts and size limits;
- no tools, write endpoints, database credentials, or decision capability;
- visible disclaimer and graceful fallback.

Template-based explanations are a valid zero-cost fallback and may be preferable for V1.0.

## 9. Deployment — Proposed minimum

One static frontend artifact, one FastAPI process image/application, and one PostgreSQL instance. Local development may use Docker Compose. Production hosting is unresolved. Do not add Redis, a message broker, worker service, object store, vector store, or orchestration platform until a measured requirement justifies it.

## 10. Security and operations baseline — Proposed

- Same-site secure session cookie is preferred over browser-stored bearer tokens if first-party authentication is selected.
- Authorization is checked on every project-scoped command/query.
- Use parameterized database access and schema migrations.
- CSRF protection is required for cookie-authenticated writes; configure restrictive CORS.
- Secrets come from environment/runtime secret injection and are never committed.
- Structured logs use correlation IDs and exclude scope descriptions and AI evidence by default.
- Health endpoints distinguish liveness from database readiness.
- Backup/restore ownership and production observability are unresolved.

## 11. Architecture decisions required before code

See U-01 through U-11 in [V1_SCOPE.md](V1_SCOPE.md). Also select the Python/Node versions, package managers, ORM/migration library, frontend build/test stack, authentication approach, and API versioning policy. Library choices must be free/open-source and recorded in short ADRs when selected.

