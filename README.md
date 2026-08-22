# Lev

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
