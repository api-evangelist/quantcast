---
name: Authenticate against the Quantcast Platform and run your first query
description: Mint an OAuth 2.0 client-credentials token from auth.quantcast.com and use it to call the Quantcast Platform GraphQL API, respecting the two token buckets and the query-depth ceiling.
api: graphql/quantcast-graphql.md
operations: [organizations, accounts]
---

# Authenticate and run your first Quantcast query

Quantcast has one programmatic platform surface: a single GraphQL endpoint at
`https://developers.quantcast.com/api/v2/graphql`. It is **read-only** — the
published schema declares zero mutations. Anything that changes campaign state
has to be done in the Quantcast Platform UI.

## 1. Get credentials (one time, by a human)

API keys cannot be minted programmatically. In the Quantcast Platform: Profile
icon → **My Profile** → **API Key** section → **Create API Key**. Copy the Key
and Secret before closing the modal — they cannot be recovered, only replaced.

The credential behaves as a platform **user**. If it is not an organisation
Owner, it must be assigned to each account through the UI before the API will
return that account's data.

## 2. Mint a bearer token

```
curl --location --request POST 'https://auth.quantcast.com/oauth2/default/v1/token' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  --user '<apiKey>:<apiSecret>' \
  --data-urlencode 'grant_type=client_credentials' \
  --data-urlencode 'scope=api_access read_reports'
```

Use `access_token` from the response as a bearer token. Treat it as valid for
**one hour** — that is what the documentation states, even though the sample
response prints `expires_in: 86400`. Re-mint before expiry; an expired token
returns **403**, not 401. A missing token returns **401** with
`{"error":"No authentication token in request"}`.

Both scopes are required for reporting work: `api_access` for the API itself,
`read_reports` for report queries.

## 3. Call the endpoint

Always `POST`, always the same URL, always a JSON body with a `query` string.
Escape newlines inside the query string.

```
curl -H "Authorization: Bearer <access_token>" -X POST \
  -d '{"query": "query { organizations(limit: 1) { edges { id } } }"}' \
  https://developers.quantcast.com/api/v2/graphql
```

## 4. Walk the hierarchy

Every list query takes the same four arguments — `filter`, `order`, `limit`,
`offset` — and returns `{ edges, pageInfo { hasMore }, totalCount }`. There
are no cursors; page with `limit`/`offset` and stop when `hasMore` is false.

```
query GetAllAccounts {
  accounts(order: {asc: ACCOUNTS_NAME}, limit: 5) {
    pageInfo { hasMore }
    totalCount
    edges { id name }
  }
}
```

The object graph is Organization → Account → Campaign → AdSet →
CreativeAssignment → Creative. See `data-model/quantcast-data-model.yml`.

## 5. Respect the limits — they are unusual

Two independent token buckets, both refilling every minute:

- **10,000 requests/minute**
- **10,000 complexity tokens/minute** — every scalar/enum you select costs 1,
  every object costs 2, multiplied by every `limit:` you ask for. Your
  selection set *is* your bill.

Plus a hard **query depth ceiling of 50**. In practice you will hit the
complexity budget long before the depth limit.

Read the remaining budget off the **response body**, not the headers —
Quantcast returns no `X-RateLimit-*` headers:

```
"extensions": { "rateLimit": {
  "queryComplexityRemaining": 5800, "requestRemaining": 9600,
  "queryComplexityResetTime": "...", "requestResetTime": "..." } }
```

If you over-ask (`limit: 100` on an account with 10 campaigns) Quantcast
refunds the difference between requested and actual complexity — so an
over-generous limit is charged on what came back, not what you asked for.
Details in `rate-limits/quantcast-rate-limits.yml`.

## Errors

`400` malformed body · `401` no/invalid token · `403` expired token **or**
missing account permission · `413` response over 10MB · `429` REST reporting
rate limit · `500` platform error. The legacy REST envelope is
`{status, error, message, request_id}` — quote `request_id` to support. See
`errors/quantcast-problem-types.yml`.
