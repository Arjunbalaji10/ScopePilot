# ScopePilot — Approved Product Decision Register

**Status:** Approved product direction for the portfolio demonstration  
**Purpose:** This register consolidates decisions explicitly approved by the product owner in the ScopePilot planning conversation. It supersedes earlier "unresolved" labels where the same topic is addressed below. It does not mean the features have been implemented.

## Project purpose and constraints

ScopePilot is a **Product Management portfolio demonstration**, not a production software product and not a developer-skills showcase. It should demonstrate product discovery, user understanding, strategy, prioritization, requirements, user journeys, workflows, wireframes, KPI thinking, trade-offs and technical feasibility.

Build a convincing, usable demo with simulated data. Do not pursue enterprise-grade infrastructure, production operations, unnecessary engineering complexity or real-customer deployment. Prefer free/local-first tools. Label simulated data and AI-generated recommendations clearly. Features must justify their value to the product story.

## Approved decisions

### 1. Product hypothesis and target customers
ScopePilot helps small software and digital agencies manage project delivery and understand how proposed requirement changes may affect timelines, workload, dependencies, delivery risks and existing commitments. It provides structured project management, evidence-based delivery intelligence and scope-change impact analysis so people can make informed decisions before approving consequential changes.

Primary customers: small software development agencies and small digital agencies. Secondary: freelancers managing client projects. Future segments: early-stage startups and small project teams. Differentiator: Project Delivery Intelligence, especially scope-change impact analysis. It must not become a generic task manager with an AI chatbot.

### 2. V1 product scope
V1 demo covers project foundation, requirements and tasks, dependencies, milestones, delivery tracking, deterministic schedule/effort and risk findings, scope-change requests, impact analysis, options, human approvals, baseline history, audit history, role-aware views and grounded AI assistance. Detailed demo boundary is in `V1_SCOPE.md`.

### 3A. Tenancy
Organization/workspace-based tenancy. A user may belong to multiple workspaces. Workspace data is isolated.

### 3B. Workspace roles
Predefined workspace roles: Owner, Admin, Member and Viewer. A user may have different roles in different workspaces. Avoid custom permission builders in the demo. Team Leader is a project responsibility/role in the operating model and may be assigned separately from workspace Admin; do not assume they are always the same person.

### Authentication
Email/password authentication using email addresses (including Gmail addresses). This does **not** mean Google Sign-In or Google OAuth. Never collect or store a user's Gmail password. Use secure password hashing and server-managed sessions if implementing authentication. No paid auth provider.

### 3C. Scope-change approval authority
Owner/Admin and Team Leader have distinct approval responsibilities for consequential baseline changes. Team Leader reviews technical feasibility, effort, workload and delivery impact. Owner/Admin reviews business commitments, priority and authorization. The requester cannot approve their own consequential change. Record actor, time and rationale. Client confirmation is required when the client's agreed deliverables, cost or delivery commitments change.

### 4. Requirements and tasks
Keep Requirements and Tasks as separate concepts. Requirements describe what the client expects; tasks describe the work needed to deliver it. One requirement can link to multiple tasks. Tasks may have dependencies. Avoid complex nested hierarchies in the demo.

### 5. Effort unit
Use person-hours as the standard effort unit. Project effort is derived from task estimates. Effort is distinct from calendar duration. Actual effort is tracked separately from estimates. Approved baseline estimates are preserved.

### 5A. Estimation method
Use three-point PERT estimates per task: optimistic (O), most likely (M), pessimistic (P). Planning estimate = (O + 4M + P) / 6. Sum task planning estimates for project effort. Track actual effort separately. Preserve estimate revisions and reasons. PERT is a planning estimate, not a guarantee or a statistical confidence interval.

### 6. Dependencies
V1 uses Finish-to-Start dependencies only. Multiple prerequisites are allowed. Reject self-dependencies and circular chains. A task starts only after its prerequisites finish. Show blocked tasks and unfinished prerequisites. Recalculation must not silently alter approved commitments.

### 7. Workspace calendar
Configurable workspace calendar. Defaults: 8 working hours per day, Monday–Friday, weekends non-working. Workspace owner can configure working days and daily hours. Keep person-hour effort separate from calendar duration. Calculate earliest feasible schedule using Finish-to-Start dependencies. Do not assume unlimited parallel capacity for the same person.

### 8. Task progress and recalculation
Statuses: Not Started, In Progress, Blocked and Completed. Track actual effort separately. Actual effort can be updated while work is underway. Completed tasks retain actual start/finish dates and are not silently changed by recalculation. In-progress tasks use remaining effort for forward schedule calculations. Blocked tasks show the reason or blocking dependency.

