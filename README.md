# ScopePilot

ScopePilot is in **Phase 0: product and architecture definition**. No application has been implemented yet.

The working V1.0 product hypothesis is a single-team workspace for turning a structured project scope into a deterministic baseline, comparing proposed changes against that baseline, and presenting grounded impact findings for human approval. This hypothesis requires product-owner confirmation; the source repository was empty when these documents were created.

## Status vocabulary

- **Approved**: explicitly required by the project brief.
- **Proposed**: a reversible default chosen to make the design concrete; it is not an approved product decision.
- **Unresolved**: a material decision that must be answered before the affected implementation begins.

## Phase 0 documents

| Document | Purpose |
|---|---|
| [PRD.md](PRD.md) | Product intent, users, requirements, success measures, and risks |
| [V1_SCOPE.md](V1_SCOPE.md) | V1.0 inclusions, exclusions, and release boundary |
| [USER_JOURNEYS.md](USER_JOURNEYS.md) | Primary workflows and approval points |
| [SYSTEM_DESIGN.md](SYSTEM_DESIGN.md) | Modular-monolith architecture and module boundaries |
| [DATA_MODEL.md](DATA_MODEL.md) | Conceptual entities, relationships, and lifecycle |
| [DOMAIN_RULES.md](DOMAIN_RULES.md) | Calculation, state, approval, and AI grounding rules |
| [API_CONTRACT.md](API_CONTRACT.md) | Proposed HTTP API and error conventions |
| [IMPLEMENTATION_PLAN.md](IMPLEMENTATION_PLAN.md) | Sequenced delivery plan and gates |
| [DEVELOPMENT_SETUP.md](DEVELOPMENT_SETUP.md) | Proposed local development contract |

## Approved technical guardrails

- Modular monolith: React + TypeScript frontend, FastAPI backend, PostgreSQL database.
- Deterministic calculations are authoritative.
- AI may explain grounded findings but may not create authoritative calculations or decisions.
- Consequential changes require explicit human approval.
- No paid dependencies or services.
- Avoid infrastructure and abstractions that V1.0 does not need.

## Intended repository structure

The following is the target structure for implementation. Phase 0 deliberately creates documentation only.

```text
ScopePilot/
├── frontend/               # React + TypeScript application (future)
├── backend/                # FastAPI modular monolith (future)
│   ├── app/
│   │   ├── api/            # HTTP transport
│   │   ├── modules/        # Domain/application modules
│   │   ├── infrastructure/ # Database and external adapters
│   │   └── main.py
│   └── tests/
├── docs/                   # ADRs and later operational docs (future)
└── <Phase 0 documents>
```

Empty implementation directories are not committed. They should be introduced by the first approved implementation change together with their build configuration and tests.

## Before implementation

Resolve the release-blocking decisions collected in [V1_SCOPE.md](V1_SCOPE.md#unresolved-release-decisions), especially the product definition, tenancy/authentication model, estimate unit and formula, change-impact rules, and AI availability. Do not interpret a proposed default as product approval.

