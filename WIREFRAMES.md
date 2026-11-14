# ScopePilot — Low-Fidelity Wireframes

Status: Stage 2 — UX structure and wireframes  
Purpose: Define the information hierarchy, screen layout, key actions, role visibility, and important states before implementation. These are structural wireframes, not final visual designs.

## Shared layout

- **Workspace header:** workspace name, workspace switcher, notifications, profile.
- **Primary navigation:** Overview, Projects, Team (Owner/Admin), Settings (Owner/Admin).
- **Project navigation:** Overview, Requirements, Delivery, Scope Changes, Risks, Releases, Activity & Baselines.
- **Main content:** page title and context, current state, attention items, affected records, primary action, supporting evidence.
- **Role visibility:** hide actions a role cannot perform; do not merely disable them without explanation.
- **Demo data:** all sample people, projects, metrics, and events are fictional and visibly labelled as simulated.

## 1. Workspace overview

**Goal:** Give workspace leaders a concise view of project health and decisions requiring attention.

Layout:
- Header: “Workspace overview”, date range, “Create project” (Owner/Admin).
- Summary row: active projects, projects at risk, overdue milestones, pending approvals.
- Main column: project portfolio table with project, client, delivery status, projected date, open risks, next milestone.
- Attention panel: pending scope approvals, unresolved escalations, overdue clarifications.
- Secondary panel: recent project activity.

Actions:
- Open a project.
- Filter by status or owner.
- Create a project (Owner/Admin).
- Open an approval or escalation item.

Visibility:
- Owner/Admin: portfolio and workspace-level actions.
- Team Leader: projects they lead and their outstanding decisions.
- Member: assigned work and relevant project links.
- Client: does not use this workspace-wide screen.
- Viewer: read-only information permitted by workspace access.

States:
- Empty workspace with guided project setup.
- Normal portfolio.
- At-risk or delayed projects.
- Loading and recoverable error.

## 2. Project overview

**Goal:** Explain the current delivery position and what needs attention.

Layout:
- Project header: name, client, Team Leader, status, target date.
- Summary cards: completion, projected completion, open scope changes, active risks.
- Delivery timeline: milestones with planned and current projected dates.
- “Needs attention” list: blocked tasks, unclear requirements, pending approvals, overdue actions.
- Recent activity and latest baseline summary.

Actions:
- Navigate to requirements, delivery, scope changes, risks, releases, and history.
- Create a scope-change request where permitted.
- Open the evidence behind a status or risk.

Visibility:
- Internal users see permitted estimates, assignments, and internal risks.
- Client sees approved commitments, milestone progress, submitted requests, and decisions; no private employee discussions or internal assignments/estimates.
- Viewer is read-only.

States:
- Planning, active delivery, at risk, delayed, completed/closed.
- No milestones or no approved baseline yet.

## 3. Requirements list and requirement detail

**Goal:** Keep client expectations distinct from implementation tasks and make clarification visible.

List layout:
- Page title and requirement status filters.
- Status groups: Draft, Needs Clarification, Under Review, Approved, Rejected, Delivered.
- Each row: requirement ID/title, priority, owner, linked task count, status, last updated.
- Primary action: submit/add requirement where role permits.

Detail layout:
- Requirement statement and acceptance criteria.
- Origin: client submission or internal entry; submitter and timestamps.
- Clarification thread with visibility labels (client-visible or internal).
- Linked tasks and delivery status.
- Review history and approval/baseline reference.

Actions:
- Client submits a requirement and answers client-visible questions.
- Member asks for clarification.
- Team Leader refines and reviews.
- Owner/Admin establishes the approved baseline.
- Authorized users link or unlink tasks.

States:
- Needs Clarification, Under Review, Approved, Rejected, Delivered.
- Missing acceptance criteria or unresolved questions must be visible, not silently treated as approved.

## 4. Delivery task board and task detail

**Goal:** Show work status, dependencies, ownership, and blockers without becoming a complex workforce-management tool.

Board layout:
- Columns: Not Started, In Progress, Blocked, Completed.
- Task card: title, requirement link, primary assignee, estimated effort, remaining effort (when applicable), dependency/blocker indicator, due context.
- Filters: assignee, requirement, status, milestone.
- Workload summary: assigned effort compared with available working hours.

Task detail:
- Task description and linked requirement(s).
- Acceptance/definition-of-done notes.
- Estimate history: optimistic, most likely, pessimistic, calculated PERT estimate, revision reason.
- Dependencies (Finish-to-Start) and blocked-by list.
- Assignee, status, actual effort, remaining effort, dates.
- Contextual discussion and activity history.

Actions:
- Create/edit tasks according to role.
- Update status and actual/remaining effort.
- Report blocker or request assistance/extension.
- Add or remove valid dependencies; reject cycles and self-dependencies.
- Suggest reassignment only; never auto-reassign.

