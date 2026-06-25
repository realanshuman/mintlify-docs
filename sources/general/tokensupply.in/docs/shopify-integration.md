# Source: https://tokensupply.in/docs/shopify-integration

## Shopify Integration

### Connecting Shopify

- Go to **Integrations → Shopify**
- Enter your **Shop Domain** and **Admin API access token**
- TokenSupply validates the credentials, lists your Shopify products and shows the connection status

### Mapping products

On a product's **Sales Channels** tab, map it to a Shopify variant. Per mapping you can set:

- **Status** — Active / Paused
- **Auto Deliver** — automatically deliver a key when an order is paid

You can also manage all mappings in bulk from **Sales Channel → Shopify**.

### Order flow

When a paid Shopify order arrives, TokenSupply reserves a key, fulfils the line item and emails the customer a tokenised delivery link to your customer portal.

### Tips

- Keep the Admin API token scoped to the minimum permissions needed
- Use **Auto Deliver** only for products with healthy stock to avoid backorders
- Reserved keys are released back to inventory if the upstream order is cancelled