# Source: https://tokensupply.in/docs/api-reference

## TokenSupply API

The TokenSupply REST API lets you read and write your store's data programmatically. All data is scoped to the store that owns the API key — a key can never read or write another store's data.

- **Base URL:** `https://iheiakmmrflybswwtknc.supabase.co/functions/v1/public-api`
- **Format:** JSON over HTTPS
- **Auth:** Bearer API key (created in **Settings → API**)

## Authentication

Create a key in **Settings → API**. The full key is shown **once** at creation time and looks like `ts_live_xxxxxxxxxxxx`. Store it securely — TokenSupply only keeps a SHA-256 hash and can never show it to you again.

Send it as a Bearer token on every request:

```
curl https://iheiakmmrflybswwtknc.supabase.co/functions/v1/public-api/orders \
  -H "Authorization: Bearer ts_live_xxxxxxxxxxxx"
```

Requests without a valid key return `401`. An expired key returns `401` with code `expired`; a revoked key returns `401`.

### Scopes

Each key carries a set of scopes. A request to an endpoint whose scope the key does not hold returns `403` with code `forbidden`.

| Scope | Grants |
| --- | --- |
| `read:orders` | GET /orders, GET /orders/{id} |
| `write:orders` | POST /orders |
| `read:inventory` | GET /inventory, GET /inventory/{id} |
| `write:inventory` | POST /inventory, PATCH /inventory/{id} |
| `read:products` | GET /products, GET /products/{id} |
| `write:products` | POST /products |
| `read:tickets` | GET /tickets, GET /tickets/{id} |
| `read:vendors` | GET /vendors, GET /vendors/{id} |
| `read:customers` | GET /customers, GET /customers/{id} |

## Conventions

### Pagination

List endpoints accept `limit` (default 50, max 100) and `offset` (default 0) query parameters and return a `pagination` object. Results are ordered by `created_at` descending.

```
{
  "data": [ ... ],
  "pagination": { "limit": 50, "offset": 0, "total": 128 }
}
```

Single-resource responses return just `{ "data": { ... } }`.

### Errors

Errors use standard HTTP status codes and a consistent body:

```
{ "error": { "message": "Missing required scope: write:orders", "code": "forbidden" } }
```

| Status | Code | Meaning |
| --- | --- | --- |
| 401 | unauthorized | Missing / malformed / invalid / revoked key |
| 401 | expired | Key past its expiry date |
| 403 | forbidden | Key lacks the required scope |
| 404 | not\_found | Resource or route does not exist |
| 422 | validation | Missing or invalid request fields |
| 400 | insert\_error / update\_error / query\_error | Database rejected the operation |
| 500 | internal | Unexpected server error |

## Endpoints

### Meta

`GET /` returns the store id the key is bound to, its scopes, and the available resources. Useful for verifying a key.

### Orders

```
GET  /orders          list
GET  /orders/{id}     retrieve one
POST /orders          create
```

**Returned fields:** `id, internal_order_id, marketplace, marketplace_order_id, status, payment_status, product_id, customer_id, inventory_item_id, quantity, amount, subtotal, currency, key_delivered, delivered_at, created_at, updated_at`

**Create** (scope `write:orders`) requires `product_id` (must belong to your store). Optional: `internal_order_id` (auto-generated if omitted), `marketplace`, `marketplace_order_id`, `customer_id`, `quantity`, `amount`, `currency`, `status`.

```
curl -X POST .../public-api/orders \
  -H "Authorization: Bearer ts_live_xxx" \
  -H "Content-Type: application/json" \
  -d '{ "product_id": "...", "quantity": 1, "amount": 9.99, "currency": "USD" }'
```

### Inventory

```
GET   /inventory        list
GET   /inventory/{id}   retrieve one
POST  /inventory        create
PATCH /inventory/{id}   update
```

**Returned fields:** `id, product_id, purchase_order_id, order_id, ref_id, value, status, expiry_date, notes, created_at`

The `value` (the fulfilment key/secret) **is** returned by the API because it is your own data. It is **never** sent over webhooks.

**Create** (scope `write:inventory`) requires `product_id` and `value`. Optional: `ref_id`, `purchase_order_id`, `expiry_date`, `status`, `notes`.

**Update** (scope `write:inventory`) accepts any of `status, value, expiry_date, ref_id, notes` — at least one field required.

### Products

```
GET  /products          list
GET  /products/{id}     retrieve one
POST /products          create
```

**Returned fields:** `id, name, sku, product_code, product_type, status, category, brand, description, image_url, created_at, updated_at`

**Create** (scope `write:products`) requires `name` and `sku` (unique within your store). Optional: `product_code`, `product_type`, `category`, `brand`, `description`, `status` (defaults to Enabled).

### Tickets

`GET /tickets` and `GET /tickets/{id}` (scope `read:tickets`). **Returned fields:** `id, ticket_code, title, description, issue_type, severity, status, order_id, product_id, seller_id, purchase_order_id, deadline_days, created_at, updated_at`

### Vendors

`GET /vendors` and `GET /vendors/{id}` (scope `read:vendors`). **Returned fields:** `id, name, email, phone, seller_type, account_type, status, country, currency, seller_code, created_at`. Bank, PAN and other sensitive details are intentionally excluded.

### Customers

`GET /customers` and `GET /customers/{id}` (scope `read:customers`). **Returned fields:** `id, first_name, last_name, email, phone, customer_type, country, currency, customer_code, created_at`

## Quick reference

| Method | Path | Scope |
| --- | --- | --- |
| GET | / | — |
| GET | /orders, /orders/{id} | read:orders |
| POST | /orders | write:orders |
| GET | /inventory, /inventory/{id} | read:inventory |
| POST | /inventory | write:inventory |
| PATCH | /inventory/{id} | write:inventory |
| GET | /products, /products/{id} | read:products |
| POST | /products | write:products |
| GET | /tickets, /tickets/{id} | read:tickets |
| GET | /vendors, /vendors/{id} | read:vendors |
| GET | /customers, /customers/{id} | read:customers |

See the **Webhooks** guide to receive real-time events.