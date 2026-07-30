---
name: Answer deal questions with source-backed facts
description: Search Lev's canonical indexed deal facts, trace each value back to the source document, and correct or record values without losing provenance.
api: openapi/lev-openapi-original.json
generated: '2026-07-19'
method: generated
source: openapi/lev-openapi-original.json + https://www.lev.com/docs/build/deals
operations:
  - getDeals
  - getDealsDealId
  - postDealsDealIdIndexSearch
  - postDealsDealIdIndexObservations
  - getDealsDealIdIndexMetricDefinitions
  - getDealsDealIdIndexEntities
  - postDealsDealIdIndexFacts
  - patchDealsDealIdIndexFacts
  - getDealsDealIdDocuments
  - getDealsDealIdDocumentsDocumentIdDownload
---

# Answer deal questions with source-backed facts

Use this when the user asks an underwriting question about a specific deal — NOI,
occupancy, valuation, rent roll figures, term details — and expects the answer to
cite where the number came from.

This is the skill that makes Lev answers defensible. Do not answer a quantitative
question about a deal from memory, from the deal record's headline fields, or from
your own reading of a document. Resolve it through the Index.

## Before you start

- Requires `deals:read`; writing facts requires `deals:write`.
- Send `Authorization: Bearer <token>` and `X-Origin-App: <your-app-name>`.

## Steps

1. **Resolve the deal first.** If you only have a name, call `getDeals` with
   `search` or `filter[title]` and confirm the match with the user. Never run an
   index search against a guessed deal id.
2. **Search the index.** Call `postDealsDealIdIndexSearch` with the user's question
   as `context`. This is a natural-language search over canonical facts, not a
   keyword lookup — pass the question close to how the user asked it. Optional:
   `min_score`, `limit`, `include_signed_urls`.
3. **Cite the source.** Each result carries a source pointing at the document the
   value came from. Report the value *and* the document. If the user needs the
   document itself, call `getDealsDealIdDocuments` to locate it and
   `getDealsDealIdDocumentsDocumentIdDownload` for a short-lived signed link.
4. **Show the alternatives when a number is contested.** Call
   `postDealsDealIdIndexObservations` with the `sot_id` from the search result
   (preferred) or a `metric_id`. This returns every value extracted from every
   document for that fact. Use it when the user asks "where did that come from" or
   when two documents disagree.
5. **Correct a canonical value.** Call `patchDealsDealIdIndexFacts` with `deal_id`,
   `sot_id`, and **exactly one** of:
   - `observation_id` — promotes an already-extracted value. **Prefer this.** It
     preserves source provenance.
   - `value` — a free-text replacement. This breaks the chain back to a document;
     only use it when no observation holds the correct value.
   Some metrics are not editable server-side and will return a clear error.
6. **Record a new value.** Call `postDealsDealIdIndexFacts` with `deal_id` and
   `values` (each a `metric_id` plus `value`, optionally an `entity_ref`).
   Discover what is recordable with `getDealsDealIdIndexMetricDefinitions` and
   valid entities with `getDealsDealIdIndexEntities` first — do not invent a
   `metric_id`.

## Rules

- **Record versus update.** `postDealsDealIdIndexFacts` *appends* a user-input
  observation when a canonical value already exists; Lev's promotion logic then
  decides what displays. To correct one specific displayed value, use
  `patchDealsDealIdIndexFacts` instead. Choosing wrong leaves the wrong number on
  screen.
- **Provenance is the product.** Always surface the source document alongside a
  number. An uncited figure from this API is a bug in your answer, not a shortcut.
- Send `Idempotency-Key: <uuid>` on both fact-write operations.
- Signed download links are short-lived. Fetch them at the moment of use; do not
  cache or store them.
- Check whether the deal is archived before presenting it as live.

## Related

- `data-model/lev-data-model.yml` — the fact → observation → document provenance edge
- `conventions/lev-conventions.yml` — envelope and idempotency
- `errors/lev-problem-types.yml`
