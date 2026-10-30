# Emboss

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Emboss is a PDF form-filling API for developers and agents. Hand it a flat or scanned PDF and it detects the fields and returns a fillable AcroForm, fills the form from structured values or from supporting documents (proposing every answer with its source, asking about what is missing), verifies the result, reads a filled form back into labelled values, batch-fills one copy per spreadsheet row, packages the filled form with its attachments and a receipt, and faxes the result to any US, Canadian or Mexican fax number. Usage-based pricing in cents with a monthly free allowance and no subscription. The same engine is exposed through four doors on api.getemboss.ai: a 115-operation authenticated REST API (OpenAPI 3.1, Bearer API key or OAuth 2.1 with dynamic client registration), a remote MCP server (20 tools, OAuth-protected, listed in the MCP registry), a signed A2A 1.0 agent card with 23 skills, and an anonymous pay-per-call door priced per job over x402 (USDC on Base) or MPP (Tempo stablecoin or card). Every document is deleted 60-70 minutes after the last activity under ephemeral processing.

**Areas:** PDF · Forms · Document Processing · Form Filling · Fax · Data Extraction · Agent-Native · MCP · A2A · x402 · pay-per-call · Government Forms

## Emboss on APIs.io

Everything profiled for Emboss is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/getemboss-ai/](https://apis.io/providers/getemboss-ai/)** — or go straight to one of the APIs or properties below.

### APIs (23)

- [Emboss MCP Server](https://apis.io/apis/getemboss-ai/emboss-mcp-server/) — Remote Model Context Protocol server at https://api.getemboss.ai/mcp (Streamable HTTP) exposing twenty form-filling tools under forms:read / forms:write…
- [Emboss A2A Agent](https://apis.io/apis/getemboss-ai/emboss-a2a-agent/) — Agent2Agent interface at https://api.getemboss.ai/a2a (JSON-RPC, A2A 1.0) discovered through a signed agent card served at /.well-known/agent-card.json on…
- [Emboss Admin API](https://apis.io/apis/getemboss-ai/getemboss-ai-admin-api/) — The Admin API from Emboss — 40 operation(s) for admin.
- [Emboss App API](https://apis.io/apis/getemboss-ai/getemboss-ai-app-api/) — The App API from Emboss — 3 operation(s) for app.
- [Emboss Artifacts API](https://apis.io/apis/getemboss-ai/getemboss-ai-artifacts-api/) — The Artifacts API from Emboss — 2 operation(s) for artifacts.
- [Emboss D API](https://apis.io/apis/getemboss-ai/getemboss-ai-d-api/) — The D API from Emboss — 1 operation(s) for d.
- [Emboss Fax API](https://apis.io/apis/getemboss-ai/getemboss-ai-fax-api/) — The Fax API from Emboss — 2 operation(s) for fax.
- [Emboss Forms API](https://apis.io/apis/getemboss-ai/getemboss-ai-forms-api/) — The Forms API from Emboss — 25 operation(s) for forms.
- [Emboss Health API](https://apis.io/apis/getemboss-ai/getemboss-ai-health-api/) — The Health API from Emboss — 1 operation(s) for health.
- [Emboss Keys API](https://apis.io/apis/getemboss-ai/getemboss-ai-keys-api/) — The Keys API from Emboss — 2 operation(s) for keys.
- [Emboss Library API](https://apis.io/apis/getemboss-ai/getemboss-ai-library-api/) — The Library API from Emboss — 1 operation(s) for library.
- [Emboss OAuth API](https://apis.io/apis/getemboss-ai/getemboss-ai-oauth-api/) — The Oauth API from Emboss — 5 operation(s) for oauth.
- [Emboss Openapi.json API](https://apis.io/apis/getemboss-ai/getemboss-ai-openapi-json-api/) — The Openapi.json API from Emboss — 1 operation(s) for openapi.json.
- [Emboss Pay API](https://apis.io/apis/getemboss-ai/getemboss-ai-pay-api/) — The Pay API from Emboss — 7 operation(s) for pay.
- [Emboss Pricing API](https://apis.io/apis/getemboss-ai/getemboss-ai-pricing-api/) — The Pricing API from Emboss — 1 operation(s) for pricing.
- [Emboss Proposals API](https://apis.io/apis/getemboss-ai/getemboss-ai-proposals-api/) — The Proposals API from Emboss — 6 operation(s) for proposals.
- [Emboss Sessions API](https://apis.io/apis/getemboss-ai/getemboss-ai-sessions-api/) — The Sessions API from Emboss — 5 operation(s) for sessions.
- [Emboss Stripe API](https://apis.io/apis/getemboss-ai/getemboss-ai-stripe-api/) — The Stripe API from Emboss — 1 operation(s) for stripe.
- [Emboss Usage API](https://apis.io/apis/getemboss-ai/getemboss-ai-usage-api/) — The Usage API from Emboss — 1 operation(s) for usage.
- [Emboss Users API](https://apis.io/apis/getemboss-ai/getemboss-ai-users-api/) — The Users API from Emboss — 7 operation(s) for users.
- [Emboss Utilities API](https://apis.io/apis/getemboss-ai/getemboss-ai-utilities-api/) — The Utilities API from Emboss — 1 operation(s) for utilities.
- [Emboss Webhooks API](https://apis.io/apis/getemboss-ai/getemboss-ai-webhooks-api/) — The Webhooks API from Emboss — 1 operation(s) for webhooks.
- [Emboss .well Known API](https://apis.io/apis/getemboss-ai/getemboss-ai-well-known-api/) — The .well Known API from Emboss — 3 operation(s) for .well known.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Getemboss Ai Callbacks](https://apis.io/asyncapis/getemboss-ai/getemboss-ai-callbacks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [emboss](https://apis.io/servers/getemboss-ai/emboss/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Getemboss Ai Agentic Access](https://apis.io/agentic-access/getemboss-ai/getemboss-ai-agentic-access/)

#### Overlays (23)

OpenAPI overlays, including conversational phrasing for each operation.

- [Getemboss Ai Account Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-account-overlay/)
- [Getemboss Ai Admin Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-admin-api-phrasing-overlay/)
- [Getemboss Ai App Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-app-api-phrasing-overlay/)
- [Getemboss Ai Artifacts Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-artifacts-api-phrasing-overlay/)
- [Getemboss Ai D Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-d-api-phrasing-overlay/)
- [Getemboss Ai Fax Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-fax-api-phrasing-overlay/)
- [Getemboss Ai Forms Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-forms-api-phrasing-overlay/)
- [Getemboss Ai Health Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-health-api-phrasing-overlay/)
- [Getemboss Ai Keys Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-keys-api-phrasing-overlay/)
- [Getemboss Ai Library Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-library-api-phrasing-overlay/)
- [Getemboss Ai Oauth Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-oauth-api-phrasing-overlay/)
- [Getemboss Ai Openapi Json Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-openapi-json-api-phrasing-overlay/)
- [Getemboss Ai Pay Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-pay-api-phrasing-overlay/)
- [Getemboss Ai Pay Per Call Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-pay-per-call-overlay/)
- [Getemboss Ai Pricing Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-pricing-api-phrasing-overlay/)
- [Getemboss Ai Proposals Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-proposals-api-phrasing-overlay/)
- [Getemboss Ai Sessions Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-sessions-api-phrasing-overlay/)
- [Getemboss Ai Stripe Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-stripe-api-phrasing-overlay/)
- [Getemboss Ai Usage Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-usage-api-phrasing-overlay/)
- [Getemboss Ai Users Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-users-api-phrasing-overlay/)
- [Getemboss Ai Utilities Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-utilities-api-phrasing-overlay/)
- [Getemboss Ai Webhooks Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-webhooks-api-phrasing-overlay/)
- [Getemboss Ai Well Known Api Phrasing Overlay](https://apis.io/overlays/getemboss-ai/getemboss-ai-well-known-api-phrasing-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Getemboss Ai Authentication](https://apis.io/security/getemboss-ai/getemboss-ai-authentication/)
- [Getemboss Ai Domain Security](https://apis.io/security/getemboss-ai/getemboss-ai-domain-security/)
- [Getemboss Ai Vulnerability Disclosure](https://apis.io/security/getemboss-ai/getemboss-ai-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Getemboss Ai Scopes](https://apis.io/scopes/getemboss-ai/getemboss-ai-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Getemboss Ai Plans Pricing](https://apis.io/plans/getemboss-ai/getemboss-ai-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Getemboss Ai Rate Limits](https://apis.io/rate-limits/getemboss-ai/getemboss-ai-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://getemboss.ai/)
- [Documentation](https://getemboss.ai/docs)
- [Getting started](https://getemboss.ai/docs/quickstart)
- [API reference](https://getemboss.ai/docs/reference/create-form)
- [Pricing](https://getemboss.ai/pricing)
- [Sign up](https://getemboss.ai/signup)
- [Security](https://getemboss.ai/security)
- [Terms of service](https://getemboss.ai/terms)
- [Privacy policy](https://getemboss.ai/privacy)
- [GitHub](https://github.com/GetEmboss-ai)

## API Evangelist rating

**Kin Score 68.2** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 85.0 |
| Contract quality | 54.6 |
| Contract governance | 18.2 |
| Operational transparency | 60.5 |
| Developer ergonomics | 64.3 |
| Access clarity | 76.3 |

**Agent readiness 75.2** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | yes |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | served (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | verified |
| OpenAPI Examples | documented (partial credit) |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | yes |
| Well Known Catalog | yes |
| Consent Identity | yes |
| Agent Card | conformant |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | self |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 52.0** — Government & Public Sector

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/getemboss-ai/](https://apis.io/providers/getemboss-ai/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Emboss: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/getemboss-ai/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
