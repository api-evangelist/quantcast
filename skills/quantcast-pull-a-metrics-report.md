---
name: Pull a Quantcast account metrics report
description: Discover the breakdowns and metrics available on an account, then run accountMetricsReport — the API equivalent of Report Builder — and fall back to the async report queries for large pulls.
api: graphql/quantcast-graphql.md
operations: [availableBreakdownsAndMetrics, accountMetricsReport, asyncMetricsReport, asyncMetricsReportDownloadURL]
---

# Pull a Quantcast account metrics report

`accountMetricsReport` is the API equivalent of Report Builder in the
Quantcast Platform, and is the reason most integrations exist. It replaces
the legacy REST Reporting API, which Quantcast announced for sunset by
**1 October 2024**. Do not build against the REST endpoint.

Requires a bearer token minted with the `read_reports` scope — see
`skills/quantcast-authenticate-and-query.md`.

## 1. Discover what this account supports first

Breakdown and metric names are **not** a fixed global list; they vary by
account. Always ask before you report.

```
query AvailableBreakdownsAndMetrics($accountId: Long!) {
  availableBreakdownsAndMetrics(accountId: $accountId) {
    breakdowns { name }
    metrics { name }
  }
}
```

## 2. Run the report

```
query AccountMetricsReport(
  $accountId: Long!,
  $startDate: Date!,
  $endDate: Date!,
  $timezone: String,
  $filters: [AccountMetricsReportRequest_FilterInput!],
  $breakdowns: [String!],
  $metrics: [String!]!
) {
  accountMetricsReport(
    accountId: $accountId,
    startDate: $startDate,
    endDate: $endDate,
    timezone: $timezone,
    filters: $filters,
    breakdowns: $breakdowns,
    metrics: $metrics
  ) { breakdowns metrics metadata }
}
```

Argument rules straight from the reference:

- `accountId`, `startDate`, `endDate` and `metrics` are **required**;
  `timezone`, `filters` and `breakdowns` are optional.
- **`startDate` is inclusive, `endDate` is exclusive.** A single day is
  `startDate: 2026-08-01, endDate: 2026-08-02`.
- `timezone` is an ISO 8601 TZ identifier (`America/Los_Angeles`). Omit it and
  the account's own timezone is used — never assume UTC.
- Each entry in `filters` applies to a specific breakdown; a row must satisfy
  **all** filters to appear.
- Rows come back as entry maps (`breakdowns`, `metrics`, `metadata`), not as a
  fixed column set — read them by key.

## 3. Watch the cost, not the row count

Report queries are cheap in *requests* and expensive in *complexity*. Every
selected field costs tokens against the 10,000/minute complexity bucket.
Narrow the metric list before you widen the date range, and read
`extensions.rateLimit.queryComplexityRemaining` on every response.

## 4. Large or slow pulls: use the async pair

Four `[Beta]` queries exist for reports too large to return inline. They are
labelled beta in the published reference with no stability guarantee, so guard
them behind a feature flag:

- `asyncMetricsReport(metricsReportRequest, fileName)` → returns a record with
  a `reportRequestId`
- `asyncMetricsReportDownloadURL(entity, reportRequestId)` → returns a signed
  download URL

The attributed-actions equivalents are `asyncAttributedActionsReport` and
`asyncAttributedActionsReportDownloadURL`.

## Gotchas

- **Money is in micro-units on campaign objects** (a $100 budget is
  `100000000`) but plain decimals on conversion revenue. Do not mix them.
- Data freshness is not instantaneous; the legacy REST surface exposed a
  `data_last_updated` timestamp for exactly this reason.
- A 403 here usually means the credential is not assigned to the account, not
  that the token is bad. Have an Owner assign it in the UI.
