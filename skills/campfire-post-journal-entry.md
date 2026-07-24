---
name: Post a journal entry
description: List and create standard and intercompany general-ledger journal entries in Campfire, and balance intercompany entries.
api: openapi/campfire-openapi-original.json
operations: [coa_api_journal_entry_list, coa_api_journal_entry_create, coa_api_intercompany_journal_entry_create, coa_api_intercompany_journal_entry_balance_create]
---

# Post a journal entry

Base URL: `https://api.meetcampfire.com`, auth `Authorization: Token <API_KEY>`
(`admin`/`clerk`). Send `Idempotency-Key` on creates. Debits must equal credits.

1. **Review existing entries** — `GET /coa/api/journal_entry`
   (`coa_api_journal_entry_list`). Supports `include_deleted` and
   `last_modified_at` filtering for incremental sync.
2. **Create a standard entry** — `POST /coa/api/journal_entry`
   (`coa_api_journal_entry_create`) with balanced debit/credit lines, each
   referencing a chart account, entity, currency, and optional department/tags.
3. **Intercompany entry** — `POST /coa/api/intercompany-journal-entry`
   (`coa_api_intercompany_journal_entry_create`) to post across legal entities.
4. **Balance intercompany** — `POST /coa/api/intercompany-journal-entry/balance`
   (`coa_api_intercompany_journal_entry_balance_create`) to auto-generate the
   due-to/due-from balancing lines.

Deleting a posted/locked entry returns `409`; unbalanced lines return `400`.
See `errors/campfire-problem-types.yml` and `data-model/campfire-data-model.yml`.
