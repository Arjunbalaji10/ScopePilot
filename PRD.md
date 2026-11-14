# ScopePilot — Product Requirements Document

## Document status
**Product direction:** Approved  
**Delivery intent:** Portfolio demonstration / functional prototype  
**Implementation status:** Not implied by this document  
The approved decisions are consolidated in [DECISION_REGISTER.md](DECISION_REGISTER.md). This PRD translates them into the product narrative and V1 requirements.

## 1. Product overview
ScopePilot is an AI-assisted Project Delivery Intelligence platform for small software and digital agencies. It helps teams coordinate client expectations, requirements, delivery work and scope changes. Its central value is making the likely consequences of a proposed change visible before people commit to it.

ScopePilot is a portfolio demonstration of product thinking and product execution. It is not intended to be a production-ready commercial service. Use fictional data, free/local-first tooling and a deliberately limited feature set.

## 2. Problem
Small delivery teams coordinate clients, developers and managers through fragmented documents and conversations. Requirements can be unclear, work can become blocked, and proposed changes can affect dependencies, workload and delivery dates. Without a shared view of commitments and evidence, teams may agree to changes without understanding the trade-offs.

## 3. Product hypothesis
If small agencies can maintain clear requirements, tasks, dependencies and approved baselines—and assess the likely effort, schedule, capacity and risk implications of proposed changes—then teams and clients can make more informed decisions and reduce avoidable misunderstandings.

## 4. Users and roles
- **Owner/Admin:** oversees workspace, project commitments, business approvals and delivery risks.
- **Team Leader:** reviews requirements, technical feasibility, estimates, dependencies, workload, blockers and change impact.
- **Developer/Member:** works on assigned tasks, updates progress/actual effort, raises clarification requests and reports blockers or workload concerns.
- **Client:** views agreed project information, submits requirements/change requests, discusses them and confirms changes to their agreement.
- **Viewer:** reads authorized workspace/project information.

Workspace roles are Owner, Admin, Member and Viewer. Client access is a separate project-level permission. Team Leader is a project responsibility, not automatically synonymous with Admin. See the decision register for approval boundaries.

## 5. Product goals
1. Give the team and client a shared view of approved requirements and delivery progress.
2. Make project work traceable from requirements to tasks, dependencies, releases and closure.
3. Show evidence-based delivery risks and capacity conflicts.
4. Assess proposed scope changes before approval.
5. Preserve immutable baselines and an auditable decision history.
6. Demonstrate how AI can explain grounded findings without taking authority away from people.

## 6. Core experience
1. Create a workspace and project, or open the seeded demo.
2. Capture client requirements and resolve ambiguity.
3. Translate approved requirements into tasks, estimates and dependencies.
4. Establish an approved baseline.
5. Track work, actual effort, milestones, blockers, workload and delivery risks.
6. Submit a change request and inspect its impact on effort, schedule, dependencies, capacity and commitments.
7. Obtain required technical/business approvals and client confirmation when their agreement changes.
8. Create a new baseline only after approval.
9. Track releases, acceptance, post-deployment issues and project closure.

## 7. Functional requirements

| ID | Requirement | Priority |
|---|---|---|
| FR-01 | Workspace, project and role-aware access for the demo. | Must |
| FR-02 | Capture requirements with status, owner/source and clarification discussion. | Must |
| FR-03 | Link requirements to tasks; support task status, primary assignee and actual effort. | Must |
| FR-04 | Support Finish-to-Start dependencies and detect invalid/circular dependencies. | Must |
| FR-05 | Estimate task effort using PERT (O, M, P) and person-hours. | Must |
| FR-06 | Calculate schedule projections using dependencies and workspace calendar. | Must |
| FR-07 | Track milestones, target dates, workload and evidence-backed delivery risks. | Must |
| FR-08 | Create change requests and show affected requirements, tasks and dependencies. | Must |
| FR-09 | Show potential effort, schedule, capacity and commitment impact before approval. | Must |
| FR-10 | Enforce the appropriate technical, business and client-confirmation workflow. | Must |
| FR-11 | Preserve immutable baseline versions and decision/audit history. | Must |
| FR-12 | Provide role-aware dashboards and project views, including client view. | Must |
| FR-13 | Support contextual discussions and in-app notifications. | Should |
| FR-14 | Support employee assistance/blocker reports and escalation. | Should |
| FR-15 | Provide release tracking, acceptance and simplified closure. | Should |
| FR-16 | Provide a centralized risk register linked to project work. | Should |
| FR-17 | Offer optional AI explanations/summaries/recommendations grounded in project evidence. | Should |
| FR-18 | Show illustrative product KPIs using clearly labelled simulated data. | Must |

## 8. Non-functional and product guardrails
- Deterministic backend calculations are authoritative; AI is optional and advisory.
- Every important finding should show the evidence or entities that support it.
- Distinguish confirmed facts, calculated projections and AI suggestions.
- No AI approval, baseline mutation, automatic reassignment or autonomous deadline change.
- Core workflows function when AI is unavailable.
- Preserve approved baseline history and audit consequential actions.
- Enforce workspace, project, client and internal-discussion visibility boundaries.
- Keep the architecture a free/local-first modular monolith; no unnecessary distributed infrastructure.
- Use fictional/demo data and clearly label it.
- Prioritize understandable workflows and a credible product story over production hardening.

## 9. Success measures
Use illustrative demo KPIs, not claimed customer outcomes:
- Scope-change assessment time.
- Requirement clarification rate.
- Change approval cycle time.
- Delivery impact visibility.
- Baseline change traceability.
- Client–team alignment.

Define each KPI's numerator, denominator, time window and data source during UX/data design. Do not invent measured results.

## 10. Flagship demo
A fictional digital agency builds an e-commerce website. The demo moves from requirement clarification and baseline approval through task planning, a mid-development change request, impact assessment, approvals, revised baseline, release/deployment, client acceptance and a post-deployment defect or enhancement. Dashboard KPIs use simulated activity from this scenario.

## 11. Out of scope
Commercial billing/subscriptions, native mobile, enterprise SSO, autonomous agents, custom model training, microservices/Kubernetes, advanced predictive forecasting, general-purpose chat, social features, complex workforce management, paid integrations/services and production-scale operations.

## 12. Risks
- **Scope expansion:** maintain Must/Should boundaries and one flagship scenario.
- **Misleading impact estimates:** label projections, expose assumptions and show evidence.
- **AI hallucinations:** constrain AI to supplied evidence; retain deterministic fallback.
- **Confusing approval authority:** show separate technical, business and client confirmation steps.
- **Overengineering:** prefer the simplest free/local approach that supports the demo.
