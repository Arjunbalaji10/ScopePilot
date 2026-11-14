# ScopePilot — Conceptual Data Model

## Status
This model reflects the approved portfolio-demo scope. It guides UX and prototype planning; it is not a migration specification. Implement only entities needed by prioritized journeys.

## Relationship overview
Workspace → WorkspaceMembership → User  
Workspace → Project → ProjectMembership → User  
Project → Requirements ↔ Tasks → TaskDependencies  
Project → Baselines → BaselineItems  
Project → ChangeRequests → Revisions → ImpactAssessments → ApprovalDecisions  
Project → Milestones, Risks, Releases, Discussions, Notifications, EmployeeConcerns and AuditEvents.

Tasks support directed Finish-to-Start dependencies. Risks, discussions, releases and concerns may reference relevant project entities.

## Identity and access
- **User:** id, email, password hash, display name, timestamps and active state. Email/password only if authentication is implemented. Never store plaintext passwords or Gmail account passwords.
- **Workspace:** name, owner, timestamps and active/archive state.
- **WorkspaceMembership:** user, workspace and predefined role: Owner, Admin, Member or Viewer.
- **ProjectMembership:** user, project and project-specific responsibility/permission. Client access is project-scoped and separate from workspace roles. Team Leader is a project responsibility, not automatically Admin.
- A user may belong to multiple workspaces. Workspace data must be isolated.

## Project planning and delivery
- **Project:** workspace, name, description, client-facing summary, lifecycle status, target date, calendar settings, current baseline reference and timestamps. Default calendar is 8 hours/day, Monday–Friday.
- **Requirement:** project, title, description, expected outcome, acceptance criteria, requester/source, priority, status and timestamps. Needs Clarification is not an approved commitment.
- **Task:** project, title, description, linked requirements, one primary assignee or none, status, priority, optimistic/most-likely/pessimistic estimates, actual effort, remaining effort, actual dates and timestamps. Estimate unit is person-hours.
- **TaskDependency:** prerequisite task, dependent task and Finish-to-Start type. Reject self-reference and cycles.
- **Milestone:** project, title, target date, status, linked work and completion metadata.
- **EmployeeConcern:** task, reporter, type (Unable to Complete, Need Assistance, Request Extension, Report Blocker), reason, description, remaining effort/expected delay if known, status, reviewer, response deadline, escalation and resolution. No automatic penalty, reassignment or deadline change.

## Scope governance
- **Baseline/BaselineItem:** project, sequential version, approval metadata, source decision, effective timestamp and immutable snapshots of approved requirements, tasks, estimates and commitments. Never overwrite an old baseline.
- **ChangeRequest:** project, requester, classification (defect, incident, enhancement, new feature), rationale, state, pinned base baseline and timestamps.
- **ChangeRevision:** exact proposed changes and before/after values. A submitted revision is immutable.
- **ImpactAssessment:** exact revision and baseline, calculation/rule version, timestamp, input snapshot, structured findings, potential effort/schedule/capacity/commitment impact and assumptions. These are projections, not guarantees.
- **ApprovalDecision:** append-only decision for a specific revision and stage (technical, business, client confirmation), with trusted actor, timestamp and rationale. Consequential changes require Team Leader technical and Owner/Admin business approval; client confirmation applies when their agreement changes.

## Risks, releases and communication
- **Risk:** project, description, cause, impact, severity, owner, status (Open, Monitoring, Mitigated, Closed), linked tasks/requirements and mitigation. Distinguish potential risks from occurred issues.
- **Release/ReleaseItem:** release version, state (Development, Testing, Ready for Deployment, Deployed, Rolled Back), deployment/rollback metadata, acceptance and links to included approved work.
- **Discussion/Comment:** contextual thread on project, requirement, task or change request; explicit client-visible or internal-only visibility. No general-purpose direct messaging.
- **Notification:** recipient, event, related entity, read state, timestamp and action link. In-app only for the demo.
- **AuditEvent:** append-only record of consequential actions with trusted actor, timestamp, target and minimal metadata.

## Calculations and AI
- **CalculationRun/Finding:** calculation type, input snapshot/fingerprint, rule-set version, timestamp, structured summary and findings. Findings carry stable codes, severity, affected entities, values and units. Backend deterministic calculations are authoritative.
- **Explanation:** optional derived artifact referencing a calculation run and cited finding IDs. AI text is advisory and never feeds authoritative calculations or approval state.

## Integrity and implementation notes
Use PostgreSQL foreign keys/check constraints for core invariants, UTC timestamps, explicit numeric units, and project/workspace-scoped access. Snapshot approved baseline data rather than relying on mutable current records. Prefer archive/read-only history over casual hard deletion. Use fictional deterministic seed data. Prioritize the requirement → task → baseline → change → impact → approval path; do not implement every conceptual entity at once.
