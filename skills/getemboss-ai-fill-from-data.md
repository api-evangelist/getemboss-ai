---
name: getemboss-ai-fill-from-data
description: Turn a flat PDF into a fillable form, put known values on it with a standard-fill session, and download the filled PDF — with the retry, ownership and retention rules Emboss documents.
api: openapi/getemboss-ai-account-openapi.yml
method: generated
generated: '2026-09-19'
operations: [account_quote_forms_quote_post, create_form_forms_post, get_form_forms__form_id__get, get_contract_forms__form_id__contract_get, create_session_sessions_post, put_fields_sessions__sid__fields_put, fill_sessions__sid__fill_post, session_pdf_sessions__sid__pdf_get, verify_filled_pdf_forms__form_id__verify_post]
sources: [https://getemboss.ai/docs/quickstart, https://getemboss.ai/docs/fill-from-data, https://getemboss.ai/docs/reference/sessions, https://getemboss.ai/docs/the-contract-shape]
---
# Fill a PDF form from data you already have

Base URL `https://api.getemboss.ai`. Every call carries `Authorization: Bearer sk_live_...`
(see `authentication/getemboss-ai-authentication.yml`). A key only sees the forms it created;
another owner's resource is a 404, not a 403.

## Steps

1. **Price it first (free, optional).** `account_quote_forms_quote_post` — `POST /forms/quote`
   multipart `file=@form.pdf`. Returns page count, whether the PDF is already fillable, and
   whether the free tier (5 of each kind per month, forms of 5 pages or fewer) covers it. Stateless,
   never metered.
2. **Create the form.** `create_form_forms_post` — `POST /forms` multipart `file=@form.pdf`
   (or `library=<slug>` from the public form library). Send an `Idempotency-Key` header (any UUID):
   a timed-out retry with the same key returns the original job instead of charging twice; keys are
   account-scoped and last 24 hours; a 4xx does not consume the key. Response is 202 with `id` and
   `status: processing`. Optional `retention: ephemeral` and `callback_url` (public https only).
3. **Wait for detection.** `get_form_forms__form_id__get` — `GET /forms/{form_id}` every 1-2 s,
   backing off to 5 s, until `status` is `ready` (or `failed`, which carries an `error`; fix the
   input and resubmit — failed jobs are not retried automatically). Or take the `form.ready` /
   `form.failed` callback signed with `X-Emboss-Signature`.
4. **Read the contract.** `get_contract_forms__form_id__contract_get` — `GET /forms/{form_id}/contract`
   lists every field (`id`, `label`, `kind`, `required`, `options` for choice fields, `group` for
   exclusive groups). Fill only what you were given: checkboxes take `yes`/`no`; choice fields take
   one of the listed option labels or values; never invent a value.
5. **Open a session.** `create_session_sessions_post` — `POST /sessions` with `form_id`. 409 if the
   form is not ready yet.
6. **Put the values.** `put_fields_sessions__sid__fields_put` — `PUT /sessions/{sid}/fields` with the
   values keyed by field id. 422 on an unknown id or invalid value; 409 if the session is already
   completed (terminal — open a new session, there is no undo).
7. **Render.** `fill_sessions__sid__fill_post` — `POST /sessions/{sid}/fill`. Billed as one standard
   fill (2¢, flat, any length). The session is now `completed`.
8. **Download.** `session_pdf_sessions__sid__pdf_get` — `GET /sessions/{sid}/pdf`. The response
   carries an `artifact_id`; hand that id to a fax or a free utility instead of re-uploading.
9. **Check your own work (optional).** `verify_filled_pdf_forms__form_id__verify_post` —
   `POST /forms/{form_id}/verify` with the filled PDF returns `complete`, `review_required`,
   `incomplete` or `failed` with the issues found. No model call; 1¢.

## Rules that matter

- 429 means back off exponentially (1 s, 2 s, 4 s); the documented default is 60 requests per window
  and no quota headers are returned (`rate-limits/getemboss-ai-rate-limits.yml`).
- 402 with `over_free_tier` / `over_page_cap` means the monthly allowance is used up or the form is
  over 5 pages with no card on file; relay `billing_url`.
- Under ephemeral processing the uploaded form, the fillable copy and every output are deleted 60-70
  minutes after the last activity; a swept form's document routes answer 410 — not a retryable error.
- Deleting a form (`delete_form_forms__form_id__delete`) is permanent and refuses (409) while work is
  running.
