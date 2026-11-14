# ScopePilot — V1 Demonstration Scope

## Purpose and boundary
V1 is a **portfolio-quality functional demonstration**, not a production release. It should tell one coherent product story with fictional data and demonstrate product discovery, prioritization, workflow design, decision governance and measurable outcomes. The approved direction is recorded in [DECISION_REGISTER.md](DECISION_REGISTER.md).

## Must have
1. Workspace/project context and role-aware navigation.
2. Requirements with clarification status and structured discussions.
3. Tasks linked to requirements, one primary assignee, status and actual effort.
4. Finish-to-Start dependencies with cycle validation and blocked-state visibility.
5. PERT estimates in person-hours: E = (O + 4M + P) / 6.
6. Workspace working calendar (default 8 hours/day, Monday–Friday).
7. Schedule projection, milestone/target-date comparison and evidence-backed On Track / At Risk / Delayed status.
8. Workload/capacity visibility and manually controlled task assignment.
9. Change requests with affected requirements/tasks/dependencies and potential effort, schedule, capacity and commitment impact.
10. Technical and business approval steps; client confirmation when their agreed deliverables/cost/dates change.
11. Immutable approved baseline versions and traceable decision history.
12. Role-aware dashboards for Owner/Admin, Team Leader, Developer/Member and Client.
13. Seeded e-commerce agency scenario, demo reset and clearly labelled simulated information.
14. Illustrative KPI dashboard with definitions and simulated data.

## Should have (include if they fit the demo without undermining the Must-have story)
- Contextual project/task/requirement/change-request discussions.
- In-app notifications.
- Employee blocker, assistance and extension requests with escalation.
- Central risk register and mitigation tracking.
- Release lifecycle, rollback record, client acceptance and simplified closure.
- Optional AI explanation of findings, requirement clarification summaries and evidence-grounded options. AI must never be required for core functionality.

## Explicitly out of scope
- Production deployment or commercial launch.
- Paid services, paid APIs or paid infrastructure.
- Google OAuth/Google Sign-In; email/password is the selected direction if authentication is implemented. Never collect Gmail credentials.
- Enterprise SSO, billing/subscriptions, native mobile, custom model training, autonomous agents or AI state mutation.
- General-purpose chat, social networking, employee surveillance or performance ranking.
- Microservices, Kubernetes, Kafka, Redis, vector databases, complex distributed infrastructure.
- Advanced predictive risk probabilities, custom workflow/formula builders, complex workforce management.
- Real customer data, confidential documents or unapproved third-party integrations.

## Demonstration acceptance criteria
- A first-time viewer can understand the problem, intended users and product value.
- The flagship scenario can be followed end-to-end without hidden manual explanation.
- A requirement can be traced to tasks and delivery evidence.
- A change request shows what changes and why its impact is projected.
- Required human approvals and client confirmation are visible and auditable.
- An approved change creates a new baseline without rewriting history.
- Dashboards distinguish actual data from illustrative/simulated data.
- AI is visibly advisory and the experience remains understandable without it.
- The demo can be reset to a known starting state.

## Prioritization rule
If time is constrained, complete the end-to-end requirement → task → baseline → change request → impact → approval → revised baseline story first. Add release, closure, notifications and optional AI only after this core story is clear. Do not expand scope merely to increase feature count.
