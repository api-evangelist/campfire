---
name: Invoice a customer and collect payment
description: Create an AR invoice in Campfire, retrieve it, mark it paid (full or partial), and void if needed. Journal entries post automatically.
api: openapi/campfire-openapi-original.json
operations: [coa_api_v1_invoice_create, coa_api_v1_invoice_retrieve, coa_api_v1_invoice_pay_create, coa_api_v1_invoice_void_create]
---

# Invoice a customer and collect (Accounts Receivable)

Base URL: `https://api.meetcampfire.com`. Authenticate with
`Authorization: Token <API_KEY>` (`admin`/`clerk` role to post). Send an
`Idempotency-Key` header on create calls.

1. **Create the invoice** — `POST /coa/api/v1/invoice/`
   (`coa_api_v1_invoice_create`) with customer, line items, and dates. The AR
   journal entry is generated automatically. For high volume, use
   `bulk_create_invoices` (`POST /coa/api/v1/invoice/bulk-create`).
2. **Retrieve it** — `GET /coa/api/v1/invoice/{id}/`
   (`coa_api_v1_invoice_retrieve`) to confirm status and totals.
3. **Mark as paid** — `POST /coa/api/v1/invoice/{invoice_id}/pay/`
   (`coa_api_v1_invoice_pay_create`); partial payments allowed. Use
   `coa_api_v1_invoice_calculate_payment_create` to preview payment math.
4. **Void if necessary** — `POST /coa/api/v1/invoice/{invoice_id}/void/`
   (`coa_api_v1_invoice_void_create`); reopen with
   `coa_api_v1_invoice_reopen_create`.

Errors: `400`/`404`/`409` per `errors/campfire-problem-types.yml`.
