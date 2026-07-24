---
name: Pull financial statements
description: Generate an income statement, balance sheet, and trial balance from Campfire for a given entity and period.
api: openapi/campfire-openapi-original.json
operations: [ca_api_get_income_statement_retrieve, ca_api_get_balance_sheet_retrieve, ca_api_get_trial_balance_retrieve]
---

# Pull financial statements

Base URL: `https://api.meetcampfire.com`, auth `Authorization: Token <API_KEY>`
(read-only `view only` role is sufficient). These are GET report endpoints;
pass the entity, period, and cadence as query parameters.

1. **Income statement** — `GET /ca/api/get_income_statement`
   (`ca_api_get_income_statement_retrieve`) for a P&L over the period. Comparative
   and cash-basis variants exist (`ca_api_income_statement_comparative_retrieve`,
   `ca_api_cash_basis_retrieve`).
2. **Balance sheet** — `GET /ca/api/get_balance_sheet`
   (`ca_api_get_balance_sheet_retrieve`); comparative via
   `ca_api_balance_sheet_comparative_retrieve`.
3. **Trial balance** — `GET /ca/api/get_trial_balance`
   (`ca_api_get_trial_balance_retrieve`) to verify debits equal credits before
   close.

Reports are scoped to the org tied to the token. For natural-language access,
the same reports are exposed as MCP tools (see `mcp/campfire-mcp.yml`).
