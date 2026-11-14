# API Contract

## Status and conventions

This is a **Proposed** resource contract, not a frozen OpenAPI specification. Final routes depend on the approved product, identity, and data model. FastAPI's generated OpenAPI document should become the machine-readable source of truth once implementation begins.

- Base path: `/api/v1` (proposed).
- JSON uses `snake_case`; timestamps are RFC 3339 UTC; identifiers are opaque UUID strings.
- Authoritative decimal values are serialized as strings with an explicit unit to avoid client precision loss.
- Commands use trusted authenticated actor context, never a client-provided actor.
- Mutation requests that can be retried should support `Idempotency-Key`; exact persistence/window rules are unresolved.
- Mutable resources expose a `version`; writes provide `If-Match` or an `expected_version` (choose one before implementation).
- Pagination is cursor-based where lists can grow; exact envelope is proposed below.

## Common shapes

```json
{
  "data": {},
  "meta": { "request_id": "opaque-id" }
}
```

```json
{
  "error": {
    "code": "stale_baseline",
    "message": "The change request no longer targets the current baseline.",
    "field_errors": [],
    "request_id": "opaque-id",
    "details": {}
  }
}
```

Error codes are stable machine-readable values. `details` must not leak internals. Proposed status usage: `400` malformed request, `401` unauthenticated, `403` forbidden, `404` hidden/not found, `409` state/version conflict, `422` domain validation, `429` explanation rate limit, `503` optional AI unavailable.

## Proposed resources and endpoints

### Projects and initial scope

| Method | Path | Purpose |
|---|---|---|
| `POST` | `/projects` | Create project |
| `GET` | `/projects` | List accessible projects |
| `GET` | `/projects/{project_id}` | Read project summary |
| `PATCH` | `/projects/{project_id}` | Update mutable project metadata |
| `GET` | `/projects/{project_id}/scope-draft` | Read initial draft and current calculation |
| `PUT` | `/projects/{project_id}/scope-draft/items/{item_id}` | Create/replace one draft item |
| `DELETE` | `/projects/{project_id}/scope-draft/items/{item_id}` | Remove one draft item |
| `POST` | `/projects/{project_id}/scope-draft/calculate` | Validate/recalculate; read-only domain effect |
| `POST` | `/projects/{project_id}/scope-draft/submit` | Submit an exact draft version |

The create-versus-replace semantics for client-generated item IDs and reordering need resolution. Bulk editing may replace item-level endpoints if the UI transaction model favors it.

### Baselines

| Method | Path | Purpose |
|---|---|---|
| `GET` | `/projects/{project_id}/baselines` | List baseline versions |
| `GET` | `/projects/{project_id}/baselines/{baseline_id}` | Read immutable snapshot and calculation |
| `POST` | `/projects/{project_id}/baseline-submissions/{submission_id}/decisions` | Approve/reject initial baseline candidate |

### Change requests

| Method | Path | Purpose |
|---|---|---|
| `POST` | `/projects/{project_id}/change-requests` | Create against an exact baseline |
| `GET` | `/projects/{project_id}/change-requests` | List/filter requests |
| `GET` | `/projects/{project_id}/change-requests/{change_id}` | Read request, current revision, diff, findings |
| `PATCH` | `/projects/{project_id}/change-requests/{change_id}` | Update draft metadata/proposal |
| `POST` | `/projects/{project_id}/change-requests/{change_id}/calculate` | Validate/recalculate current draft revision |
| `POST` | `/projects/{project_id}/change-requests/{change_id}/submit` | Freeze and submit exact revision |
| `POST` | `/projects/{project_id}/change-requests/{change_id}/decisions` | Approve/reject exact submitted revision |

### Explanations, findings, and audit

| Method | Path | Purpose |
|---|---|---|
| `POST` | `/calculation-runs/{run_id}/explanations` | Generate/read optional grounded explanation |
| `GET` | `/calculation-runs/{run_id}` | Read calculation metadata and findings |
| `GET` | `/projects/{project_id}/audit-events` | List authorized business history |

AI endpoints are omitted entirely or return a clear feature-unavailable response when AI is not configured. They never accept arbitrary prompts in V1.0.

## Command examples

### Decide a submitted change

```http
POST /api/v1/projects/{project_id}/change-requests/{change_id}/decisions
Idempotency-Key: 21c4...client-generated...
Content-Type: application/json
```

```json
{
  "revision": 3,
  "base_baseline_id": "uuid",
  "decision": "approved",
  "rationale": "Reviewed impact with delivery lead."
}
```

The response returns the decision and, when approved, the newly created baseline. If revision 3 is not submitted, is already decided, or its baseline is stale, return `409` with a specific error code.

### Structured calculation result

```json
{
  "calculation_run_id": "uuid",
  "rule_set_version": "unresolved",
  "input_fingerprint": "algorithm:value",
  "summary": {
    "baseline_total": { "value": "0.00", "unit": "UNRESOLVED" },
    "proposed_total": { "value": "0.00", "unit": "UNRESOLVED" },
    "delta": { "value": "0.00", "unit": "UNRESOLVED" }
  },
  "findings": [
    {
      "id": "finding-id",
      "code": "example_only_not_approved",
      "severity": "info",
      "parameters": {},
      "affected_refs": []
    }
  ]
}
```

Placeholder values deliberately do not imply an approved estimate unit or formula.

## Authorization matrix — Unresolved

An endpoint-level matrix cannot be finalized until roles and tenancy are approved. Proposed baseline: viewers read; editors mutate drafts and submit; approvers decide; project metadata changes require owner/admin. Every resource lookup is scoped through project access to prevent cross-project ID enumeration.

## Contract evolution — Proposed

- Additive compatible fields may ship within `/v1`; clients ignore unknown fields.
- Removing/renaming fields or changing semantics requires a versioned migration plan.
- Error codes and state values are contract elements.
- Generate TypeScript API types/client from reviewed OpenAPI rather than maintaining duplicate handwritten DTOs.

