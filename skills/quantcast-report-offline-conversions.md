---
name: Report offline conversions to Quantcast server-to-server
description: Acquire a Quantcast browser token with the required consent signals, then POST conversion events to the Conversion API so offline and delayed sales are attributed alongside browser conversions.
api: https://help.quantcast.com/docs/tagging-with-the-quantcast-live-tag-using-the-conversion-api
operations: [acquireBrowserToken, reportConversions]
---

# Report offline conversions to Quantcast

The Conversion API is a server-to-server companion to the Live Tag. Use it for
events that happen outside the browser — offline sales, delayed financial
conversions, call-centre orders — and for signal resilience where third-party
cookies are unavailable.

This is the **only write surface** Quantcast exposes publicly. It is keyed by
account id, not by a bearer token, so treat the account id as configuration
and the browser token as the identity.

## 1. Acquire a browser token (in the browser, before the offline event)

Best accuracy comes from linking the server-side event back to real web
activity via a Quantcast browser token. Three supported ways:

**a. Live Tag callback (recommended)**

```html
<script type="text/javascript" async="true" src="https://pixel.quantserve.com/quant.js"></script>
<script type="text/javascript">
window._qevents = window._qevents || [];
_qevents.push({
  "qacct": "<account id>",
  "event": "PageView",
  "token_callback": function (bt) {
    // bt.token — the browser token string
    // bt.expires — expiry as a Unix epoch timestamp
  }
});
</script>
```

**b. The events SDK**

```js
import token from "@quantcast-labs/events-sdk";
token("<account-id>").then((t) => navigator.sendBeacon("/store-token", JSON.stringify(t)));
```

**c. Call the token endpoint directly** (JSON-P or fetch, form-encoded
parameters) when you use neither the tag nor the SDK.

Persist `token` on your side, keyed to the user. You do not need to send
`expires` back to Quantcast.

## 2. Consent is mandatory, not optional

The token endpoint is a consent gate. It **may refuse to issue a token** when
the signals are missing:

| Parameter | Rule |
|---|---|
| `a` | Account id (same value as `qacct`). |
| `gdpr` | `0`/`1` — **strictly required**. |
| `gdpr_consent` | Base64-URL IAB TCF v2 TC string. **MUST** be present when `gdpr=1`. |
| `gpp` / `gpp_sid` | IAB Global Privacy Platform string and applicable section ids — **SHOULD** be sent when a GPP-compatible CMP is on the page. |
| `us_privacy` | IAB US Privacy string. Deprecated in favour of GPP. |
| `fpa` / `fpan` / `d` | First-party cookie value, whether it was set this page load, and the cookie domain. Omitting `fpa` reduces report accuracy. |

Live Tag and the SDK integrate with approved CMPs automatically; a direct
call does not, and you inherit the obligation.

## 3. POST the conversion events

Send a **JSON array** — the API is batch-shaped by default — with the account
id in the `a` query parameter:

```
curl -X POST -H 'Content-Type: application/json' \
  -d '[{ "user": { "token": "<browser token>" }, "name": "Purchase" }]' \
  'https://pixel.quantserve.com/conversion?a=<account id>'
```

Fields, from the published data model:

- **conversion**: `name` (required), `time` (Unix epoch, seconds or
  milliseconds; defaults to now), `url`, `referer`
- **user**: `token` — **or**, when omitted, `client_user_agent` **and**
  `client_ip` are both required. `external_id` (your customer/cookie id) is
  strongly recommended. `email` must be a **SHA-256 hash**; unhashed
  addresses are rejected.
- **event**: `labels[]`, `orderid`, `revenue` (decimal, no currency symbol,
  in the account's billing currency), `product_category`

## 4. There is no idempotency key — design for that

Quantcast provides no idempotency header and does not de-duplicate on
`orderid`. Its own guidance is explicit: the tag is *stateless*, so if the
event fires it is counted. Prevent double counting on your side — track
transaction state before you send, and make sure a confirmation page cannot
re-fire on refresh or redirect.

## Verify

Use the Quantcast Tag Inspector Chrome extension to confirm the browser-side
tag is firing and emitting the expected labels. Allow a few minutes for
delivery and up to ~15 minutes for an event label to appear. There is no
sandbox or test-mode account — sends are live.
