---
name: Subscribe to vivenu webhooks
description: Register a webhook endpoint and react to vivenu real-time events.
api: openapi/vivenu-openapi-original.json
operations: [webhooks/list, webhooks/create, webhooks/update, webhooks/delete]
---

# Subscribe to vivenu webhooks

Use this skill to receive real-time notifications for transactions, tickets,
checkouts, purchase intents, customers, and more.

## Auth
`Authorization: Bearer <API_KEY>` against `https://vivenu.com/api` (or the
`https://vivenu.dev/api` staging host while testing).

## Steps
1. **List current subscriptions** — `GET /api/webhooks` (`webhooks/list`).
2. **Create a subscription** — `POST /api/webhooks` (`webhooks/create`) with your
   endpoint URL and the event types to receive.
3. **Update / delete** — `PUT /api/webhook/{id}` (`webhooks/update`),
   `DELETE /api/webhook/{id}` (`webhooks/delete`).

## Event types
39 event types are published, grouped by domain: `webhook.transaction.*`,
`webhook.checkout.*`, `webhook.ticket.*`, `webhook.purchaseIntent.*`,
`webhook.customer.*`, `webhook.event.*`, `webhook.job.*`,
`webhook.ticketTransfer.*`, `webhook.bundle.*`, `webhook.product.*`,
`webhook.subscription.*`, and `webhook.scan.created`. Full list in
`asyncapi/vivenu-webhooks.yml`.

## Rules
- Handlers must be idempotent on your side — the same event may be delivered
  more than once.
- Return 2xx quickly; do heavy processing async.
