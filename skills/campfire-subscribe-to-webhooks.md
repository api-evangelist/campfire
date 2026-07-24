---
name: Subscribe to webhooks
description: Register a Campfire webhook against topics, list subscriptions, inspect the delivery log, and delete a webhook.
api: openapi/campfire-openapi-original.json
operations: [integrations_api_v1_webhook_create, integrations_api_v1_webhook_list, integrations_api_v1_webhook_events_list, integrations_api_v1_webhook_destroy]
---

# Subscribe to webhooks

Base URL: `https://api.meetcampfire.com`, auth `Authorization: Token <API_KEY>`.
Campfire POSTs events to your URL and records each delivery attempt.

1. **Create a subscription** — `POST /integrations/api/v1/webhook`
   (`integrations_api_v1_webhook_create`) with `url`, `topics[]`, and
   `active: true`. Campfire returns a `token` used to sign/verify deliveries and
   a `uuid`.
2. **List subscriptions** — `GET /integrations/api/v1/webhook`
   (`integrations_api_v1_webhook_list`).
3. **Inspect deliveries** — `GET /integrations/api/v1/webhook/{id}/events`
   (`integrations_api_v1_webhook_events_list`) returns WebhookEvent records
   (topic, status, http result, timestamp) for debugging retries.
4. **Update or remove** — `PATCH /integrations/api/v1/webhook/{id}`
   (`integrations_api_v1_webhook_partial_update`) to toggle `active`/topics;
   `DELETE /integrations/api/v1/webhook/{id}`
   (`integrations_api_v1_webhook_destroy`) to remove.

Available topics are returned dynamically as WebhookTopic objects. See
`asyncapi/campfire-webhooks.yml`.
