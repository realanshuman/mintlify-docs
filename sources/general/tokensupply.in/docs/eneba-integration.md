# Source: https://tokensupply.in/docs/eneba-integration

## Eneba Sales Channel Integration

Eneba uses a **GraphQL Seller API** with OAuth (`api_consumer` grant). TokenSupply supports both **sandbox** and **production** environments.

### Setting up

- Go to **Integrations → Eneba**
- Pick **Sandbox** or **Production**
- Enter your **Client ID** and **Client Secret**
- Allowlist TokenSupply's egress IP in Eneba's dashboard — requests are proxied through a stable IP so allowlisting works reliably
- Save and complete the OAuth handshake — tokens are stored encrypted and refreshed automatically

### Listings & auto-fulfil

Manage Eneba listings under **Sales Channel → Eneba**:

- Toggle **Active** and **Auto Deliver** per listing
- When **Auto Deliver** is on, a paid Eneba order reserves a key, fulfils the line item and delivers it back to Eneba through the GraphQL API
- A scheduled sync cron pulls order updates and reconciles status

### Activity log

The **Activity** tab on the integration page records every sync run, fulfilment attempt and API error — useful for debugging IP allowlist or token issues.