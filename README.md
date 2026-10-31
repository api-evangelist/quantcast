# Quantcast

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

Quantcast is a San Francisco-headquartered digital advertising and audience intelligence company founded in 2006. Its flagship offering is the Quantcast Platform, an AI-driven demand-side platform (DSP) for programmatic display, video, CTV, audio, mobile, and native advertising, powered by the company's proprietary Audience Graph and Ara AI engine. Quantcast also operates Quantcast Measure, a free audience measurement product that has tagged millions of digital properties to produce demographic, psychographic, and cross-device audience insights. For programmatic access, Quantcast exposes a developer portal at developers.quantcast.com built around a GraphQL API (v2) for reporting, campaign management, and audience operations on the Quantcast Platform, secured via OAuth 2.0 client credentials. A server-to-server Conversion API augments the browser-side Live Tag for offline and signal-loss-resilient conversion tracking. Quantcast Choice, the company's IAB TCF v2-compliant Consent Management Platform, was acquired by InMobi in August 2023 and is now operated as part of InMobi CMP; legacy Quantcast Choice mobile SDKs remain published under the quantcast GitHub organization for reference. Quantcast also open-sources the Quantcast File System (QFS), a C++ distributed file system, and mobile/Roku measurement SDKs.

**Areas:** Advertising · AdTech · Programmatic Advertising · DSP · Audience Measurement · Audience Intelligence · Consent Management · CMP · Privacy · GraphQL · Conversion Tracking · CTV

## Quantcast on APIs.io

Everything profiled for Quantcast is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/quantcast/](https://apis.io/providers/quantcast/)** — or go straight to one of the APIs or properties below.

### APIs (3)

- [Quantcast Platform GraphQL API](https://apis.io/apis/quantcast/quantcast-platform-graphql-api/) — The Quantcast Platform GraphQL API (v2) is the primary programmatic interface to the Quantcast advertising platform. It exposes queries and mutations for…
- [Quantcast Conversion API](https://apis.io/apis/quantcast/quantcast-conversion-api/) — The Quantcast Conversion API is a server-to-server integration that augments the browser-side Quantcast Live Tag. It accepts a JSON array of conversion…
- [Quantcast Measure (Live Tag)](https://apis.io/apis/quantcast/quantcast-measure-tag/) — Quantcast Measure is the company's free audience measurement product. Publishers and advertisers integrate the Quantcast Live Tag (Q Pixel) on web…

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### GraphQL (1)

GraphQL schemas.

- [Quantcast GraphQL API](https://apis.io/graphqls/quantcast/quantcast-graphql/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [quantcast](https://apis.io/servers/quantcast/quantcast/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Quantcast Authentication](https://apis.io/security/quantcast/quantcast-authentication/)
- [Quantcast Domain Security](https://apis.io/security/quantcast/quantcast-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Quantcast Scopes](https://apis.io/scopes/quantcast/quantcast-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Quantcast Plans Pricing](https://apis.io/plans/quantcast/quantcast-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Quantcast Rate Limits](https://apis.io/rate-limits/quantcast/quantcast-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.quantcast.com)
- [Documentation](https://developers.quantcast.com/docs/graphql-api)
- [Getting started](https://developers.quantcast.com/docs/get-started/)
- [API reference](https://developers.quantcast.com/docs/graphql-api/reference/)
- [Sign up](https://www.quantcast.com/signup/)
- [Support](https://help.quantcast.com)
- [Blog](https://www.quantcast.com/resources/blog/)
- [Terms of service](https://legal.quantcast.com/)
- [Privacy policy](https://www.quantcast.com/privacy/)
- [GitHub](https://github.com/quantcast)
- [Status](https://status.quantcast.com)

## API Evangelist rating

**Kin Score 43.4** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 79.5 |
| Contract quality | 5.3 |
| Contract governance | 18.2 |
| Operational transparency | 50.0 |
| Developer ergonomics | 80.4 |
| Access clarity | 34.2 |

**Agent readiness 21.4** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | — |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | — |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | na |

**Regulatory alignment 31.8** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/quantcast/](https://apis.io/providers/quantcast/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Quantcast: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/quantcast/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
