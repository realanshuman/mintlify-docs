# Source: https://tokensupply.in/docs/creating-orders

## Creating Manual Orders

Manual orders cover sales outside connected sales channels — direct customers, B2B deals, replacements, gifting.

### Flow

- Go to **Orders → Create Order**
- Pick a customer (or create one inline)
- Select a product, quantity and unit price; concatenated keys are supported
- The order auto-completes when the customer reveals the key in the portal
- A customer portal link is generated automatically and can be re-sent at any time

### Order statuses

| Status | Meaning |
| --- | --- |
| **Pending** | Created, awaiting delivery |
| **Completed** | Customer revealed the key |
| **Failed** | Delivery error |
| **Refunded** | Refunded — keys auto-revoked |

### List view

`Transactions → All Transactions` shows the full ledger across channels. The **Key** column has been removed in favour of platform-source filters and Order ID search.

### Detail view

The transaction detail page shows the platform source (Manual, Shopify, G2A, …), the most recent delivery token and a delivery timeline. Refunds automatically revoke any active customer portal links and may return keys to inventory.