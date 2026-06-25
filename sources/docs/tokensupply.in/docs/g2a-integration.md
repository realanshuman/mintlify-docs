# Source: https://tokensupply.in/docs/g2a-integration

## G2A Sales Channel Integration

### Setting up

- Go to **Integrations → G2A**
- Enter your **Client ID**, **Client Secret**, **API URL** and **Token URL**
- Save and accept the G2A contract terms

### Product search

Use **Search G2A Products** on the integration page or from an offer's product picker. The modal:

- Loads an initial **50-per-page** list with pagination
- Switches to **live API search** the moment you type — every keystroke fetches matching products directly from G2A's full catalog, not just a cached subset
- Caches recent results in-memory so repeat searches are instant
- Shows live fetch status (Searching… / Cached / Error)

### Listings

From the integration detail page you can:

- Map internal products to G2A offers
- Set retail and business prices, declared stock and delivery time
- Toggle **Active** and **Auto Deliver** per listing
- View competing dropshipping offers from other G2A sellers

### Auto sync

Enable **Auto Sync** and choose an interval — syncs run automatically through `pg_cron`. Manual sync buttons have been removed in favour of scheduled, deterministic syncs.

### Checkout contract (Import API)

TokenSupply exposes the G2A Import API at the `g2a-contract` edge function. The contract endpoints follow G2A's documented shape strictly:

- `POST /reservation` returns only `reservation_id` and the `stock` array (no extra fields, which previously caused G2A's checkout to reject reservations)
- `PUT /reservation/{id}` extends a reservation
- `DELETE /reservation/{id}` releases it
- Price and currency are derived from G2A's `additional_data` to avoid a slow live lookup on every reservation

If a buyer ever sees "cart updated / out of stock" during checkout, it usually means the reservation endpoint returned an unexpected field — the strict-contract response prevents that.

### Rate limits

G2A enforces request limits — bursts can return **ERR429**. Sync intervals are tuned to stay within the published quotas.