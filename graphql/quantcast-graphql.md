# Quantcast GraphQL API

<!--
generated: '2026-08-13'
method: searched
source: https://developers.quantcast.com/docs/graphql-api/reference/
note: >-
  Operation inventory transcribed from the published schema reference pages.
  Live introspection is auth-gated — POST {__schema{queryType{name}}} to the
  endpoint returned HTTP 401 {"error":"No authentication token in request"}
  on 2026-08-13 — so no SDL is captured. Nothing below is inferred; each name
  appears verbatim in the reference.
-->

The Quantcast Platform GraphQL API (v2) is the primary programmatic interface to the Quantcast advertising platform. It exposes queries for reporting, campaign and ad set inspection, creative and audience metadata, geo/reference lookups, and account administration. Authentication uses OAuth 2.0 client credentials issued from the Quantcast Platform profile settings; tokens are short-lived and passed as bearer tokens. The full schema (queries, objects, enums, input objects, scalars) is documented on the developer portal but is **not** published as a downloadable OpenAPI or GraphQL SDL artifact, and introspection is authenticated-only.

**Endpoint:** https://developers.quantcast.com/api/v2/graphql (POST only, single endpoint)

**Documentation:** https://developers.quantcast.com/docs/graphql-api

## Surface shape (from the published reference, 2026-08-13)

| | |
|---|---|
| Queries | 25 |
| Mutations | **0** — "The API doesn't have any mutation types at this point." |
| Object types | 93 |
| Introspection | auth-gated (HTTP 401 without a bearer token) |
| SDL published | no |
| Postman collection | yes — https://developers.quantcast.com/docs/QuantcastDeveloperAPI.postman_collection.json |

The API is **read-only**. Every write to campaign state happens in the Quantcast Platform UI. The only public write surface Quantcast operates is the Conversion API on `pixel.quantserve.com`.

## Queries

**Reporting**

- `accountMetricsReport` — metrics report for ad delivery and performance; the API equivalent of Report Builder.
- `availableBreakdownsAndMetrics` — the breakdowns and metrics available on an account, per account.
- `asyncMetricsReport` *[Beta]* — request an async metrics report.
- `asyncMetricsReportDownloadURL` *[Beta]* — download URL for an async metrics report.
- `asyncAttributedActionsReport` *[Beta]* — request an async attributed-actions report.
- `asyncAttributedActionsReportDownloadURL` *[Beta]* — download URL for an async attributed-actions report.

**Campaign objects**

- `organizations` — organizations the credential can see.
- `accounts` — account resources the credential is assigned to.
- `campaigns` — campaigns.
- `adsets` — ad sets.
- `creatives` — creative resources.
- `creativeAssignments` — creative-to-ad-set assignments.
- `surveys` — brand-lift survey resources.
- `keyEvents` — changes recorded against a resource.

**Access administration**

- `members` — members of an organization.
- `roles` — account-level roles defined under an organization.
- `teams` — teams defined under an organization.
- `teamMembers` — members associated with a team.
- `userAccountAssignments` — non-owner users assigned to accounts via roles.

**Targeting reference data**

- `countries`, `states`, `cities`, `metroAreas` (media markets/DMAs), `postcodes`, `isps`.

## Conventions

Every list query takes `filter`, `order`, `limit` and `offset`, and returns a `*Connections` type with `edges`, `pageInfo { hasMore }` and `totalCount`. There are no cursors. Filters and ordering are typed input objects per collection (`AccountsFilterInput`, `AccountsOrderByInput`, …).

Rate limiting is dual-bucket — 10,000 requests/minute **and** 10,000 query-complexity tokens/minute, plus a query-depth ceiling of 50 — and the remaining budget is returned in the response body under `extensions.rateLimit`, not in headers. See `rate-limits/quantcast-rate-limits.yml`.

**References:**

- Documentation: https://developers.quantcast.com/docs/graphql-api
- Authentication: https://developers.quantcast.com/docs/get-started/authentication/
- Reference: https://developers.quantcast.com/docs/graphql-api/reference/
- Queries: https://developers.quantcast.com/docs/graphql-api/reference/queries/
- Objects: https://developers.quantcast.com/docs/graphql-api/reference/objects/
- Rate limits: https://developers.quantcast.com/docs/graphql-api/usage/rate-limits/
- Recipes: https://developers.quantcast.com/docs/graphql-api/usage/recipes/
- Understanding the domain: https://developers.quantcast.com/docs/get-started/understanding-the-domain/
