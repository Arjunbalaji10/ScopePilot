# ScopePilot — User Flow Map

## Purpose
Map the flagship product journey and role handoffs before wireframing. This flow represents the approved product direction; it is not an implementation claim.

## 1. End-to-end flagship flow

```mermaid
flowchart TD
    A[Open ScopePilot demo] --> B[Workspace overview]
    B --> C[Open e-commerce project]
    C --> D[Review client requirements]
    D --> E{Requirement clear?}
    E -- No --> F[Ask clarification in context]
    F --> G[Team Leader refines requirement]
    G --> D
    E -- Yes --> H[Approve requirement into scope]
    H --> I[Create linked tasks]
    I --> J[Add PERT estimates and dependencies]
    J --> K[Review schedule and workload]
    K --> L[Approve initial baseline]
    L --> M[Track delivery progress]
    M --> N[Client/team submits scope change]
    N --> O[Classify request and pin baseline]
    O --> P[Calculate impact]
    P --> Q[Review affected requirements, tasks, dates and capacity]
    Q --> R[Team Leader technical review]
    R --> S{Technically acceptable?}
    S -- No --> T[Needs Resolution / revise request]
    T --> N
    S -- Yes --> U[Owner/Admin business review]
    U --> V{Business approval?}
    V -- No --> T
    V -- Yes --> W{Client agreement changes?}
    W -- Yes --> X[Client confirms revised agreement]
    W -- No --> Y[Create new immutable baseline]
    X --> Y
    Y --> Z[Continue delivery and track release]
    Z --> AA[Client acceptance / post-deployment cycle]
    AA --> AB[Project closure and history]
```

## 2. Role handoff map

| Stage | Primary actor | Supporting actor | Product evidence |
|---|---|---|---|
| Requirement submission | Client | Team Leader | Requirement record and acceptance criteria |
| Clarification | Team Leader / Member | Client | Contextual questions and resolved status |
| Delivery planning | Team Leader | Developer/Member | Linked tasks, PERT estimates, dependencies |
| Initial baseline | Owner/Admin | Team Leader | Approved scope snapshot |
| Daily delivery | Developer/Member | Team Leader | Status, actual effort, blockers |
| Change proposal | Client or authorized team member | Team Leader | Request type, rationale and base baseline |
| Impact assessment | ScopePilot calculation engine | Team Leader | Affected work, effort/schedule/capacity projection |
| Technical review | Team Leader | Developer/Member | Feasibility and delivery rationale |
| Business review | Owner/Admin | Team Leader | Priority and commitment decision |
| Client confirmation | Client | Owner/Admin | Revised agreement confirmation |
| Baseline update | ScopePilot after required approvals | Owner/Admin | New immutable baseline and audit record |
| Release and closure | Team Leader / Owner | Client | Release state, acceptance and handover record |

## 3. Change request decision flow

```mermaid
flowchart TD
    A[Create change request] --> B[Select classification and describe reason]
    B --> C[Pin current approved baseline]
    C --> D[Assess affected requirements, tasks and dependencies]
    D --> E[Calculate potential effort, schedule and capacity impact]
    E --> F{Assessment complete and current?}
    F -- No --> G[Show missing inputs or stale assessment]
    G --> D
    F -- Yes --> H[Team Leader technical review]
    H --> I{Technical approval?}
    I -- No --> J[Needs Resolution; record reason]
    J --> K[Revise or consider alternatives]
    K --> A
    I -- Yes --> L[Owner/Admin business review]
    L --> M{Business approval?}
    M -- No --> J
    M -- Yes --> N{Client commitment changes?}
    N -- Yes --> O[Request client confirmation]
    O --> P{Client confirms?}
    P -- No --> J
    P -- Yes --> Q[Create new baseline]
    N -- No --> Q
    Q --> R[Record decisions and audit history]
```

## 4. Employee concern flow

```mermaid
flowchart TD
    A[Employee opens assigned task] --> B[Report blocker, assistance, unable to complete or extension]
    B --> C[Record reason and remaining effort if known]
    C --> D[Notify Team Leader]
    D --> E{Team Leader responds in configured period?}
    E -- Yes --> F[Review and provide help / clarification / schedule recommendation]
    E -- No --> G[Escalate to Admin/Owner]
    G --> F
    F --> H{Project commitment affected?}
    H -- No --> I[Record resolution]
    H -- Yes --> J[Create impact assessment and required approvals]
    J --> I
    I --> K[Employee sees status and outcome]
```

## 5. AI explanation flow

```mermaid
flowchart TD
    A[User opens calculated impact or risk] --> B[Request explanation]
    B --> C[Provide minimum approved evidence and findings]
    C --> D{AI available and enabled?}
    D -- No --> E[Show deterministic findings and template explanation]
    D -- Yes --> F[Generate advisory explanation]
    F --> G[Validate references and remove unsupported claims]
    G --> H[Label as AI suggestion]
    E --> I[Human reviews evidence]
    H --> I
    I --> J[Human makes decision]
```

## 6. Navigation flow for prototype

Workspace overview → Project overview → Requirements → Requirement detail → Task board → Task detail → Scope changes → Change detail → Impact assessment → Approval review → Baseline history.

Parallel role entry points:
- Client: Invited project overview → Requirements/progress → Change requests → Client confirmation.
- Developer: My work → Task detail → Clarification/concern → Concern status.
- Team Leader: Project overview → Delivery/workload → Requirements → Technical review → Risks.
- Owner/Admin: Workspace overview → Project commitments → Business approvals → Risks and history.

## 7. Important states to wireframe
- Empty workspace / no projects.
- Project with no requirements.
- Requirement Needs Clarification.
- Requirement approved and linked to tasks.
- Task blocked by prerequisite.
- Capacity conflict / projected delay.
- Change request draft, submitted, Needs Resolution, awaiting technical review, awaiting business approval, awaiting client confirmation, approved and rejected.
- Stale impact assessment because baseline changed.
- AI disabled/unavailable.
- Employee concern awaiting response and escalated.
- Release rolled back / client acceptance pending.
- Closed project read-only.

## 8. Prototype acceptance
A reviewer should be able to follow the e-commerce scenario from requirement to revised baseline, understand who acts at each handoff, see what evidence informs the impact assessment, and understand why a change cannot proceed without the required approvals. The client view must demonstrate a clear visibility boundary from internal agency work.
