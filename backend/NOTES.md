# Backend Notes (Express + MongoDB)

This file explains how I structured the backend in simple words.

---

## Collections I Created

### 1. Users
Stores:
- Airtable ID
- access token
- refresh token
- login time

### 2. Forms
Stores:
- owner ID
- Airtable base ID
- Airtable table ID
- list of questions
- conditional logic

### 3. Responses
- formId
- airtableRecordId
- answers
- createdAt
- updatedAt
- deletedInAirtable (boolean)

---

## Routes I Planned

### Auth
- `/auth/login`
- `/auth/callback`

### Form Builder
- `POST /forms`
- `GET /forms/:id`

### Responses
- `POST /forms/:id/submit`
- `GET /forms/:id/responses`

### Webhook
- `POST /webhooks/airtable`

---

## Conditional Logic Function

Kept it as a pure function to test independently.

---

## Webhook Handling

If Airtable sends:
- updated record → sync answers
- deleted record → mark deletedInAirtable = true

---

## Airtable API Notes

Only supported field types:
- short text
- long text
- single select
- multi select
- attachment

Others I skip to avoid errors.
