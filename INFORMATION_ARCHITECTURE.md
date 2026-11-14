# ScopePilot — Information Architecture

## Purpose
Define the product structure and navigation for the portfolio demo before drawing individual screens. The experience uses one application with role-aware navigation and permissions, not separate products for each role.

## 1. Product structure

```text
ScopePilot
├── Workspace
│   ├── Overview
│   ├── Projects
│   │   └── Project workspace
│   │       ├── Overview
│   │       ├── Requirements
│   │       │   └── Requirement detail / clarification
│   │       ├── Delivery
│   │       │   ├── Task board
│   │       │   ├── Schedule & milestones
│   │       │   └── Team workload
│   │       ├── Scope changes
│   │       │   └── Change detail / impact assessment
│   │       ├── Approvals
│   │       ├── Risks
│   │       ├── Releases & closure
│   │       └── Activity / baseline history
│   ├── Team
│   └── Workspace settings
├── Notifications
├── Profile
└── Demo guide / reset
```

The client experience enters through an invited project and exposes only client-authorized project sections. It does not expose workspace administration or internal team information.

## 2. Global navigation

### Primary navigation
- **Overview:** workspace-level summary and projects.
- **Projects:** accessible project list and project workspaces.
- **Team:** workspace members and roles, available to authorized Owner/Admin users.
- **Notifications:** actionable in-app events for the current user.

### Utility navigation
- Profile and session actions.
- Workspace switcher where a user belongs to multiple workspaces.
- Demo guide and reset for the portfolio demonstration; reset is a clearly separated demo-only action.

### Project navigation
- **Overview:** project health, milestones, target date, pending decisions and key risks.
- **Requirements:** approved, draft and Needs Clarification requirements.
- **Delivery:** task board, schedule and workload.
- **Scope changes:** requests, classification, impact assessment and decision progress.
- **Approvals:** decisions requiring the current user's authority.
- **Risks:** risk register and mitigation state.
- **Releases:** release lifecycle, client acceptance and closure.
- **Activity:** baseline versions, approvals and consequential project events.

Do not show empty or inaccessible navigation items as dead ends. Hide or explain unavailable sections based on role and project state.

## 3. Role-aware experience

| Role / responsibility | Default landing view | Primary actions | Restricted information |
|---|---|---|---|
| Owner | Workspace overview | Create/manage projects, business approvals, commitments, risks | No access beyond assigned workspace |
| Admin | Workspace/project overview | Manage members, project setup, business approvals within authority | No access beyond assigned workspace |
| Team Leader | Project overview / delivery | Review requirements, plan tasks, manage workload, technical reviews, risks | No automatic access to other workspaces |
| Developer / Member | My work / assigned tasks | Update task progress/actual effort, ask questions, report blockers | Internal project information only as permitted; no business approval by default |
| Client | Invited project overview | View agreed progress, submit requirements/change requests, discuss and confirm changed agreement | No internal estimates/assignments, private employee discussions or workspace settings |
| Viewer | Workspace/project overview | Read authorized information | No mutations or approvals |

Workspace roles remain Owner, Admin, Member and Viewer. Team Leader is a project responsibility and can be assigned to an authorized workspace member. Client is a separate project-level access type.

## 4. Key screen inventory

### Core screens — design first
1. **Demo entry / sign-in:** explain product briefly; allow a guided demo entry. Do not require Google Sign-In.
2. **Workspace overview:** projects, delivery pulse, pending approvals and risks.
3. **Project overview:** project summary, status, target date, milestones, key risks and next actions.
4. **Requirements list/detail:** requirement status, acceptance criteria, linked tasks and clarification thread.
5. **Task board/detail:** status, assignee, PERT estimate, actual effort, prerequisites and linked requirements.
6. **Schedule & workload:** projected milestones, dependency chain and capacity conflicts.
7. **Scope change list/detail:** request type, requester, state, base baseline and affected work.
8. **Impact assessment:** before/after, effort and schedule projection, capacity, dependencies, assumptions and evidence.
9. **Approval review:** technical review, business approval, client confirmation where needed, rationale and audit trail.
10. **Baseline history:** version comparison and immutable decision record.
11. **Client project view:** agreed progress, requirements, milestones, change requests and client decisions.

### Secondary screens — design after core flow
12. Risk register and risk detail.
13. Employee concern submission/status and Team Leader review/escalation.
14. Notifications centre.
15. Release tracking, acceptance and project closure.
16. Team/member management and workspace settings.
17. Demo guide/reset and illustrative KPI detail.

## 5. Information hierarchy

Use the following order on project screens:
1. **What is the state?** Project status, milestone and pending decision.
2. **What needs attention?** Blockers, risks, overdue actions and approvals.
3. **What is affected?** Requirements, tasks, dependencies, people and commitments.
4. **What can the user do?** Role-authorized next actions.
5. **Why is this shown?** Evidence, assumptions, history and explanatory notes.

Impact assessments should present deterministic findings and evidence before optional AI explanation.

## 6. Navigation and interaction rules
- Keep workspace navigation distinct from project navigation.
- Maintain a visible project context when moving between project sections.
- Every detail view should link back to its parent project and relevant linked entities.
- Use status labels consistently across dashboard, lists and details.
- Distinguish internal and client-visible content at the point of creation and display.
- Confirm consequential actions and explain whether they create a new baseline.
- Never rely on hidden buttons as a substitute for backend authorization.
- Use empty states to explain the next useful action.
- Clearly label simulated data and optional AI output.

## 7. Demo-first prioritization
The first prototype should make these screens navigable: Workspace overview → Project overview → Requirements → Task board → Change request → Impact assessment → Approval review → Baseline history. Client view is the parallel perspective for the same project. Secondary areas can be represented by concise entry points until the flagship journey is clear.
