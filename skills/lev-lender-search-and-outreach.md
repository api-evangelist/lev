---
name: Find lenders for a deal and prepare outreach
description: Browse the Lev lender directory, inspect lending programs, and build a CRM contact list for outreach — including the credit-charging AI contact unlock.
api: openapi/lev-openapi-original.json
generated: '2026-07-19'
method: generated
source: openapi/lev-openapi-original.json + https://www.lev.com/docs/build/lender-directory
operations:
  - getDealsDealId
  - getDealsDealIdFinancials
  - getLendersDirectory
  - getLendersOrgId
  - getLendersOrgIdPrograms
  - getContacts
  - getContactsContactId
  - postContactsContactIdActionsUnlock
  - postContacts
  - postCompanies
  - postDealsDealIdNotes
  - getBillingCreditsBalance
---

# Find lenders for a deal and prepare outreach

Use this when the user wants to identify capital sources for a deal and assemble
the contacts to approach.

## Before you start

- Requires `lenders:read` and `contacts:read`. Creating CRM records requires
  `contacts:write` / `companies:write`. **The contact unlock additionally requires
  the `ai:actions` scope and consumes credits.**
- Send `Authorization: Bearer <token>` and `X-Origin-App: <your-app-name>`.

## Steps

1. **Load the deal's shape.** Call `getDealsDealId` and `getDealsDealIdFinancials`.
   You need loan amount, loan type, transaction type, business plan, and asset type
   before you can judge lender fit. Do not filter the directory on assumptions.
2. **Browse the directory.** Call `getLendersDirectory`. Page with `limit` (default
   50, max 200) and `cursor`. Narrow with the documented `filter[...]` parameters
   rather than fetching everything and filtering client-side.
3. **Inspect a candidate.** Call `getLendersOrgId` for the lender's detail, then
   `getLendersOrgIdPrograms` for its lending programs. Match the deal against
   program terms — this is where fit is actually decided, not at the directory
   level.
4. **Find existing contacts first.** Call `getContacts` with `search` or
   `filter[...]` scoped to the lender before unlocking anything. The account may
   already have the relationship, in which case an unlock spends credits for
   nothing.
5. **Unlock an AI-recommended contact only with consent.** `postContactsContactIdActionsUnlock`
   reveals an AI-recommended lender contact and **charges credits**. Before calling
   it: check the balance with `getBillingCreditsBalance`, tell the user the action
   costs credits, and get explicit approval. Never unlock speculatively or in a
   loop over candidates.
6. **Record the outcome.** Create any missing CRM records with `postCompanies` and
   `postContacts`, and log the outreach plan on the deal with `postDealsDealIdNotes`
   so the pipeline reflects the work.

## Rules

- **Credit-consuming actions need explicit human approval, every time.** The unlock
  is gated behind its own `ai:actions` scope precisely because it is not an ordinary
  read. A `402 payment_required` response means insufficient credits or plan — the
  body carries `upgrade_url`; surface it rather than retrying.
- The lender surface is read-only. There is no `lenders:write` scope; you cannot
  edit directory records.
- Enum values are lowercase on the wire.
- Send `Idempotency-Key: <uuid>` on the unlock and on every CRM create — an
  accidental retry of the unlock spends credits twice.
- Page with `cursor`, not `offset`, unless you are sorting. Cursor and `sort` are
  mutually exclusive.

## Related

- `plans/lev-plans.yml` — credit allowances per plan
- `scopes/lev-scopes.yml` — why `ai:actions` is separate
- `data-model/lev-data-model.yml` — org_id links CRM companies to directory lenders
