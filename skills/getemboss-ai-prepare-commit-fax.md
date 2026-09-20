---
name: getemboss-ai-prepare-commit-fax
description: Fill a form from supporting documents the safe way — prepare a proposal with evidence, resolve the open questions, commit with an idempotency key, attach supporting documents into one submission package, and fax the result, tracking delivery.
api: openapi/getemboss-ai-account-openapi.yml
method: generated
generated: '2026-09-19'
operations: [prepare_new_forms_prepare_post, prepare_existing_forms__form_id__prepare_post, get_proposal_proposals__proposal_id__get, add_attachment_proposals__proposal_id__attachments_post, remove_attachment_proposals__proposal_id__attachments__n__delete, commit_proposals__proposal_id__commit_post, receipt_proposals__proposal_id__receipt_get, commit_pdf_proposals__proposal_id__pdf_get, send_fax_fax_post, get_fax_fax__job_id__get, get_artifact_artifacts__artifact_id__get]
sources: [https://getemboss.ai/docs/prepare-commit-verify, https://getemboss.ai/docs/submission-package, https://getemboss.ai/docs/send-fax, https://getemboss.ai/docs/artifacts, https://getemboss.ai/docs/reference/read-and-package, https://getemboss.ai/docs/reference/fax]
---
# Prepare, commit, package and fax

Use this instead of a direct context fill whenever a human or an agent should see what Emboss
decided — and on what evidence — before anything is written into the PDF.

## Steps

1. **Prepare.** `prepare_new_forms_prepare_post` — `POST /forms/prepare` with the blank PDF plus
   context (`context` files, `context_text`, `context_urls`, up to 5 documents / 30 MB total), or
   `prepare_existing_forms__form_id__prepare_post` — `POST /forms/{form_id}/prepare` for a form already
   in the library. Optional `policy`: `safe` (write high and medium confidence, default) or `strict`
   (high only). Billed as one context fill (3¢ flat up to 5 pages of form+context, +2¢/page after).
   Returns 202 with a `job_id` and a `proposal_id`.
2. **Read the proposal.** `get_proposal_proposals__proposal_id__get` — `GET /proposals/{proposal_id}`:
   every field's state, candidate values each naming the document and page it came from, the
   `questions` still open, `confirmations` awaiting a yes, and the attachment `requirements` the form
   asks for. Free.
3. **Resolve.** Answer the open questions from the user or your own context. Never guess a value the
   documents do not support.
4. **Attach (optional).** `add_attachment_proposals__proposal_id__attachments_post` —
   `POST /proposals/{proposal_id}/attachments` (PDF, PNG or JPEG; optional `requirement` name).
   Reversible until commit: `remove_attachment_proposals__proposal_id__attachments__n__delete` —
   `DELETE /proposals/{proposal_id}/attachments/{n}` (409 after commit or expiry, 410 after the
   retention sweep).
5. **Commit.** `commit_proposals__proposal_id__commit_post` — `POST /proposals/{proposal_id}/commit`
   JSON `{confirm: [field ids], values: [{field_id, value, note}], policy, package: true|false,
   idempotency_key}`. Set `idempotency_key` so a retried commit returns the original job. The commit
   writes, renders with text that fits, verifies, and returns a receipt; with `package: true` it also
   builds the submission package (filled form + attachments in the form's order + embedded receipt),
   billed as one package (2¢). Up to 10 commits per proposal are free within the billed prepare; each
   commit is a new artifact and earlier artifacts never change.
6. **Collect.** `receipt_proposals__proposal_id__receipt_get` — `GET /proposals/{proposal_id}/receipt`
   (survives the retention sweep, values redacted) and `commit_pdf_proposals__proposal_id__pdf_get` —
   `GET /proposals/{proposal_id}/pdf`. The job result lists `artifacts` with roles `filled`, `receipt`,
   `package`.
7. **Confirm the fax number with the user** and show it back in E.164 form (`+15025551212`). US,
   Canada and Mexico are served.
8. **Fax.** `send_fax_fax_post` — `POST /fax` JSON `{to, artifact_id}` (the package or filled PDF —
   no download needed) or `{to, sources: [{artifact_id, pages: "1-2"}, ...]}` for one packet. Send an
   `Idempotency-Key`; independently, the same artifact to the same number within ten minutes returns
   the same job with `deduplicated: true`. Returns 202 with `job_id`, `pages`, `price_cents`,
   `destination_masked`. A fax in flight cannot be cancelled.
9. **Track delivery.** `get_fax_fax__job_id__get` — `GET /fax/{job_id}` until `status` is `delivered`
   (carries `price` and `artifact_sha256`) or `failed` (carries `failure_category` in
   `destination|delivery|timeout|vendor`, `retryable`, and the refund state). Billed 3¢/page only at
   delivery; a failed fax is not charged. Retry a retryable failure by sending again — each send is
   its own job.
10. **Audit lineage (optional).** `get_artifact_artifacts__artifact_id__get` —
    `GET /artifacts/{artifact_id}` shows `produced_by`, `inputs` and `used_by`, so you can prove which
    pages of which files went out.

## Rules that matter

- An uncommitted proposal is auto-committed under its own policy when it expires (receipt marks it
  `auto`), so decide promptly.
- Ephemeral processing deletes the documents 60-70 minutes after the last activity; only the redacted
  receipt record survives.
- Fees are non-refundable except the failed-fax case above; on the anonymous pay door a failed paid
  fax is refunded automatically on card and by support for stablecoins.
