# ScopePilot — Core User Journeys

These journeys describe the approved product direction. They are demo journeys, not proof that the workflows have been implemented.

## 1. Client submits a requirement
**Actor:** Client

1. Client opens the project view they were invited to.
2. Client reviews project context and submits a requirement with expected outcome and relevant detail.
3. Requirement is marked Needs Clarification until reviewed.
4. Team members ask focused questions in the requirement discussion.
5. Team Leader reviews/refines it and resolves ambiguity.
6. Owner/Admin includes it in the approved scope baseline when ready.
7. Client can see its status and the agreed version.

**Outcome:** A clear requirement becomes a traceable commitment only after approval.

## 2. Team plans and tracks delivery
**Actors:** Team Leader, Developer/Member

1. Team Leader links one or more tasks to each approved requirement.
2. Tasks receive PERT estimates, primary assignee (or remain unassigned), priority and Finish-to-Start dependencies.
3. ScopePilot calculates planning effort and a calendar-based schedule projection.
4. Developer views assigned work, prerequisites and expected effort.
5. Developer updates status and actual effort, or reports a blocker/assistance need.
6. Team Leader reviews workload, blockers and project risks; any assignment or schedule change is a deliberate human action.
7. Dashboard reflects current delivery evidence.

**Outcome:** Team can trace progress and risks from tasks back to agreed requirements.

## 3. Team assesses a proposed scope change
**Actors:** Client or authorized team member; Team Leader; Owner/Admin

1. A change request is created against the current approved baseline.
2. Requester describes the requested outcome and reason; request is classified (for example, enhancement or new feature).
3. ScopePilot identifies affected requirements, tasks and dependencies.
4. Deterministic calculations estimate potential effort and schedule/capacity effects using current planning inputs.
5. The UI presents the before/after view, assumptions, affected commitments and risks.
6. Team Leader reviews technical feasibility, effort, workload and delivery impact.
7. Owner/Admin reviews business priority and commitment implications.
8. If deliverables, cost or agreed dates change, the client confirms the revised agreement.
9. If an approver raises a concern, the request enters Needs Resolution; the requester may revise and resubmit or consider alternatives.
10. Only after all required approvals does ScopePilot create a new immutable baseline and record the decision.

**Outcome:** People see trade-offs before committing. Impact is a projection, not a guarantee.

## 4. Employee reports a blocker or workload concern
**Actor:** Developer/Member

1. Employee opens an assigned task and selects Unable to Complete, Need Assistance, Request Extension or Report Blocker.
2. Employee records the reason and remaining effort/expected delay if known.
3. ScopePilot records the report and notifies the Team Leader.
4. Team Leader reviews, assists, requests clarification or considers a schedule/assignment change.
5. If project commitments may change, ScopePilot routes the proposed change through impact assessment and required approvals.
6. If no response occurs within the configured response period, the concern escalates to Admin/Owner.
7. Employee can see report status and resolution.

**Guardrails:** Reporting does not penalize the employee, automatically change a deadline or automatically reassign work.

## 5. Owner/Admin monitors commitments and risks
**Actor:** Owner/Admin

1. Owner/Admin opens the workspace/project dashboard.
2. Dashboard highlights milestone status, target-date projection, high-priority risks, workload conflicts and pending business approvals.
3. Owner/Admin opens an item to inspect supporting requirements, tasks, dependencies and decisions.
4. Owner/Admin approves/rejects business commitments or requests clarification/revision.
5. Important decisions remain in project history.

**Outcome:** Business oversight is based on traceable delivery evidence rather than unsupported risk scores.

## 6. Client follows delivery and confirms changes
**Actor:** Client

1. Client views milestones, progress, approved requirements and agreed dates.
2. Client participates in authorized requirement/change-request discussions.
3. Client sees the assessed consequences of a proposed change.
4. Client confirms revised deliverables/cost/dates when their agreement changes.
5. Client can view the decision and resulting agreed baseline.

**Guardrails:** Client cannot view private employee discussions or internal estimates/assignments.

## 7. Team handles deployment and post-deployment work
**Actors:** Team Leader, Owner/Admin, Client

1. Team tracks release through Development, Testing, Ready for Deployment, Deployed or Rolled Back.
2. Release records link to included approved requirements/tasks.
3. Client acceptance or concerns are recorded where required.
4. A defect, incident, enhancement or new feature is classified and assessed according to the agreement and urgency.
5. Post-deployment work uses a controlled change cycle; it does not silently rewrite the deployed baseline.
6. Project closes after the simplified closure conditions are met; closed history remains read-only.

## 8. AI explains delivery evidence
**Actor:** Authorized team member

1. User requests an explanation of a calculated impact or risk.
2. ScopePilot provides only relevant, approved project facts and deterministic findings to the optional AI layer.
3. AI returns a concise explanation and possible options, referencing the supplied evidence.
4. UI distinguishes facts, calculated projections and AI suggestions.
5. Human user makes the decision.

**Guardrails:** AI cannot calculate authoritative values, approve a change, alter project state or reassign tasks. Core workflows continue when AI is unavailable.

## Cross-journey experience requirements
- Make role and visibility boundaries understandable.
- Keep requirement, task, change request, risk, release and decision history linked.
- Distinguish draft, submitted, approved, rejected and Needs Resolution states.
- Show assumptions and evidence beside projected impact.
- Confirm consequential actions and describe their effect on the baseline.
- Avoid unsupported probabilities or guarantees.
- Use fictional data and label simulated metrics.
