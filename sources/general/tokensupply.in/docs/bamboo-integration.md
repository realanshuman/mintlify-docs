# Source: https://tokensupply.in/docs/bamboo-integration

## Bamboo Card Distributor Sourcing

Bamboo Card is a **distributor source** — you procure stock from them instead of (or in addition to) listing on a marketplace.

### Setting up

- Go to **Integrations → Bamboo Card**
- Provide the API credentials supplied by your Bamboo Card account manager
- Share TokenSupply's egress IP for **IP whitelisting** on Bamboo's side
- Once whitelisted, the catalog browser unlocks

### Sourcing flow

- Browse the Bamboo catalog from the integration page
- Convert any catalog item into a **Purchase Order** against a "Bamboo Card" vendor record
- Delivered keys flow into your inventory the same way as any other PO

### Notes

- Bamboo is a procurement source, not a sales channel — it does not appear under **Sales Channel**
- Credentials are stored encrypted and never returned by the API or webhooks