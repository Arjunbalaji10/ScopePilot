# ScopePilot — Development Setup

## Current state
The repository currently contains product and technical documentation. The application, dependency manifests, database migrations, container configuration and test suites have not yet been created. The instructions below define the intended setup direction; they are not commands that can be run today.

## Intended stack
- React, TypeScript, Vite, Tailwind CSS and shadcn/ui.
- Python and FastAPI with Pydantic and SQLAlchemy.
- PostgreSQL and Alembic.
- Docker Compose for local services where useful.
- pytest, Vitest, React Testing Library and Playwright where proportionate.

All dependencies must be free/open-source. Pin compatible runtime and package-manager versions when Stage 4 begins. Review licenses before adoption.

## Prerequisites (to be pinned later)
- Git.
- Supported Node.js LTS version and one locked package manager.
- Supported Python version and one locked dependency/environment tool.
- PostgreSQL, locally installed or through Docker Compose.
- Docker Engine with Compose, optional if PostgreSQL is installed directly.

## Configuration approach
Create a committed .env.example with variable names and safe local examples only. Keep actual secrets in ignored local environment files. Expected settings may include:
- APP_ENV
- DATABASE_URL
- FRONTEND_ORIGIN
- SESSION_SECRET
- AI_EXPLANATIONS_ENABLED=false

Exact names and formats must match the implementation. Do not add external AI credentials unless an optional provider is explicitly selected. Never store Gmail passwords or commit secrets.

## Intended local workflow
Once the app exists, provide documented commands to:
1. install locked frontend and backend dependencies;
2. start local PostgreSQL;
3. apply reviewed Alembic migrations;
4. start FastAPI and the frontend development server;
5. run formatting, lint, type checks and tests;
6. load/reset fictional demo data;
7. stop services without deleting data by default.

Prefer a small set of project scripts or cross-platform task runner commands. Windows/PowerShell should be supported.

## Database and demo-data rules
- Use PostgreSQL for integration tests that depend on PostgreSQL behavior.
- Use a separate test database and prevent tests from targeting production-like URLs.
- Migrations own schema changes; application startup must not mutate schema opportunistically.
- Seed fixtures are deterministic and entirely fictional.
- Destructive reset is an explicit command that identifies and validates its target.
- Preserve audit history and approved baseline snapshots within normal workflows.

## Quality checks to establish
Backend: formatter, linter, static type checking, unit tests, PostgreSQL integration tests and migration consistency.

Frontend: formatter/linter, strict TypeScript check, component tests, production build and critical end-to-end/accessibility checks.

Repository: generated OpenAPI/client consistency, secret scanning and dependency/license review using free tooling.

Select exact tool names and versions in short architecture decision records rather than prematurely fixing them here.

## Current limitations
There is no valid npm, Python, Docker, migration, build, lint, type-check or test command in the repository yet. Do not infer application health or feature completion from documentation updates. The next product milestone after documentation alignment is UX structure and wireframes; implementation follows the clickable prototype plan.
