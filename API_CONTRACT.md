# ScopePilot — Conceptual API Contract

## Status
This is a proposed API surface for the portfolio demo, not a frozen OpenAPI specification. Implement routes only when their user journey is prioritized. FastAPI-generated OpenAPI becomes the source of truth once the API exists.

## Conventions
- Base path: /api/v1.
- JSON field names use snake_case; identifiers are opaque UUID strings.
- Timestamps use RFC 3339 UTC.
- Numeric values include explicit units; authoritative decimal values must not depend on browser floating-point arithmetic.
- Actor identity comes from trusted server-side session context, never request-body actor IDs.
- Every project-scoped operation checks workspace and project access.
- Use resource versions/ETags for conflicting edits; choose the exact mechanism during implementation.
- Errors use stable machine-readable codes.

## Common response shapes
Success: data object plus request metadata.  
Error: stable code, safe message, field errors, request ID and non-sensitive details.

Suggested status codes: 400 malformed request, 401 unauthenticated, 403 forbidden, 404 unavailable/not found, 409 state/version conflict, 422 domain validation, 429 optional AI rate limit, 503 optional AI unavailable.

## Identity and workspace
| Method | Path | Purpose |
|---|---|---|
| POST | /auth/register | Create email/password account, if auth is in demo |
| POST | /auth/login | Start server-managed session |
| POST | /auth/logout | End session |
| GET | /me | Current user and workspace memberships |
| GET/POST | /workspaces | List/create workspaces |
| GET | /workspaces/{workspace_id} | Read workspace |
| GET | /workspaces/{workspace_id}/members | List members and roles |

Email verification/password reset may be deferred because no paid email provider is allowed. Do not implement Google OAuth/Sign-In.

## Projects and requirements
| Method | Path | Purpose |
|---|---|---|
| GET/POST | /workspaces/{workspace_id}/projects | List/create projects |
| GET/PATCH | /projects/{project_id} | Read/update project metadata |
| GET/POST | /projects/{project_id}/requirements | List/create requirements |
| GET/PATCH | /requirements/{requirement_id} | Read/update requirement |
| POST | /requirements/{requirement_id}/clarifications | Add contextual clarification |
| POST | /requirements/{requirement_id}/approve | Approve requirement into scope, if authorized |

## Tasks and delivery
| Method | Path | Purpose |
|---|---|---|
| GET/POST | /projects/{project_id}/tasks | List/create tasks |
| GET/PATCH | /tasks/{task_id} | Read/update task |
| PUT | /tasks/{task_id}/dependencies | Replace Finish-to-Start prerequisites |
| POST | /tasks/{task_id}/effort-entries | Record actual effort |
| POST | /tasks/{task_id}/concerns | Report blocker/assistance/extension |
| GET | /projects/{project_id}/schedule | Read schedule projection |
| GET | /projects/{project_id}/capacity | Read workload/capacity view |

## Baselines and change management
| Method | Path | Purpose |
|---|---|---|
| GET | /projects/{project_id}/baselines | List approved versions |
| GET | /baselines/{baseline_id} | Read immutable baseline |
| POST | /projects/{project_id}/change-requests | Create request pinned to current baseline |
| GET | /projects/{project_id}/change-requests | List/filter requests |
| GET/PATCH | /change-requests/{change_id} | Read/update draft request |
| POST | /change-requests/{change_id}/assess | Calculate deterministic impact |
| POST | /change-requests/{change_id}/submit | Freeze and submit revision |
| POST | /change-requests/{change_id}/decisions | Record technical/business decision |
| POST | /change-requests/{change_id}/client-confirmation | Record client confirmation when required |

Decision endpoints identify the exact submitted revision and approval stage. Approval fails if the baseline or revision is stale. A new baseline is created only after all required approvals/confirmations.

## Risks, releases, communication and dashboard
| Method | Path | Purpose |
|---|---|---|
| GET/POST | /projects/{project_id}/risks | List/create risks |
| GET/PATCH | /risks/{risk_id} | Read/update risk |
| GET/POST | /projects/{project_id}/releases | List/create releases |
| PATCH | /releases/{release_id} | Update release lifecycle |
| GET | /projects/{project_id}/dashboard | Role-aware project summary |
| GET/POST | /projects/{project_id}/discussions | Contextual discussion threads |
| POST | /discussions/{discussion_id}/comments | Add comment with visibility policy |
| GET | /me/notifications | List in-app notifications |
| POST | /notifications/{notification_id}/read | Mark notification read |
| GET | /projects/{project_id}/audit-events | Authorized activity history |

## Optional AI
POST /impact-assessments/{assessment_id}/explanation generates an explanation from an existing assessment. No general-purpose chat endpoint in V1. If AI is disabled, hide the action or return a clear feature-unavailable response. AI endpoints are read-only with respect to project state.

## Illustrative impact response
An assessment may return assessment ID, baseline version, rule-set version, calculation time, potential additional effort (person-hours), projected completion change (working days), assumptions, affected entities, severity-coded findings and limitations. These are illustrative response fields, not a promise that missing data can be calculated. Never fabricate values.

## Authorization principles
- Owner/Admin manage workspace and business commitments within their authority.
- Team Leader performs technical review and project delivery oversight.
- Members work on authorized tasks, submit requirements/concerns and participate in permitted discussions.
- Viewer is read-only.
- Client access is limited to invited projects and client-visible data.
- Requester cannot approve their own consequential change.
- API enforces permissions independently of frontend controls.

## Contract evolution
Keep schemas small and aligned to implemented journeys. Generate frontend types from reviewed OpenAPI where practical. Changes to lifecycle values, approval stages or calculation semantics require documentation and tests.