States:
- Unassigned, blocked by prerequisite, overloaded assignee, completed.
- Invalid dependency attempt with a clear explanation.

## 5. Scope-change detail and impact assessment

**Goal:** Make consequences visible before anyone approves a change.

Request summary:
- Change title, requester, reason, submission date, urgency, status.
- Proposed requirement change and acceptance criteria.
- Client-facing discussion and internal discussion clearly separated.

Impact assessment:
- Affected requirements and tasks.
- Added/changed effort, with assumptions and estimate source.
- Dependency and milestone effects.
- Projected completion before vs. after the proposed change.
- Workload/capacity impact and existing commitments affected.
- Risks, unknowns, and items needing clarification.
- Options: defer, reduce scope, move date, add capacity, or reject; show trade-offs without presenting suggestions as decisions.

Actions:
- Request clarification or revise assessment.
- Team Leader records technical review.
- Owner/Admin records business decision.
- Client confirms when agreed deliverables, cost, or dates change.
- Approval creates a new immutable baseline; rejection or deferral records rationale.

States:
- Draft, Submitted, Needs Clarification, Under Assessment, Awaiting Technical Approval, Awaiting Business Approval, Awaiting Client Confirmation, Approved, Rejected, Deferred, Needs Resolution.
- No approval action for the requester on their own consequential request.

## 6. Approval review

**Goal:** Give each approver the evidence and decision authority relevant to their role.

Layout:
- Request summary and current approval stage.
- Proposed change vs. current approved baseline.
- Impact evidence: effort, schedule, dependencies, workload, risks, affected commitments.
- Previous decisions, comments, and rationale.
- Decision panel with Approve, Request changes/clarification, Reject, or Defer as permitted.

Rules:
- Team Leader records technical approval.
- Owner/Admin records business approval.
- Client confirms when the external agreement changes; client confirmation does not replace agency approval.
- Requester cannot approve their own consequential change.
- Every decision records actor, timestamp, decision, and rationale.

States:
- Waiting for this approver, waiting for another approval, needs resolution, completed.
- Display why an action is unavailable.

## 7. Baseline history

**Goal:** Make the approved project commitment traceable over time.

Layout:
- Current baseline summary and version identifier.
- Chronological baseline timeline.
- Each version shows approval date, approving roles, change reason, and source request.
- Version comparison: requirements, effort, milestones/dates, and affected commitments.
- Link from each baseline version to its scope-change request and approval record.

Actions:
- View and compare historical versions.
- Export or print may be considered later; not required for the first interactive prototype.
- No editing historical baselines.

States:
- Initial baseline not yet established.
- One baseline.
- Multiple approved revisions.
- Read-only project closure history.

## 8. Client project view

**Goal:** Give clients clarity and a safe way to participate without exposing internal agency operations.

Layout:
- Project name, overall status, target date, and concise status explanation.
- Approved requirements and acceptance criteria.
- Milestones and client-visible progress.
- Client-submitted requirements and open clarification questions.
- Scope-change requests, impact summary appropriate for client visibility, and decisions.
- Client-visible activity and release/acceptance information.

Actions:
- Submit a requirement.
- Answer clarification questions.
- Submit a scope-change request.
- Confirm a proposed change when the agreement changes.
- Review delivery and provide acceptance where applicable.

Never show:
- Internal employee conversations.
- Private workload/assignment details.
- Internal-only risk notes.
- Internal estimates or deliberations not approved for client visibility.

States:
- No requirements submitted, clarification needed, active delivery, awaiting client confirmation, ready for acceptance, closed.

## Cross-screen interaction rules

1. Every status must have a clear meaning and next action.
2. Show the evidence behind delivery status, schedule projection, and risk findings.
3. Distinguish approved baseline values from proposed changes and current forecasts.
4. Keep client-visible and internal discussion visibly separate.
5. Use confirmation and rationale capture for consequential decisions.
6. Do not make AI suggestions look like approved facts or decisions.
7. Keep the demo focused on one end-to-end fictional e-commerce project.

## Prototype build order

1. Workspace overview and project overview.
2. Requirements list/detail.
3. Task board/detail.
4. Scope-change request and impact assessment.
5. Approval review and baseline history.
6. Client project view.
7. Add secondary screens: risks, releases, notifications, employee concerns, settings, and demo guide.

## Wireframe acceptance checklist

- [ ] Each core screen has a clear primary purpose.
- [ ] Primary actions match the approved role and approval rules.
- [ ] Client and internal information are separated.
- [ ] Baseline, proposed change, and forecast are visually distinct.
- [ ] Loading, empty, error, and important business states are represented.
- [ ] The screens support the flagship e-commerce scenario end to end.
- [ ] No screen implies autonomous approval, auto-reassignment, or guaranteed forecasts.
