---
name: Sync Lev deals into an external system
description: Bulk-read deals and their sub-resources out of Lev correctly — cursor pagination, incremental filters, field selection, and rate-limit backoff.
api: openapi/lev-openapi-original.json
generated: '2026-07-19'
method: generated
source: openapi/lev-openapi-original.json + https://www.lev.com/docs/build/data-sync-patterns
operations:
  - getMe
  - postAuthValidateApiKey
  - getDeals
  - getDealsDealId
  - getDealsDealIdFinancials
  - getDealsDealIdProperties
  - getDealsDealIdTeam
  - getContacts
  - getCompanies
  - getPlacements
  - getHealth
---

# Sync Lev deals into an external system

Use this for headless, server-to-server extraction of Lev data into a warehouse,
CRM, or reporting system. Use the REST API with a `lev_sk_` API key for this — the
MCP server is per-user and built for live sessions, not batch automation.

## Before you start

- Requires `deals:read` (plus `contacts:read` / `companies:read` for those
  resources). Validate the key and read its scopes with `postAuthValidateApiKey`
  before a long run.
- Call `getMe` and read `platform.api_tier` and `platform.rate_limits` to learn your
  actual budget. Do not assume a tier.

## Steps

1. **Check liveness.** `getHealth` is unauthenticated and capped at 100 req/min.
   Use it as a preflight, not as a heartbeat inside the loop.
2. **Establish the budget.** From `getMe`: free is 30 req/min account-wide and 10
   per-endpoint; standard is 100/20; enterprise is 500/60. Pace the sync to the
   *per-endpoint* number, which is the binding constraint on a single-resource
   crawl.
3. **Page with cursors.** Call `getDeals` with `limit=200` (the maximum) and no
   `sort`. Pass the returned `next_cursor` back as `cursor` and repeat while
   `has_more` is true. Cursor paging is stable — no duplicates, no skips.
4. **Do not sort during a bulk sync.** Supplying `sort` switches the endpoint to
   offset pagination, which can skip or duplicate rows when records are inserted or
   deleted mid-crawl. Sort after extraction, on your side.
5. **Go incremental.** On subsequent runs filter with
   `filter[created_at][gte]` / `filter[created_at][lte]` rather than re-walking the
   whole collection.
6. **Cut the payload.** Use `fields` to request only the columns you persist (`id`
   is always returned), and `include=financials,properties,team` to pull
   sub-resources inline instead of issuing three extra calls per deal. Choosing
   `include` over per-deal calls is the single biggest rate-limit saving in a sync.
7. **Only fall back to per-deal calls** — `getDealsDealIdFinancials`,
   `getDealsDealIdProperties`, `getDealsDealIdTeam` — for records where the inline
   include is insufficient.
8. **Handle 429 properly.** On `error.type == "rate_limit_exceeded"`, sleep
   `error.retry_after_seconds`, then resume with exponential backoff. Do not retry
   immediately and do not parallelize your way around the limit.

## Rules

- **Cursor and `sort` are mutually exclusive.** Pick cursor for correctness.
- **Cache static data.** Market base rates and asset types change rarely; caching
  them keeps request budget for the deal crawl.
- Persist the `cursor` between runs so an interrupted sync resumes rather than
  restarting.
- Log the `request_id` from every failed response — it is what support needs.
- Deals are soft-deleted (archived), not removed. Reconcile on the archived state
  rather than treating a disappearing record as a hard delete; `filter[archived]`
  controls whether archived deals are returned.
- `503 service_unavailable` is transient. Retry with backoff and check
  https://lev.statuspage.io/ before escalating.

## Related

- `rate-limits/lev-rate-limits.yml` — exact tier limits
- `conventions/lev-conventions.yml` — pagination, filtering, field selection
- `errors/lev-problem-types.yml`
