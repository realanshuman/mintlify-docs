# Source: https://tokensupply.in/docs/webhooks

## TokenSupply Webhooks

Webhooks push real-time events to your server as they happen — no polling required. Configure endpoints in **Settings → Webhooks**.

Events fire automatically from the database, so anything that changes your data (the dashboard, the API, marketplace syncs) triggers a webhook.

## How it works

- You register an endpoint URL and select which events to subscribe to. A signing secret (`whsec_...`) is generated for you.
- When a subscribed event occurs, TokenSupply enqueues a delivery and immediately POSTs a signed JSON payload to your URL.
- Your endpoint must respond with a `2xx` status within **10 seconds**.
- Non-2xx responses (or timeouts) are retried with exponential backoff up to **5 attempts**: after **1, 5, 15, 60, 180 minutes**. After that the delivery is marked `failed`.

You can inspect every attempt under **View deliveries** on each endpoint, and fire a `ping` test event at any time.

## Request format

Each delivery is an HTTP POST with these headers:

| Header | Description |
| --- | --- |
| `Content-Type` | application/json |
| `User-Agent` | TokenSupply-Webhooks/1 |
| `X-TokenSupply-Event` | The event type, e.g. order.completed |
| `X-TokenSupply-Delivery` | Unique delivery id (for idempotency) |
| `X-TokenSupply-Signature` | sha256=&lt;hmac&gt; — see below |

Body:

```
{
  "id": "delivery-uuid",
  "event": "order.completed",
  "created": 1749312000,
  "data": { ... event-specific payload ... }
}
```

`created` is a Unix timestamp (seconds). Use `id` / `X-TokenSupply-Delivery` to deduplicate, since retries reuse the same delivery id.

## Verifying signatures

Every payload is signed with HMAC-SHA256 using your endpoint's secret. Compute the HMAC over the **raw request body** and compare it (constant-time) to the hex value in `X-TokenSupply-Signature` after the `sha256=` prefix.

### Node.js (Express)

```
import crypto from "node:crypto";

// IMPORTANT: verify against the raw body, not the parsed JSON.
app.post("/webhooks/tokensupply", express.raw({ type: "application/json" }), (req, res) => {
  const secret = process.env.TOKENSUPPLY_WEBHOOK_SECRET; // whsec_...
  const signature = req.header("X-TokenSupply-Signature") || "";
  const expected = "sha256=" + crypto.createHmac("sha256", secret).update(req.body).digest("hex");

  const ok =
    signature.length === expected.length &&
    crypto.timingSafeEqual(Buffer.from(signature), Buffer.from(expected));

  if (!ok) return res.status(401).send("invalid signature");

  const event = JSON.parse(req.body.toString());
  // handle event.event / event.data ...
  res.sendStatus(200);
});
```

### Python (Flask)

```
import hmac, hashlib
from flask import request, abort

def verify(secret: str):
    raw = request.get_data()  # raw bytes
    expected = "sha256=" + hmac.new(secret.encode(), raw, hashlib.sha256).hexdigest()
    sig = request.headers.get("X-TokenSupply-Signature", "")
    if not hmac.compare_digest(sig, expected):
        abort(401)
```

## Event types

Subscribe to any combination of the following.

### Orders

`order.created`, `order.completed`, `order.refunded`, `order.cancelled`. **data:** id, order\_id, marketplace, marketplace\_order\_id, status, payment\_status, product\_id, customer\_id, quantity, amount, currency, created\_at

### Inventory

`inventory.created`, `inventory.sold`, `inventory.low_stock` (fires when available stock for a product drops to 5 or fewer). **data** (created/sold): id, ref\_id, product\_id, purchase\_order\_id, status, expiry\_date, created\_at. **data** (low\_stock): product\_id, available, threshold. The raw `value` is **never** included.

### Tickets

`ticket.created`, `ticket.updated`, `ticket.resolved`. **data:** id, ticket\_code, title, issue\_type, severity, status, order\_id, product\_id, seller\_id, created\_at

### Purchase Orders

`purchase_order.created`, `purchase_order.paid`. **data:** id, po\_number, seller\_id, product\_id, quantity, status, total\_value, currency, created\_at

### Vendors

`vendor.created`. **data:** id, name, email, seller\_type, status, created\_at

### Products

`product.created`, `product.updated`, `product.deleted`. **data:** id, name, sku, product\_type, status, category, brand, created\_at

### Customers

`customer.created`, `customer.updated`. **data:** id, first\_name, last\_name, email, customer\_type, country, created\_at

### Integrations & sales channels

`integration.connected`, `integration.disconnected`. **data:** id, marketplace, is\_active, created\_at. Credentials are **never** included.

### Test

`ping` — sent when you click **Send test** on an endpoint.

## Best practices

- **Respond fast.** Return 2xx immediately and process asynchronously; you have a 10-second window before the request times out and is retried.
- **Deduplicate.** Retries reuse `X-TokenSupply-Delivery`; treat handling as idempotent.
- **Always verify the signature** against the raw body before trusting a payload.
- **Subscribe narrowly.** Only enable the events you actually consume.