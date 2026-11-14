# ScopePilot — System Design

## 1. Design intent
ScopePilot is a portfolio demonstration and functional prototype. Use a simple free/local-first modular monolith. Architecture supports the user journeys and explainable delivery-impact workflow; it is not an exercise in infrastructure complexity.

## 2. Approved technology direction
- Frontend: React, TypeScript, Vite, Tailwind CSS, shadcn/ui, React Router and TanStack Query; Recharts only where useful.
- Backend: Python, FastAPI, Pydantic and SQLAlchemy.
- Database: PostgreSQL with Alembic migrations.
- Local development: Docker Compose where useful.
- Testing: pytest, Vitest, React Testing Library and Playwright where proportionate.
- Optional AI: provider-independent adapter; local Ollama or a free provider only if no-cost and privacy-appropriate.
- Source control/automation: Git, GitHub and free GitHub Actions usage where available.
Pin compatible versions when implementation begins. Do not add paid dependencies or services.

## 3. System context
Browser → React + TypeScript application → FastAPI JSON API (single modular monolith) → PostgreSQL. An optional AI explanation adapter is disabled by default.

The browser never connects directly to PostgreSQL or an AI provider. Backend owns authorization, validation, deterministic calculations, workflow transitions and audit records.

## 4. Logical backend modules
| Module | Responsibility |
|---|---|
| Identity & Access | Email/password identity if implemented, workspace membership, project/client access |
| Workspaces & Projects | Workspace isolation, project metadata and lifecycle |
| Requirements | Requirement capture, clarification and approval state |
| Delivery Planning | Tasks, assignments, PERT estimates, dependencies, calendar and schedule |
| Capacity & Concerns | Workload visibility, employee reports and escalation |
| Change Management | Change lifecycle, revisions, classification and impact assessment |
| Approvals & Baselines | Technical/business/client decisions and immutable versions |
| Risks & Releases | Risk register, release tracking, acceptance and closure |
| Communication | Contextual discussion and in-app notifications |
| Intelligence | Deterministic rules, findings and optional AI explanations |
| Audit | Append-only consequential action history |

These are boundaries inside one codebase/runtime, not separate services. Avoid elaborate abstractions without a real need.

## 5. Layering
FastAPI routes/Pydantic schemas → application use cases and transaction boundaries → domain rules and pure calculation functions → SQLAlchemy repositories/PostgreSQL. Optional AI sits behind an adapter.

Transport schemas are not database entities. Calculation functions accept explicit inputs and return structured outputs without I/O/model calls. Authorization is checked server-side. Database constraints protect critical invariants. Approval/baseline transitions run in a transaction.

## 6. Deterministic delivery calculation
1. Validate estimates, task status, dependencies, assignments and calendar inputs.
2. Calculate PERT task estimate: (O + 4M + P) / 6.
3. Calculate planned effort from task estimates.
4. Build a valid Finish-to-Start dependency order and reject cycles.
5. Calculate schedule projection against workspace working days/hours and remaining effort.
6. Compare projected completion with target date.
7. Evaluate workload against available capacity.
8. Return structured findings with affected requirement/task references, assumptions and calculation version.

The formula and dependency rules are approved at product level. Exact rounding, partial-day allocation, resource capacity allocation and thresholds need a short calculation specification and golden examples before implementation. A schedule projection is not a guarantee.

## 7. Scope-change impact flow
Pin request to a baseline; freeze the submitted revision; identify affected requirements, tasks and downstream dependencies; calculate potential effort, schedule, capacity and risk effects; show assumptions, missing inputs and affected commitments; collect Team Leader technical review, Owner/Admin business approval and client confirmation when their agreement changes. Create a new immutable baseline only after required approvals. If the baseline changes after assessment, mark the assessment stale and require recalculation/review.

## 8. AI boundary
AI is optional, advisory and disabled by default. It may summarize/explain supplied findings and suggest options. It must not calculate authoritative values, access unrestricted database content, use write tools or change project state. Provide template-based fallback. If a model is enabled, minimize data, record provider/model/template version, validate references and label output.

## 9. Frontend organization
Organize by workspace, dashboard, projects, requirements, tasks, change requests, impact review, approvals, client view, risks, releases and history. Reuse navigation, forms, status indicators and API client. Role-aware navigation is not authorization; backend enforces permissions. Use charts only when they clarify delivery/product outcomes.

## 10. Security and privacy baseline
- Never store plaintext passwords or Gmail account passwords.
- Hash application passwords with Argon2id if email/password auth is implemented.
- Prefer secure server-managed sessions/cookies; protect cookie-authenticated writes against CSRF.
- Scope every query/mutation to authorized workspace/project access.
- Separate client-visible data from internal notes, estimates and assignments.
- Validate inputs and use parameterized database access.
- Keep secrets out of source control and browser bundles.
- Minimize logs and AI payloads; do not send confidential project information to external models without an approved basis.
- Use fictional demo data.

## 11. Local setup and deployment boundary
Local-first development is the default. Docker Compose may run PostgreSQL and the app locally. Production deployment is not required for the portfolio objective. Do not introduce Redis, Kafka, microservices, Kubernetes, vector databases, worker fleets, enterprise observability or paid hosting without a demonstrated requirement.

## 12. Architecture decision records
Before implementation, record short decisions for compatible runtime versions, package managers, auth/session approach, database driver, AI mode (or no AI), test tooling and local run commands. Prefer reversible decisions and explain the user need each supports.
