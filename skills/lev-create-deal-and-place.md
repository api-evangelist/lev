---
name: Create a Lev deal and place it with a lender
description: Create a commercial real estate deal in Lev, move it into a pipeline stage, place it with a capital source, and record the resulting term sheet.
api: openapi/lev-openapi-original.json
generated: '2026-07-19'
method: generated
source: openapi/lev-openapi-original.json + https://www.lev.com/docs/build/deals
operations:
  - postDeals
  - getDealsDealId
  - getPipelines
  - getPipelinesPipelineId
  - postDealsDealIdPipeline
  - postPlacements
  - getPlacementsPlacementId
  - postDealsDealIdTermSheets
  - getDealsDealIdTermSheets
---

# Create a Lev deal and place it with a lender

Use this when the user wants to originate a new CRE financing deal in Lev and carry
it through to a recorded term sheet.

## Before you start

- Base URL is `https://api.lev.com/api/external/v2`.
- Send `Authorization: Bearer <token>` and `X-Origin-App: <your-app-name>` on every
  request. Both are required.
- You need an API key with the `deals:write` scope. Confirm scopes with
  `postAuthValidateApiKey` or `getMe` before starting — a `read_only` key will fail
  every write in this skill with `403 forbidden`.
- Every write below is a state mutation. Confirm with the user before executing.

## Steps

1. **Create the deal.** Call `postDeals`. `title` is the only required field.
   Optional: `loan_amount`, `loan_type`, `transaction_type`, `business_plan`,
   `description`, `estimated_close_date`. Send an `Idempotency-Key: <uuid>` header
   so a retry does not create a duplicate deal. Keep the returned `id`.
2. **Confirm what was created.** Call `getDealsDealId`. Use `include=financials,properties,team`
   to pull sub-resources in one round trip instead of separate calls.
3. **Find the target pipeline.** Call `getPipelines` to list pipelines on the
   account, then `getPipelinesPipelineId` to read its statuses. You need both the
   pipeline id and the status id as integers — do not guess them.
4. **Move the deal into a stage.** Call `postDealsDealIdPipeline` with the pipeline
   and status ids. Moving a deal into a launching status (Outreach, Negotiating,
   Closing, Closed) on a financing pipeline automatically sets the deal's launch
   date if it is not already set. Say this to the user before you do it.
5. **Create the placement.** Call `postPlacements` against the deal to record the
   capital source you are placing with. A placement can reference a company via
   `private_company_id` and a contact via `contact_id`. Verify the placement with
   `getPlacementsPlacementId`.
6. **Record the term sheet.** Call `postDealsDealIdTermSheets`. A term sheet is
   created against a placement, so pass the `placement_id` from step 5 — a term
   sheet with no placement has no counterparty. List with `getDealsDealIdTermSheets`
   to confirm.

## Rules

- **Idempotency.** Every write operation accepts `Idempotency-Key: <uuid>`. Always
  send one. Replaying the same key with a *different* body returns `409 conflict`;
  reuse the identical body on retry, or mint a new key for a genuinely new request.
- **Enums are lowercase on the wire.** `loan_type`, `transaction_type`, and
  `business_plan` values must be lowercase (`permanent`, `bridge`, `construction`,
  `stabilized`, `value_add`). A wrong-case or unknown enum returns
  `422 validation_error`, not `400`.
- **Errors.** Read `error.type`, not just the status: `bad_request` (malformed),
  `validation_error` (semantically wrong value), `forbidden` (scope or tier),
  `not_found` (wrong id or no access), `402 payment_required` (needs credits or a
  plan upgrade — the body carries `upgrade_url`).
- **Always keep `request_id`** from the response envelope. It is the only handle
  support can trace.
- **Deleting a deal archives it.** `deleteDealsDealId` is a soft delete, not a
  removal. Note deletes, by contrast, are permanent.

## Related

- `conventions/lev-conventions.yml` — envelope, pagination, idempotency
- `errors/lev-problem-types.yml` — full error type reference
- `data-model/lev-data-model.yml` — how deals, placements, and term sheets relate
