# ScopePilot — Domain Rules

## Status
These rules translate approved product decisions into a consistent demo model. Detailed edge-case semantics can be finalized during UX and calculation specification. They are not evidence that behavior has been implemented.

## 1. Authority and evidence
- **Approved:** Deterministic backend calculations are authoritative.
- **Approved:** AI may explain grounded findings but cannot replace calculations, approve changes or mutate project state.
- **Approved:** Impact results are potential scenarios, not guaranteed outcomes.
- **Demo rule:** Material findings identify supporting requirements, tasks, dependencies, estimates, capacity or commitments.
- **Demo rule:** UI distinguishes confirmed facts, calculated projections and AI suggestions.
- **Demo rule:** Core flows work with AI disabled or unavailable.

## 2. Workspace, roles and visibility
- Workspace roles: Owner, Admin, Member and Viewer.
- Users may belong to multiple workspaces; workspace data is isolated.
- Client access is project-level, separate from workspace roles.
- Team Leader is a project responsibility with technical review authority; it is not automatically equivalent to Admin.
- Every backend operation checks access to the specific workspace, project and resource.
- Clients see agreed progress, milestones, approved requirements, change requests, authorized discussion and decisions.
- Clients do not see internal estimates/assignments, private employee discussions or workspace controls.
- Internal-only discussion content must never be returned to client-facing views.

## 3. Requirements and tasks
- Requirements describe client outcomes; tasks describe delivery work.
- One requirement may link to multiple tasks.
- Unclear requirements remain Needs Clarification and are not approved commitments.
- Only reviewed/approved requirements enter the baseline.
- Each task has one primary assignee or remains unassigned; assignees must be authorized project members.
- Task statuses: Not Started, In Progress, Blocked, Completed.
- Actual effort is separate from estimated effort.
- Completed tasks retain actual dates and effort; recalculation must not rewrite historical actuals.

## 4. Estimates, dependencies and schedule
- Estimate unit: person-hours.
- Each task has optimistic (O), most likely (M) and pessimistic (P) estimates.
- Planning estimate: E = (O + 4M + P) / 6.
- Sum task planning estimates for planned effort; effort is not calendar duration.
- Track actual effort separately.
- Default calendar: 8 hours/day, Monday–Friday; workspace owner may configure working days/hours.
- V1 dependencies are Finish-to-Start only. Reject self-dependencies and cycles.
- A dependent task cannot start until all prerequisites are complete.
- In-progress tasks use remaining effort for forward projection; blocked tasks expose the blocker.
- Capacity compares assigned effort with available working hours. Show conflicts; never auto-reassign.
- Delivery status is On Track, At Risk or Delayed with visible evidence. Do not invent risk probabilities or guarantee dates.
- Before implementing the calculation engine, specify rounding, partial-day scheduling, resource allocation and threshold semantics with golden examples.

## 5. Baselines and change requests
- Initial approved scope creates baseline version 1.
- Approved baseline snapshots are immutable.
- Every change request pins the baseline it was assessed against.
- Submitted revisions are immutable; later edits require a new revision/resubmission.
- Impact identifies affected requirements, tasks, dependencies and commitments, plus potential effort, schedule, capacity and risk effects where data supports them.
- Rejection does not change the baseline.
- Approval of a consequential change creates a new baseline; prior versions remain available.
- If the pinned baseline is no longer current, do not approve against stale data. Reassess against the current baseline.
- Concurrent requests may exist, but stale assessments must be refreshed before approval.
- Disclose missing inputs and assumptions rather than fabricating impact.

## 6. Approval authority
- Team Leader reviews technical feasibility, effort, workload, dependencies and delivery impact.
- Owner/Admin reviews business priority and changes to agency commitments.
- Both approvals are required for consequential baseline changes.
- Client confirms when agreed deliverables, cost or delivery dates change.
- Requesters cannot approve their own consequential changes.
- Mandatory requests receive highest priority but are not automatically approved.
- Routine low-risk changes may be delegated to Team Leader within policy; consequential baseline changes still require business approval.
- Emergency production fixes may receive expedited technical authorization followed by documented review.
- Rejections record a reason; requests needing revision enter Needs Resolution.
- Alternatives include scope reduction, date extension or authorized resource allocation changes.
- No baseline change until all required approvals and confirmations are complete.

## 7. Change classification and lifecycle
- **Defect:** delivered behavior fails an agreed requirement/acceptance criterion. Commercial responsibility depends on warranty/contract; it is not automatically paid new scope.
- **Production incident:** service disruption or critical operational issue; prioritize response and document expedited authorization.
- **Enhancement:** improvement to existing functionality; assess effort, dependencies and release/commitment impact.
- **New feature:** functionality outside agreed scope; create a change proposal and approval path.
- Pre-deployment changes use strict scope control.
- Post-deployment changes remain controlled but distinguish defects, incidents, enhancements and new features.
- Deployed baselines are preserved; post-deployment work never silently rewrites them.

## 8. Employee concerns and workload fairness
- Employees may report Unable to Complete, Need Assistance, Request Extension or Report Blocker.
- Capture task, reason, remaining effort/expected delay if known and report time.
- Notify Team Leader; support assistance, clarification, schedule review or suggested reassignment.
- If project commitments may change, use impact assessment and required approvals.
- If Team Leader response exceeds the configured period, escalate to Admin/Owner and preserve timestamps.
- Reporting creates no automatic penalty, deadline change or reassignment.
- Workload views compare assigned effort with availability and explain conflicts.
- No employee surveillance or performance ranking.

## 9. Risks, releases and closure
- A risk is a possible future event; an issue/incident has occurred.
- Risk records include description, cause, impact, severity, owner, status and linked work.
- Risk statuses: Open, Monitoring, Mitigated, Closed.
- Show high-priority unresolved risks on the dashboard.
- Release states: Development, Testing, Ready for Deployment, Deployed, Rolled Back.
- Track release version, included approved work, rollback and client acceptance where required.
- Close only after requirements are accounted for, outstanding issues recorded, release/deployment history available, acceptance/concerns noted and handover/warranty responsibilities recorded where applicable.
- Closed projects are read-only; further work uses a new post-deployment change cycle.

## 10. Discussion and notifications
- Discussions are contextual to project, requirement, task or change request.
- Client-visible and internal-only content have explicit visibility.
- No general-purpose chat or private messaging.
- Notifications are in-app, role-aware and linked to the relevant entity; avoid notification overload.

## 11. AI safeguards
- Provide only minimum approved evidence for an explanation.
- AI suggestions cite supplied entities/findings.
- Omit unsupported values, probabilities and claims.
- Label AI text advisory and non-authoritative.
- AI cannot write, approve, reassign, change deadlines or alter baselines.
- AI failure never blocks deterministic workflows.
- Prefer template explanations if model integration adds cost or complexity.

## 12. Demo data
All sample organizations, users, clients, projects, tasks, estimates, risks and metrics are fictional. Label illustrative KPIs and simulated AI content. Provide a reset to a known demo state.
