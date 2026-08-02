---
name: Manage events in vivenu
description: Create, retrieve, and list events on the vivenu ticketing platform.
api: openapi/vivenu-openapi-original.json
operations: [events/list, events/create, events/get, events/update]
---

# Manage events in vivenu

Use this skill to work with events — the core object organizers sell tickets against.

## Auth
Send every request with `Authorization: Bearer <API_KEY>`. Use a **staging** key
against `https://vivenu.dev/api` while building; switch the base URL to
`https://vivenu.com/api` for production. See `authentication/vivenu-authentication.yml`.

## Steps
1. **List existing events** — `GET /api/events` (`events/list`). Page with
   `skip` (offset) and `top` (page size) query params.
2. **Create an event** — `POST /api/events` (`events/create`) with the event
   body (name, dates, seller, ticket types).
3. **Retrieve one event** — `GET /api/events/{id}` (`events/get`).
4. **Update an event** — `PUT /api/events/{id}` (`events/update`).

## Rules
- Pagination is offset-based (`skip`/`top`), not cursor-based.
- There is **no idempotency-key** support — do not assume safe retries on
  create; check for the created resource before retrying.
- Errors return `{ statusCode, error, message }` (not RFC 9457). See
  `errors/vivenu-problem-types.yml`.
- An event `belongs_to` a Seller via `sellerId`.
