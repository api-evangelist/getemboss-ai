---
name: getemboss-ai-pay-per-call-anonymous
description: Use Emboss with no account — get an exact free quote, answer the 402 with an x402 or MPP payment, resend the identical request, poll the tokened status URL, and reuse the result by artifact_id + artifact_token.
api: openapi/getemboss-ai-pay-per-call-openapi.yml
method: generated
generated: '2026-09-19'
operations: [pay_quote, pay_make_fillable, pay_fill, pay_fill_with_context, pay_read, pay_fax]
sources: [https://getemboss.ai/docs/pay-per-call, https://getemboss.ai/docs/pay-per-call/mpp, https://getemboss.ai/docs/pay-per-call/x402, https://api.getemboss.ai/pay/llms.txt]
---
# Pay per call, anonymously

The pay door is `https://api.getemboss.ai/pay`. No API key, no account, always ephemeral
(documents deleted 60-70 minutes after the last activity). Every operation takes the PDF as JSON
(`pdf_url` or `pdf_base64`, 10 MB) or as a multipart `file`.

## Steps

1. **Quote (free, stateless).** `pay_quote` — `POST /pay/quote` with the PDF (and the same context
   files if you will call fill-with-context). Returns `pages`, `already_fillable`, and the exact
   price of each operation, plus `methods` and the card minimum. Anonymous quotes are limited per IP
   per hour. If `already_fillable` is true, skip make-fillable.
2. **Send the request unpaid.** e.g. `pay_make_fillable` — `POST /pay/make-fillable`. Emboss answers
   `402 Payment Required` with one challenge per rail:
   - **MPP** in `WWW-Authenticate: Payment` — Tempo USDC.e at the exact price, or a Stripe card via
     Shared Payment Tokens with a $0.50 minimum;
   - **x402** in a `PAYMENT-REQUIRED` header — USDC on Base (`eip155:8453`), or a gasless
     `GatewayWalletBatched` entry for every chain Circle Gateway supports.
   The 402 always carries the exact amount; `x-payment-info` on each operation in the spec gives the
   floor/ceiling and the accepted networks/assets.
3. **Pay and resend the identical request** with `Authorization: Payment <credential>` (MPP) or the
   signed EIP-3009 authorization (x402). A standard client (`pympp`, `mppx`, the x402 SDKs, Circle's
   CLI) does this for you. Do not change the body between the two requests.
4. **Accepted.** `202` with `job_id`, `status_url` (carries an HMAC token — no auth needed to poll),
   `quote_id`, and a `Payment-Receipt` header. Results also carry `artifact_id` and, for anonymous
   callers, an `artifact_token` — keep both together; the token is your proof of ownership.
5. **Poll `status_url`** until the job is ready and download the result from it. Quotes are payable
   for 24 hours.
6. **Chain without re-uploading.** `pay_fax` — `POST /pay/fax` with `to` (E.164) and either the
   `artifact_id` + `artifact_token` from step 4 or a `sources` list, priced per transmitted page
   (3¢ floor, $0.50 card minimum); `pay_read` — `POST /pay/read` reads a filled PDF back to labelled
   values for 1¢ and stores nothing. The seven free utilities run on your artifacts too via
   `POST /utilities/{skill}` with the token on every source.

## Rules that matter

- A rejected or failed x402 attempt on the pay door gets a fresh 402 and a new nonce on the same quote
  is accepted; on the A2A rail a failed attempt consumes the quote's nonce — ask for a new quote.
- If verification passes but on-chain settlement fails after the job ran, nothing is charged.
- `/pay/read` results stay on the quote for a replay until the quote expires and is purged.
- Fees are otherwise non-refundable; a failed paid fax is refunded (automatically on card).
