---
name: Query Dash0 telemetry
description: Query OTLP spans, logs and traces, run SQL over telemetry, and evaluate PromQL in Dash0.
api: openapi/dash0-openapi.json
operations: [post_api-spans, post_api-logs, post_api-trace-ids, post_api-trace-details, post_api-sql, post_api-prometheus-api-v1-query, post_api-prometheus-api-v1-query-range]
---

# Query Dash0 telemetry

## Auth
`Authorization: Bearer <DASH0_AUTH_TOKEN>`, regional API host, optional
`?dataset=<name>`. Provide a time window (`start`/`end`) on telemetry queries.

## Steps
1. **Find traces fast**: `post_api-trace-ids` returns only the unique trace IDs
   matching your filters (lightweight two-step pattern).
2. **Fetch a full trace**: `post_api-trace-details` returns the OTLP spans and
   log records for a trace ID.
3. **Query spans / logs directly**: `post_api-spans` and `post_api-logs` return
   OTLP records for filters; use `limit`/`offset` to page.
4. **Ad-hoc analytics**: `post_api-sql` executes a SQL query and returns JSON.
5. **Metrics**: `post_api-prometheus-api-v1-query` (instant) or
   `post_api-prometheus-api-v1-query-range` (range) evaluate PromQL.

## Rules
- Prefer `post_api-trace-ids` then `post_api-trace-details` over `post_api-spans`
  when you only need trace IDs — it is significantly cheaper.
- Errors: `{ "error": { "code", "message", "traceId" } }`.
