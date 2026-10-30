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

Lev is an AI platform and product system for commercial real estate (CRE) teams, used by sponsors, financing brokers, investment-sales brokers, lenders, capital-markets teams, and enterprise operators. The platform is organized in four layers: CRE apps (CRM, pipeline, vault/data rooms, checklists, memos, commissions), source-backed AI agents (Lev Agent, Lev Memo, Lender Search, Lev Match, Lev Index), CRE data (lender, market, contact, property, and recent-terms data), and a developer platform. That platform layer is the API Evangelist interest: a versioned REST API at api.lev.com covering deals, documents and vaults, checklists, contacts, companies, the lender directory, term sheets, placements, pipelines, market data, account, and billing; a hosted remote MCP server at mcp.lev.com with roughly 60 tools and OAuth 2.1 discovery; and a first-party Python CLI. The API publishes an OpenAPI 3.1 description, scoped API keys, cursor pagination, Idempotency-Key support on writes, request-id correlation, and a documented error-type and rate-limit contract.

**Areas:** Company · Commercial Real Estate · Real Estate · PropTech · CRE Financing · Lending · CRM · Artificial Intelligence · AI Agents · Deal Management · Market Data · Documents

## Lev on APIs.io

Everything profiled for Lev is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/lev/](https://apis.io/providers/lev/)** — or go straight to one of the APIs or properties below.

### APIs (16)

- [Lev Account & Team API](https://apis.io/apis/lev/lev-account-team-api/) — The Account & Team API from Lev — 4 operation(s) for account & team.
- [Lev API Keys API](https://apis.io/apis/lev/lev-api-keys-api/) — The API Keys API from Lev — 2 operation(s) for api keys.
- [Lev Billing API](https://apis.io/apis/lev/lev-billing-api/) — The Billing API from Lev — 2 operation(s) for billing.
- [Lev Companies API](https://apis.io/apis/lev/lev-companies-api/) — The Companies API from Lev — 4 operation(s) for companies.
- [Lev Contacts API](https://apis.io/apis/lev/lev-contacts-api/) — The Contacts API from Lev — 5 operation(s) for contacts.
- [Lev Deal Financials API](https://apis.io/apis/lev/lev-deal-financials-api/) — The Deal Financials API from Lev — 1 operation(s) for deal financials.
- [Lev Deal Properties API](https://apis.io/apis/lev/lev-deal-properties-api/) — The Deal Properties API from Lev — 1 operation(s) for deal properties.
- [Lev Deal Team API](https://apis.io/apis/lev/lev-deal-team-api/) — The Deal Team API from Lev — 1 operation(s) for deal team.
- [Lev Deals API](https://apis.io/apis/lev/lev-deals-api/) — The Deals API from Lev — 21 operation(s) for deals.
- [Lev Lender Directory API](https://apis.io/apis/lev/lev-lender-directory-api/) — The Lender Directory API from Lev — 3 operation(s) for lender directory.
- [Lev API Documentation API](https://apis.io/apis/lev/lev-lev-api-documentation-api/) — The Lev API Documentation API from Lev — 1 operation(s) for lev api documentation.
- [Lev Market Data API](https://apis.io/apis/lev/lev-market-data-api/) — The Market Data API from Lev — 2 operation(s) for market data.
- [Lev Pipelines API](https://apis.io/apis/lev/lev-pipelines-api/) — The Pipelines API from Lev — 3 operation(s) for pipelines.
- [Lev Placements API](https://apis.io/apis/lev/lev-placements-api/) — The Placements API from Lev — 4 operation(s) for placements.
- [Lev Quickstart API](https://apis.io/apis/lev/lev-quickstart-api/) — The Quickstart API from Lev — 1 operation(s) for quickstart.
- [Lev Term Sheets API](https://apis.io/apis/lev/lev-term-sheets-api/) — The Term Sheets API from Lev — 2 operation(s) for term sheets.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [Lev](https://apis.io/servers/lev/lev/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Lev Agentic Access](https://apis.io/agentic-access/lev/lev-agentic-access/)

#### Collections (32)

Postman and Open Collection request collections.

- [Lev Account & Team API](https://apis.io/collections/lev/open-lev-account-team-api/)
- [Lev Account & Team API Keys API](https://apis.io/collections/lev/open-lev-api-keys-api/)
- [Lev Account & Team Billing API](https://apis.io/collections/lev/open-lev-billing-api/)
- [Lev Account & Team Companies API](https://apis.io/collections/lev/open-lev-companies-api/)
- [Lev Account & Team Contacts API](https://apis.io/collections/lev/open-lev-contacts-api/)
- [Lev Account & Team Deal Financials API](https://apis.io/collections/lev/open-lev-deal-financials-api/)
- [Lev Account & Team Deal Properties API](https://apis.io/collections/lev/open-lev-deal-properties-api/)
- [Lev Account & Team Deal Team API](https://apis.io/collections/lev/open-lev-deal-team-api/)
- [Lev Account & Team Deals API](https://apis.io/collections/lev/open-lev-deals-api/)
- [Lev Account & Team Lender Directory API](https://apis.io/collections/lev/open-lev-lender-directory-api/)
- [Lev Account & Team Lev API Documentation API](https://apis.io/collections/lev/open-lev-lev-api-documentation-api/)
- [Lev Account & Team Market Data API](https://apis.io/collections/lev/open-lev-market-data-api/)
- [Lev Account & Team Pipelines API](https://apis.io/collections/lev/open-lev-pipelines-api/)
- [Lev Account & Team Placements API](https://apis.io/collections/lev/open-lev-placements-api/)
- [Lev Account & Team Quickstart API](https://apis.io/collections/lev/open-lev-quickstart-api/)
- [Lev Account & Team Term Sheets API](https://apis.io/collections/lev/open-lev-term-sheets-api/)
- [Lev Account & Team API](https://apis.io/collections/lev/postman-lev-account-team-api/)
- [Lev Account & Team API Keys API](https://apis.io/collections/lev/postman-lev-api-keys-api/)
- [Lev Account & Team Billing API](https://apis.io/collections/lev/postman-lev-billing-api/)
- [Lev Account & Team Companies API](https://apis.io/collections/lev/postman-lev-companies-api/)
- [Lev Account & Team Contacts API](https://apis.io/collections/lev/postman-lev-contacts-api/)
- [Lev Account & Team Deal Financials API](https://apis.io/collections/lev/postman-lev-deal-financials-api/)
- [Lev Account & Team Deal Properties API](https://apis.io/collections/lev/postman-lev-deal-properties-api/)
- [Lev Account & Team Deal Team API](https://apis.io/collections/lev/postman-lev-deal-team-api/)
- [Lev Account & Team Deals API](https://apis.io/collections/lev/postman-lev-deals-api/)
- …and 7 more published on APIs.io

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Lev Api Overlay](https://apis.io/overlays/lev/lev-api-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Lev Authentication](https://apis.io/security/lev/lev-authentication/)
- [Lev Domain Security](https://apis.io/security/lev/lev-domain-security/)
- [Lev Trust Center](https://apis.io/security/lev/lev-trust-center/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Lev Scopes](https://apis.io/scopes/lev/lev-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Lev Plans](https://apis.io/plans/lev/lev-plans/)

#### Rate limits (1)

Published request limits.

- [Lev Rate Limits](https://apis.io/rate-limits/lev/lev-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.lev.com/)
- [Documentation](https://www.lev.com/docs)
- [Getting started](https://www.lev.com/docs/build/getting-started)
- [API reference](https://www.lev.com/docs/build/api-overview)
- [Pricing](https://www.lev.com/pricing)
- [Sign up](https://www.lev.com/auth/login?screen_hint=signup)
- [Support](https://www.lev.com/docs/learn)
- [Changelog](https://www.lev.com/docs/changelog)
- [Blog](https://www.lev.com/blog)
- [Security](https://www.lev.com/docs/learn/security)
- [Compliance](https://www.lev.com/docs/learn/trust)
- [Terms of service](https://www.lev.com/docs/learn/terms)
- [Privacy policy](https://www.lev.com/docs/learn/privacy-policy)
- [Status](https://lev.statuspage.io/)

## API Evangelist rating

**Kin Score 63.0** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 50.8 |
| Contract governance | 4.5 |
| Operational transparency | 73.7 |
| Developer ergonomics | 67.3 |
| Access clarity | 85.5 |

**Agent readiness 55.3** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | verified |
| Auth Clarity | served (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | verified |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | distinct |

**Regulatory alignment 39.7** — Securities & Market Data

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/lev/](https://apis.io/providers/lev/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Lev: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/lev/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
