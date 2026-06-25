# Source: https://tokensupply.in/docs/vendor-offers

## Vendor Offers

A **vendor offer** is a price + delivery-time mapping between one vendor and one product. They power two things:

- **PO auto-fill** — selecting a vendor + product on the create-PO page auto-fills the unit price from the matching offer.
- **Best-source visibility** — the Products list highlights the **Lowest Price** across all vendor offers per product so you can spot the cheapest source.

### Where to manage them

- **Per product** — open a product → **Vendor Offers** tab. Add, edit or remove offers; mark active/inactive.
- **Per vendor** — open a vendor → **Products / Offers** tab. Same data, scoped to the vendor.
- **Vendor portal** — invited vendors see and edit their own offers under **Products** in their constrained portal. They can only act on listings you've made open to offers.

### Fields

| Field | Notes |
| --- | --- |
| **Product** | Picked via the EntityPicker |
| **Price** | In the vendor's default currency |
| **Delivery Time** | Instant / Within 1 hour / Within 24 hours / Custom |
| **Status** | Active offers participate in PO auto-fill and Lowest Price calculations |

### Privacy

Vendors can see their own active offer per product but **cannot see competitor identities or exact competitor prices** — only relative signals (e.g. "your offer is the lowest" / "lower offers exist"). Offer history is preserved for auditing.