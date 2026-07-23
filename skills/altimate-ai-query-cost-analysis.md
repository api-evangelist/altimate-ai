---
name: Analyze warehouse query cost and lineage
description: Authenticate to the Altimate platform, list observed queries, and drill into a query's cost metrics and SQL lineage to find expensive workloads.
api: openapi/altimate-ai-openapi-original.json
operations:
  - auth_login_auth_login_post
  - get_all_queries_query_v2__get
  - get_query_query_v2_items__query_id__get
  - get_sql_lineage_query_v2_sql_lineage__query_id__get
  - get_hash_metrics_query_v2_query_group_stats__query_hash__get
---

# Analyze warehouse query cost and lineage

Use the Altimate platform API (`https://api.myaltimate.com`) to find and analyze
expensive warehouse queries.

## Auth
- Send `Authorization: Bearer <ALTIMATE_API_KEY>` on every request (scheme `HTTPBearer`).
- Supply your instance/tenant via the `x-tenant` header where accepted.
- Generate the API key in the Altimate dashboard (Settings -> API Key).

## Steps
1. (If you only have credentials) `POST /auth/login` (`auth_login_auth_login_post`) to
   obtain a session token; otherwise use your API key directly.
2. List observed queries with `GET /query/v2/` (`get_all_queries_query_v2__get`); apply
   filters from `GET /query/v2/filters/` to narrow by warehouse/tag/time.
3. Inspect one query with `GET /query/v2/items/{query_id}`
   (`get_query_query_v2_items__query_id__get`).
4. Pull cost/perf metrics for the query group with
   `GET /query/v2/query_group/stats/{query_hash}` (`get_hash_metrics_...`).
5. Trace what the query touches with
   `GET /query/v2/sql_lineage/{query_id}` (`get_sql_lineage_...`).

## Conventions & errors
- Pagination is page/size style on list endpoints.
- Errors use the FastAPI `{"detail": ...}` envelope; `422` returns per-field validation
  errors. See `errors/altimate-ai-problem-types.yml` and `conventions/altimate-ai-conventions.yml`.
- `403` means the operation is not permitted for your role/tenant.
