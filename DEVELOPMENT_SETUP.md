# Development Setup

## Current state

The repository contains Phase 0 documentation only. There is no application, dependency manifest, container definition, migration, or test suite to run. The commands below are a **Proposed setup contract**, not currently executable instructions.

## Proposed prerequisites

- Git
- A supported Node.js LTS release and a single locked package manager (versions unresolved)
- A supported Python release and a single locked environment/dependency tool (versions unresolved)
- PostgreSQL (version unresolved)
- Optional Docker Engine with Compose for local PostgreSQL

Exact versions must be pinned when Phase 1 begins. All selected dependencies must be free/open-source; their licenses should be reviewed.

## Proposed configuration

Commit a `.env.example` containing names and safe examples only. Local secrets belong in ignored files. Candidate variables:

```dotenv
APP_ENV=development
DATABASE_URL=postgresql+<driver>://scopepilot:local-only@localhost:5432/scopepilot
FRONTEND_ORIGIN=http://localhost:<port>
AI_EXPLANATIONS_ENABLED=false
```

Driver and ports are intentionally unspecified. AI provider variables must not be introduced until U-09 is approved. The backend should fail fast on missing required configuration and never silently use production-like defaults.

## Proposed developer workflow

Once Phase 1 tooling exists, the documented workflow should provide stable commands for:

1. install locked frontend and backend dependencies;
2. start PostgreSQL;
3. apply migrations;
4. start FastAPI and the frontend development server;
5. run formatting checks, lint, static type checks, unit/integration tests, and end-to-end tests;
6. stop local services without deleting database data by default.

Prefer project scripts or a small cross-platform task runner over a long collection of raw commands. Windows/PowerShell is a supported development environment unless the team decides otherwise.

## Proposed local database rules

- Use PostgreSQL for integration tests that rely on PostgreSQL semantics.
- Use a separate test database/schema and prevent tests from accepting a production connection string.
- Migrations create schema; application startup does not mutate schema opportunistically.
- Seed fixtures are deterministic and contain no real user/project data.
- Destructive reset is an explicit command that prints/validates its target and is never part of ordinary startup.

## Quality gates to establish in Phase 1

### Backend

- formatter and linter;
- static type checker;
- unit and PostgreSQL integration tests with coverage reported but no arbitrary coverage claim;
- migration consistency check;
- dependency vulnerability/license review using free tooling.

### Frontend

- formatter/linter;
- TypeScript strict type check;
- component/unit tests;
- production build;
- critical end-to-end and accessibility checks.

### Repository

- generated OpenAPI drift check and generated client/type check;
- secret scanning and dependency update policy using free tooling;
- no required paid CI actions or services.

Tool names should be selected in ADRs instead of being prematurely fixed here.

## Troubleshooting contract — Proposed

Future setup documentation must cover port conflicts, database readiness, migration mismatch, clean dependency reinstall, test-database safety, and AI-disabled behavior. Any command that deletes volumes or data must explicitly warn the user and identify the exact target.

## Not yet available

There is currently no valid `npm`, Python, Docker, migration, build, lint, type-check, or test command in this repository. Do not infer project health from the documentation checks performed during Phase 0.

