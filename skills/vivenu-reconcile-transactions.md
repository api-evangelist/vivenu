---
name: Reconcile vivenu transactions and tickets
description: List transactions, inspect a transaction, and pull its tickets for reconciliation.
api: openapi/vivenu-openapi-original.json
operations: [get_all_transactions, get_a_transaction, get_all_transaction_tickets, tickets/list]
---

# Reconcile vivenu transactions and tickets

Use this skill to reconcile sales — walk transactions and their issued tickets.

## Auth
`Authorization: Bearer <API_KEY>`. Base `https://vivenu.com/api`.

## Steps
1. **List transactions** — `GET /api/transactions` (`get_all_transactions`).
   Page with `skip`/`top`; filter by `start`/`end`, `eventId`, `sellerId`,
   `status`, `createdAt`.
2. **Retrieve a transaction** — `GET /api/transactions/{id}`
   (`get_a_transaction`).
3. **Pull the transaction's tickets** — `get_all_transaction_tickets`.
4. **Cross-check tickets directly** — `GET /api/tickets` (`tickets/list`),
   filterable by `eventId`, `transactionId`, `customerId`.

## Rules
- A Ticket `belongs_to` a Transaction via `transactionId`, an Event via
  `eventId`, and a Customer via `customerId` (see
  `data-model/vivenu-data-model.yml`).
- Some analytics/rich transaction endpoints are **deprecated** (e.g.
  `get_all_transactions_rich`, `get_a_transaction` variants) — see
  `lifecycle/vivenu-lifecycle.yml` before building on them.
