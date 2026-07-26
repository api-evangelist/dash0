---
name: Create Dash0 alerting check rules
description: Define Prometheus alert (check) rules and wire them to notification channels in Dash0.
api: openapi/dash0-openapi.json
operations: [get_api-alerting-check-rules, post_api-alerting-check-rules, put_api-alerting-check-rules-originorid, post_api-alerting-check-rules-bulk, get_api-notification-channels, post_api-notification-channels]
---

# Create Dash0 alerting check rules

## Auth
`Authorization: Bearer <DASH0_AUTH_TOKEN>`, regional API host, optional
`?dataset=<name>`.

## Steps
1. **Ensure a notification channel** exists: `get_api-notification-channels`, and
   create one with `post_api-notification-channels` (webhook/Slack/email) if needed.
2. **Create or upsert a check rule** with a PromQL expression:
   - Single rule, idempotent: `put_api-alerting-check-rules-originorid` with your
     own origin/id.
   - New-only: `post_api-alerting-check-rules`.
   - Up to 1000 rules atomically: `post_api-alerting-check-rules-bulk` (create-only,
     NOT idempotent — a verbatim retry 400s on origin collision; body limit 2MB).
3. **Verify** with `get_api-alerting-check-rules`.

## Rules
- PromQL, intervals, summary length and template functions are validated; a 400
  rejects the whole (bulk) batch with per-item diagnostics and writes nothing.
- Keep origins stable and unique per dataset.
