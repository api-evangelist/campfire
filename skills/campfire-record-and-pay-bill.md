---
name: Record and pay an accounts-payable bill
description: Create an AP bill in Campfire, retrieve it, mark it paid (full or partial), and void if needed. Automatic journal entries are generated on post.
api: openapi/campfire-openapi-original.json
operations: [coa_api_v1_bill_create, coa_api_v1_bill_retrieve_2, coa_api_v1_bill_pay_create, coa_api_v1_bill_void_create]
---

# Record and pay a bill (Accounts Payable)

Base URL: `https://api.meetcampfire.com`. Authenticate every request with
`Authorization: Token <API_KEY>` (mint the key under Settings > API Keys; the
API user needs the `admin` or `clerk` role to post). Send `Idempotency-Key` on
create calls so retries never double-post.

1. **Create the bill** — `POST /coa/api/v1/bill/` (`coa_api_v1_bill_create`).
   Include the vendor, line items (account, department/tags, amount), and dates.
   Campfire generates the AP journal entry automatically.
2. **Retrieve it** — `GET /coa/api/v1/bill/{id}/` (`coa_api_v1_bill_retrieve_2`)
   to confirm status, totals, and the generated entry.
3. **Mark as paid** — `POST /coa/api/v1/bill/{bill_id}/pay/`
   (`coa_api_v1_bill_pay_create`). Partial payments are allowed; repeat until
   the balance is cleared.
4. **Void if necessary** — `POST /coa/api/v1/bill/{bill_id}/void/`
   (`coa_api_v1_bill_void_create`). Reopen a voided bill with
   `coa_api_v1_bill_reopen_create` if it was voided in error.

Errors: `400` validation (unbalanced/invalid lines), `404` unknown bill, `409`
conflicting state (e.g. already paid/locked). See `errors/campfire-problem-types.yml`.
