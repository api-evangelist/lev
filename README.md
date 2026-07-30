# Lev

Lev is an AI platform and product system for commercial real estate (CRE) teams —
sponsors, financing brokers, investment-sales brokers, lenders, capital-markets
teams, and enterprise operators. The product is organized in four layers: CRE apps
(CRM, pipeline, vault/data rooms, checklists, memos, commissions), source-backed AI
agents (Lev Agent, Lev Memo, Lender Search, Lev Match, Lev Index), CRE data
(lender, market, contact, property, and recent-terms data), and a developer
platform.

Website: https://www.lev.com/ · Docs: https://www.lev.com/docs

## Developer surface

| Surface | Where |
|---|---|
| REST API | `https://api.lev.com/api/external/v2` — 81 operations, 57 paths |
| OpenAPI 3.1 | https://www.lev.com/docs/openapi.json (version `2026-03`) |
| MCP server | `https://mcp.lev.com/mcp` — hosted, streamable HTTP, 60 tools, OAuth 2.1 |
| CLI | `lev-cli` (Python, early access — not yet on PyPI) |
| llms.txt | https://www.lev.com/llms.txt |
| Status | https://lev.statuspage.io/ |

The API covers deals (and their financials, properties, team, documents, vaults,
checklists, memos, notes, and source-backed indexed facts), contacts, companies,
placements, term sheets, pipelines, the lender directory, market data, account,
API keys, and billing.

## Notable API characteristics

- **Idempotency** — `Idempotency-Key: <uuid>` on 19 write operations, with
  documented `409 conflict` replay semantics.
- **Cursor pagination** by default (`cursor` / `next_cursor` / `has_more`,
  limit max 200); switches to offset paging when `sort` is supplied.
- **Response envelope** — every response carries `request_id` (UUID v4),
  `timestamp`, and `data`.
- **Typed errors** — a proprietary `{request_id, error:{status, type, message,
  details}}` envelope, not RFC 9457 problem+json.
- **Published rate limits** — 30/100/500 requests per minute account-wide by tier,
  with per-endpoint sub-limits, discoverable at runtime via `getMe`.
- **Scoped API keys** — `lev_sk_` prefix, domain-based `read`/`write` scopes plus a
  separate `ai:actions` scope gating credit-consuming AI actions.
- **Provenance as a first-class feature** — indexed deal facts trace back through
  per-document observations to the source document.

## Gaps observed

- No `/.well-known/security.txt` on any host, and no published vulnerability
  disclosure or bug bounty programme.
- No deprecation or sunset policy (RFC 8594); no operation marked deprecated.
- No event, streaming, or webhook surface — and therefore no AsyncAPI.
- No first-party SDK in any public package registry; `lev-cli` is documented but
  unpublished.
- The OpenAPI ships an empty top-level `tags[]` despite 16 tags in use, and models
  its required headers as an `x-lev-headers` vendor array rather than as parameters.
  Both are captured in `overlays/lev-api-overlay.yaml`.

## Artifacts in this repo

`openapi/` · `overlays/` · `mcp/` · `skills/` · `llms/` · `well-known/` ·
`authentication/` · `scopes/` · `conventions/` · `errors/` · `rate-limits/` ·
`plans/` · `lifecycle/` · `changelog/` · `cli/` · `packages/` · `conformance/` ·
`data-model/` · `security/` · `agentic-access/`

Backed by: canaan-partners
