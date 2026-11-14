# ScopePilot — Implementation Plan

## Delivery objective
Build a coherent, demonstrable product experience that communicates the approved ScopePilot value proposition. This is a portfolio prototype, not a production launch. Prioritize user journeys and PM evidence over breadth of engineering.

## Guiding principles
- Product and UX decisions lead implementation.
- Use the approved free/local-first stack and one modular monolith.
- Build the smallest end-to-end slice before secondary features.
- Deterministic calculations are authoritative; AI remains optional.
- Use fictional seeded data and a repeatable demo reset.
- Do not add infrastructure/features merely to increase apparent complexity.
- Report only work actually completed and verified.

## Stage 1 — Documentation baseline
**Status:** In progress.
- Consolidate approved product decisions.
- Align PRD, V1 scope, user journeys and technical documents.
- Record implementation-specific assumptions without reopening settled product decisions.
**Exit criteria:** documents tell one consistent product story; stale unresolved labels no longer contradict approved decisions.

## Stage 2 — UX structure and wireframes
**Next after documentation alignment.**
- Define information architecture and role-aware navigation.
- Map the flagship e-commerce agency scenario end-to-end.
- Prioritize screens: demo entry/workspace, dashboard, project overview, requirements/clarification, task board, change request, impact assessment, approval review, client view and baseline history.
- Add secondary screens only as needed: risk register, employee concern, notifications, release and closure.
- Create low-fidelity wireframes annotated with decisions, visibility rules, states and empty/error conditions.
- Review whether a first-time viewer understands the product without narration.
**Exit criteria:** core flows and screen responsibilities are clear; key trade-offs are documented.

## Stage 3 — Clickable prototype
- Build a navigable prototype with free tools.
- Use realistic fictional data and label simulated content.
- Demonstrate requirement → task plan → baseline → change request → impact → approvals → revised baseline.
- Show role differences and client/internal visibility.
- Use deterministic mock calculations if backend calculation logic is not implemented; label them as simulated.
**Exit criteria:** a reviewer can complete the flagship scenario and understand the differentiator.

## Stage 4 — Functional demo foundation
- Set up React/TypeScript frontend, FastAPI backend and PostgreSQL local environment.
- Pin free/open-source dependency versions and document local setup.
- Add only identity/workspace/project structure required by the demo.
- Seed fictional demo data and provide reset.
- Add automated checks for implemented paths.
**Exit criteria:** clean setup and repeatable local run are verified; no paid service required.

## Stage 5 — Core delivery workflow
- Implement requirements and clarification.
- Implement tasks, PERT estimates, Finish-to-Start dependencies and progress.
- Implement deterministic schedule/capacity findings with visible assumptions.
- Implement immutable baseline and version history.
- Implement change request, impact comparison, technical/business approval and client confirmation.
- Add audit history for consequential actions.
**Exit criteria:** core story works end-to-end with tests for calculations, permissions and baseline integrity.

## Stage 6 — Secondary demo capabilities
Prioritize based on remaining time/value: risk register; employee concerns/escalation; in-app notifications; release tracking/client acceptance/closure; contextual discussions; illustrative KPI dashboard. Do not implement every secondary capability if it weakens the core story.

## Stage 7 — Optional AI explanation
- First evaluate whether template-generated explanations meet the need.
- If useful and still no-cost/privacy-appropriate, add an optional provider adapter.
- Ground outputs in supplied findings; label suggestions; test unsupported claims and AI unavailability.
- No tools, write access, approval authority or autonomous actions.
This stage can be omitted without making the core product incomplete.

## Stage 8 — Portfolio packaging
Prepare a case study covering problem, target users, hypothesis, discovery evidence, strategy, prioritization, key decisions, wireframes, prototype, metrics and trade-offs. Record what is functional, simulated and out of scope. Capture a short walkthrough. Do not claim production readiness or customer impact.

## Validation approach
Review each journey against acceptance criteria. Test deterministic calculations with normal/boundary examples; authorization and client/internal visibility; baseline immutability and approval transitions; frontend states/navigation; clean local setup and demo reset. Maintain a verification log with command, environment, result and date.

## Current checkpoint
Stage 1 documentation alignment is underway. PRD, V1 scope, user journeys, decision register and README have been updated. Technical documents are being reconciled. No application implementation or test completion is implied.