### 9. Task assignment and capacity
Each task has one primary assignee or may remain unassigned. Assignees must be workspace members. Track individual availability and working hours. Identify workload and over-allocation, and include capacity conflicts in delivery-risk analysis. Do not automatically reassign tasks or change assignments.

### 10. Deadlines and delivery risks
Projects may have target delivery dates. Calculate projected completion using estimates, dependencies and the workspace calendar. Compare projection with target date and show On Track, At Risk or Delayed. Explain each risk with evidence such as dependency delays, capacity conflicts or increased effort. Do not fabricate risk percentages or guarantee future outcomes.

### 11. Scope-change impact intelligence
Every proposed change receives an impact assessment. Impacts are possibilities/scenarios, not guaranteed outcomes. Show potential additional/reduced effort, affected requirements/tasks/dependencies, potential delivery-date changes, workload/capacity consequences and existing commitments affected. Mandatory changes receive highest priority but still require approval. Client and team communication is contextual to project work. Consequential approvals and baseline history remain auditable.

### 12. Client access
Provide a dedicated client-facing project view. Clients can view progress, milestones, approved requirements and agreed dates; submit change requests; discuss and provide feedback on requests; and view decisions. They cannot edit internal estimates/assignments, view private employee discussions or approve on behalf of the agency.

### 13. Client identity and project access
Clients are invited by email and receive project-level access only to projects they are invited to. Multiple client representatives may belong to a project. Client permissions are separate from workspace roles. Owners/Admins manage invitations and access.

### 14. Communication and mediation
ScopePilot is an internal project-delivery mediator between clients, developers, Team Leaders and employees—not a social or general-purpose messaging platform. Use structured, contextual discussions around projects, requirements, tasks and change requests. Client-visible discussions are controlled; internal discussions remain private. Record important decisions. No open-ended social chat or general private messaging in V1 demo.

### 15. Requirement ownership and clarification
Clients can submit requirements. Team members can ask clarification questions. Team Leaders review/refine requirements. Owners/Admins establish approved requirement baselines. Unclear requirements remain Needs Clarification. A requirement is not an approved commitment until it passes the approval process.

### 16. Joint approval and baseline versioning
Team Leader approval is required to validate technical feasibility, effort, workload and delivery impact. Owner/Admin approval is required for changes affecting agreed scope, budget or delivery commitments. Both approvals are required for consequential baseline changes. Team Leaders can raise concerns and request revisions without escalating every discussion. Approved changes create a new immutable baseline version; record approvals, rejections and revisions. Team Leader technical approval does not independently commit the agency commercially.

### 17. Disagreements and lifecycle-aware change control
If either required approver rejects a consequential change, it cannot proceed as approved. Record the reason; allow revision/resubmission and alternatives. Disagreements enter Needs Resolution. No baseline changes until required approvals are complete.

**Before deployment/client acceptance:** strict change control. Changes to agreed deliverables or commitments require formal assessment, Team Leader and Owner/Admin approvals, and client confirmation when their agreement changes.

**After deployment/client acceptance:** controlled flexibility for defects, incidents, enhancements and new features. Each request is classified and assessed. Required technical/business/client approvals still apply. Preserve deployed baselines and history. Post-deployment flexibility is not automatic implementation.

### 18. Request classification
Distinguish:
- Defect: delivered functionality fails agreed requirements/acceptance criteria; investigate against contract and warranty/maintenance terms.
- Production incident: service disruption or critical operational problem; expedited response.
- Enhancement: improvement to existing functionality; assess effort, feasibility and release impact.
- New feature: additional functionality outside existing scope; treat as a new change proposal.
A defect is not automatically paid extra scope. Commercial responsibility depends on the agreement. Incidents are prioritized by urgency.

### 19. Release management
Track release versions and which approved requirements/tasks each release includes. Release states: Development, Testing, Ready for Deployment, Deployed and Rolled Back. Record client acceptance where required. Keep rollback records and link post-deployment incidents/defects to releases. Preserve original approved baselines across releases.

### 20. Project closure and handover
Use a simplified demo closure workflow: account for agreed requirements; document outstanding defects/issues; record deployment/release details; record client acceptance or concerns; provide handover documentation where applicable; record warranty/maintenance responsibilities if agreed; close only when required closure conditions are met. Closed projects are read-only historical records; post-deployment work follows a new change cycle.

### 21. Product success metrics
Use demonstration KPIs: scope-change assessment time; requirement clarification rate; change approval cycle time; delivery impact visibility; baseline change traceability; client–team alignment. Use simulated data and label it illustrative, not real customer results.

