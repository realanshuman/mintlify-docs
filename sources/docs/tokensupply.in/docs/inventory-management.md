# Source: https://tokensupply.in/docs/inventory-management

## Inventory & Key Management

### Adding inventory

From a product's **Inventory** tab you can:

- **Single key** — add one key inline with optional expiry and notes
- **Bulk upload** — paste or upload a CSV (one key per row)
- **From a Purchase Order** — vendor-uploaded stock files flow directly into inventory once the stock file is approved

### Duplicate prevention

A unique constraint on `ref_id` prevents the same key from being added twice. The bulk-entry UI also detects duplicates in real time before submission.

### Masked keys & the Reveal modal

Keys are always masked in lists. Click **Reveal** to open the **Key Reveal Modal**, which shows the full value briefly and logs the action. There is no inline copy-to-clipboard button — every reveal is auditable.

### Statuses

| Status | Meaning |
| --- | --- |
| **Available** | Ready for sale or delivery |
| **Reserved** | Held for a pending order |
| **Sold** | Delivered to a customer |
| **Invalid** | Marked non-functional |

### Replacements

Use **Replace Key** on a sold or invalid item to swap in a new key in place. The full replacement history is preserved on the inventory item.

### Activity log

Every action — add, reveal, copy, sell, replace, link to a ticket — is logged with actor, timestamp and metadata in the **Activity** dialog.