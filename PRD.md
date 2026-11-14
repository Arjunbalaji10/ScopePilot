# Product Requirements Document — ScopePilot V1.0

## 1. Document status

This is a Phase 0 baseline. The repository contained no prior product artifacts or implementation at preparation time. Requirements explicitly stated in the project brief are **Approved**. The product definition and detailed behavior below are **Proposed** or **Unresolved** as labeled.

## 2. Product hypothesis — Unresolved

ScopePilot is assumed to help a delivery team:

1. describe a project's scope as structured items;
2. establish a human-approved baseline;
3. calculate a deterministic estimate and summary from that baseline;
4. model a proposed scope change without mutating the baseline;
5. calculate and explain the change's impact; and
6. require a human to approve or reject the change.

This definition is plausible from the name and guardrails, but is not evidenced by repository content. Product ownership must confirm or replace it before feature implementation.

## 3. Problem statement — Proposed

Project scope and estimates often drift across documents and conversations. Teams need one traceable representation of what was approved, what is proposed, and what deterministic effect a change has. Explanations may improve comprehension, but neither generated text nor an automated agent should silently change a commitment.

## 4. Goals

### Approved

- Use authoritative deterministic calculations.
- Restrict AI to explanations grounded in calculated findings.
- Require human approval for consequential changes.
- Deliver with a React/TypeScript frontend, FastAPI backend, and PostgreSQL in a modular monolith.
- Depend on no paid product or infrastructure service.

### Proposed

- Make baseline versus proposed scope visually and semantically distinct.
- Preserve an auditable history of approvals and rejections.
- Make every impact result reproducible from stored inputs and a versioned rule set.
- Allow the core product to function when AI is disabled or unavailable.

## 5. Personas — Unresolved

The proposed roles are:

- **Editor**: creates projects, edits draft scope, and submits baselines or changes.
- **Approver**: approves/rejects baselines and change requests.
- **Viewer**: reads projects, findings, and history.

Whether one person may hold multiple roles, and whether V1.0 needs real authorization rather than attribution only, remain unresolved.

## 6. Functional requirements

| ID | Requirement | Status |
|---|---|---|
| FR-01 | Create and update a project record. | Proposed |
| FR-02 | Add, edit, order, and remove scope items while the scope is a draft. | Proposed |
| FR-03 | Validate all inputs used by calculations. | Proposed |
| FR-04 | Calculate totals and summaries deterministically on the backend. | Approved principle; formula unresolved |
| FR-05 | Submit a draft baseline for approval and approve or reject it explicitly. | Proposed |
| FR-06 | Freeze an immutable snapshot when a baseline is approved. | Proposed |
| FR-07 | Create a change request against one approved baseline without changing that baseline. | Proposed |
| FR-08 | Present a field-level diff and deterministic impact findings. | Proposed |
| FR-09 | Approve or reject a change request and record actor, time, and rationale. | Approved principle; workflow proposed |
| FR-10 | On approval, create a new baseline version atomically. | Proposed |
| FR-11 | Optionally request a plain-language explanation derived only from stored inputs and findings. | Approved constraint; provider/availability unresolved |
| FR-12 | Clearly label AI output as explanatory and non-authoritative. | Proposed |
| FR-13 | View baseline and change history. | Proposed |

## 7. Non-functional requirements

- **Correctness:** decimal/numeric calculations use defined rounding and never binary floating point for authoritative stored values.
- **Traceability:** an impact result records its input snapshot, rule-set version, and calculation time.
- **Integrity:** state transitions and their audit event commit in one database transaction.
- **Security:** validate at the API boundary; do not expose secrets or model credentials to the browser.
- **Accessibility:** proposed target is WCAG 2.2 AA for core journeys; confirmation required.
- **Performance:** no numeric target is approved. Proposed local target is p95 under 500 ms for non-AI API reads at expected V1 scale; scale itself is unresolved.
- **Availability:** the deterministic workflow remains usable without AI.
- **Privacy:** do not send project content to an AI provider without an approved provider, policy, and user action.

## 8. Success measures — Unresolved

Instrumentation and targets require owner approval. Candidate measures are:

- percentage of proposed changes with a computed impact before approval;
- percentage of approvals with complete attribution and rationale;
- calculation reproducibility across repeated runs;
- time from change creation to an informed decision;
- frequency of AI explanations rejected as inconsistent with findings (target should be zero, with feedback mechanism still unresolved).

## 9. Risks and mitigations

| Risk | Mitigation |
|---|---|
| Product intent differs from the hypothesis. | Confirm the product definition before feature work. |
| Estimate formula is treated as obvious and later changes. | Approve a formula specification and version it before implementing calculations. |
| AI introduces unsupported claims. | Build explanations from an allow-listed evidence payload; validate references; make AI optional. |
| Approval semantics are ambiguous. | Define roles, self-approval, concurrency, and effective-date rules first. |
| Premature infrastructure increases cost and maintenance. | One deployable backend, one frontend, one PostgreSQL database; no queue/cache/vector DB by default. |

## 10. Acceptance for Phase 0

Phase 0 is complete when these documents are reviewed, contradictions are resolved, and release-blocking unresolved decisions have named answers. Documentation completion alone does not approve proposed requirements.