### 22. Flagship demonstration scenario
Use one coherent scenario: a digital agency building an e-commerce website for a client. Demonstrate requirements, clarification, baseline approval, task estimates/dependencies, schedule/risk, a mid-development scope change, impact assessment, joint approval, revised baseline, deployment/client acceptance, post-deployment defect or enhancement and KPI dashboard.

### 23. Product experience
One shared workspace with role-aware dashboards, not separate applications:
- Owner: portfolio, commitments, approvals and delivery risks.
- Team Leader: workload, requirements, blockers and change reviews.
- Developer/Member: assigned tasks, dependencies, estimates and clarifications.
- Client: progress, approved requirements, change requests and decisions.
- Viewer: read-only authorized project information.
Navigation and permissions adapt to role. Protect internal information.

### 24. AI positioning
Position AI as a Project Delivery Intelligence Assistant, not an autonomous project manager. It can summarize/clarify requirements, explain calculated findings, highlight evidence-backed risks, summarize contextual discussions/decisions and suggest options. Deterministic calculations remain authoritative. AI cannot approve, modify baselines or autonomously reassign work. Core demo works without an external AI service.

### 25. AI recommendations and evidence
AI recommendations must be based on actual project data and calculated findings; explain why they are suggested; reference affected requirements/tasks/dependencies/estimates/risks; distinguish facts, calculated projections and AI suggestions; disclose uncertainty; suggest alternatives where useful; never fabricate missing data. Human decision-making remains mandatory. AI unavailability must not block core workflows.

### 26. Demo data
Use a fictional agency and client with fictional users and realistic requirements, tasks, estimates and dependencies. Include normal, delayed and at-risk scenarios, plus pre- and post-deployment changes. Label simulated data and AI-generated recommendations. Do not use real customer/confidential data. Provide a demo reset.

### 27. Usability and onboarding
Provide role-based onboarding, guided workspace/project setup, preloaded demo project, contextual explanations, clear pending-approval/blocker/risk indicators, helpful empty states and simple navigation. First-time users should understand the product and complete a basic workflow without extensive training.

### 28. Notifications
Provide role-aware in-app notifications for actionable events: Team Leaders (reviews, blockers, change requests); Owners/Admins (business approvals and delivery risks); clients (clarifications, decisions and confirmations); developers (assignments, dependency changes and blockers). Remind for overdue actions and approaching milestones. Link each notification to its project/task/change request. No email integration required for the demo.

**Employee assistance extension:** Employees can report Unable to Complete, Need Assistance, Request Extension or Report Blocker. Capture reason, affected task, remaining effort and expected delay if known. Notify Team Leader; support review, assistance, clarification, schedule review or recommended reassignment. Reporting does not automatically change deadlines or penalize employees. Show concern status and resolution. Reassignment requires authorized action. If the concern affects project commitments, update potential impact and obtain required approvals.

### 29. Escalation
If a Team Leader does not respond within a configurable response period, escalate an unresolved employee concern to Admin/Owner. Preserve original report and timestamps, show elapsed unresolved time, avoid automatic blame/penalty, and record resolution and responsible person.

### 30. Workload and task fairness
Compare assigned effort with individual available working hours. Highlight overload/underutilization and conflicting commitments considering deadlines, dependencies and priorities. Team Leaders may explore reassignment suggestions but tasks are never automatically reassigned. Employees can raise workload concerns. Show evidence. This is workload planning, not employee surveillance or performance ranking.

### 31. Project risk management
Provide a centralized project risk register. Team Leaders and members can report risks. Record description, cause, impact, severity and owner. Distinguish risks from realized issues. Track mitigation recommendations and statuses Open, Monitoring, Mitigated and Closed. Link risks to affected tasks/requirements. Show unresolved high-priority risks on the project dashboard. AI explanations/recommendations must be evidence-grounded.

## Cross-cutting product principles

- Human approval for consequential changes; no autonomous AI mutation.
- Deterministic calculations are authoritative; AI is optional and explanatory.
- Preserve immutable approved baselines and auditable decisions.
- Clearly distinguish facts, calculated projections and suggestions.
- Respect project/client/internal visibility boundaries.
- Keep the experience a portfolio demo; prioritize product story and usability over production infrastructure.
- Do not present simulated metrics as actual customer outcomes.

## Implementation note

This register records approved product direction, not implementation completion. Detailed formulas, thresholds, sample values, UI behavior and technical choices may still need design specification. Where a detail is not explicitly settled here, use a reversible demo-friendly default and document it rather than reopening routine approvals.
