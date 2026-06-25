# Source: https://tokensupply.in/docs/customer-portal

## Customer Delivery Portal

Each order generates a unique, tokenised customer portal URL of the form `/s/{token_id}/order/{orderToken}`. Customers see:

- Your store branding (logo, colours)
- A list of delivered keys with status badges
- A **Reveal** action that unmasks the key and marks the order complete
- Download buttons for any attached files

### Refunds

When you mark an order as refunded, all associated customer portal links are auto-revoked and any unrevealed keys are returned to inventory.

### Re-sending

Use **Re-send delivery** on the transaction detail page to email the customer the portal link again. A new delivery token is generated each time so old links can be safely invalidated.