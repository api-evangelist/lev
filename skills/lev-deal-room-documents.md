---
name: Run a Lev deal room and its diligence checklist
description: Navigate a deal's vaults and documents, work the Deal Room checklist, and drive tasks to completion with comments and assignments.
api: openapi/lev-openapi-original.json
generated: '2026-07-19'
method: generated
source: openapi/lev-openapi-original.json + https://www.lev.com/docs/build/deals
operations:
  - getDealsDealId
  - getDealsDealIdVaults
  - getDealsDealIdDocuments
  - getDealsDealIdDocumentsDocumentId
  - getDealsDealIdDocumentsDocumentIdDownload
  - getDealsDealIdChecklists
  - postChecklistTasks
  - patchChecklistTasksTaskId
  - postChecklistTasksTaskIdComplete
  - getChecklistTasksTaskIdNotes
  - postChecklistTasksTaskIdNotes
  - getDealsDealIdMemos
  - getDealsDealIdMemosMemoUuid
---

# Run a Lev deal room and its diligence checklist

Use this when the user is managing document collection on a deal — chasing missing
diligence, checking what a borrower has uploaded, or driving a checklist to close.

## Before you start

- Requires `deals:read`; checklist writes require `deals:write`.
- Send `Authorization: Bearer <token>` and `X-Origin-App: <your-app-name>`.

## Steps

1. **Understand the vault layout.** Call `getDealsDealIdVaults`. A deal has a
   private Resources area plus any shared Deal Rooms. These are different trust
   boundaries — a document in a shared Deal Room is visible to external parties.
   Establish which vault you are working in before you report on or move anything.
2. **List what exists.** Call `getDealsDealIdDocuments` to see uploaded documents
   across all of the deal's vaults. Narrow with `vault_id`, `folder_id`, or
   `extension`. Use `getDealsDealIdDocumentsDocumentId` for one document's metadata.
3. **Fetch a document only when needed.** `getDealsDealIdDocumentsDocumentIdDownload`
   returns a short-lived signed link. Use it at the moment of need; never cache,
   log, or forward the URL.
4. **Read the checklist.** Call `getDealsDealIdChecklists`. There is one checklist
   per shared Deal Room, each with sections, tasks, expected document types, and
   task-linked files. Compare expected document types against step 2 to find the
   real gaps — that comparison is the point of this skill.
5. **Add missing items.** Call `postChecklistTasks` to add a task to a deal's
   checklist.
6. **Update a task.** Call `patchChecklistTasksTaskId` to change fields such as
   assignee or due date. Tasks can nest subtasks.
7. **Complete a task.** Call `postChecklistTasksTaskIdComplete`. Complete only when
   the linked file is actually present — verify against step 2 first rather than
   trusting the request.
8. **Communicate on the task.** `getChecklistTasksTaskIdNotes` and
   `postChecklistTasksTaskIdNotes` read and add comments. Keep chase-ups on the task
   so context stays with the item.
9. **Surface the work product.** `getDealsDealIdMemos` lists generated memos
   (published and draft); `getDealsDealIdMemosMemoUuid` returns one with a signed
   PDF link and an optional `quality` (`original`, `high`, `medium`, `low`). A
   draft that has not rendered has `pdf_ready: false` and no PDF — say so rather
   than returning a broken link.

## Rules

- **Respect the vault boundary.** Do not describe or expose private Resources
  content as though it were in a shared Deal Room, and vice versa.
- **Note deletes are permanent.** `deleteChecklistTasksTaskIdNotesNoteId` does not
  archive. Confirm before deleting any comment.
- Send `Idempotency-Key: <uuid>` on every task create, update, and complete.
- Signed links expire. Re-fetch rather than reusing.
- Page with `cursor` and `limit` (max 200); `sort` switches to offset paging.

## Related

- `data-model/lev-data-model.yml` — vault, document, checklist, and task graph
- `conventions/lev-conventions.yml`
- `errors/lev-problem-types.yml`
