---
name: Manage Dash0 dashboards as code
description: List, create, and idempotently upsert Dash0 dashboards via the API for Observability-as-Code workflows.
api: openapi/dash0-openapi.json
operations: [get_api-dashboards, post_api-dashboards, put_api-dashboards-originorid, delete_api-dashboards-originorid, post_api-import-dashboard]
---

# Manage Dash0 dashboards as code

## Auth
Send `Authorization: Bearer <DASH0_AUTH_TOKEN>`. Pick the API host for your
region (e.g. `https://api.eu-west-1.aws.dash0.com`). Add `?dataset=<name>` to
scope to a dataset (defaults to the org default).

## Steps
1. **List** existing dashboards with `get_api-dashboards` to see current origins/ids.
2. **Upsert** a dashboard with `put_api-dashboards-originorid`, using a stable
   caller-owned `originOrId` (your `dash0.com/origin` label). This is idempotent:
   re-applying the same definition updates in place, so it is safe to run from CI.
   Use `post_api-dashboards` only when you want the server to generate the id.
3. **Delete** with `delete_api-dashboards-originorid` when retiring a dashboard.
4. For one-time migrations of externally-authored dashboards, use
   `post_api-import-dashboard` (keeps the asset fully UI-editable). Do NOT use
   import in ongoing IaC loops — it causes drift.

## Rules
- Prefer origin-keyed `PUT` upserts for reproducible, drift-free config.
- Errors use `{ "error": { "code", "message", "traceId" } }`; a 413 means the
  body exceeded 256KB.
