# Source: https://tokensupply.in/docs/vendor-portal

## Vendor Portal

The Vendor Portal is a separate, per-store workspace for your external suppliers. It sits **on top of each store's URL** so vendors always know which store they're working in.

### URLs

| Page | URL |
| --- | --- |
| Auth | `tokensupply.in/s/{token_id}/vendor-portal` |
| Setup (from invite email) | `tokensupply.in/s/{token_id}/vendor-portal/setup?token=...` |
| Portal home | `tokensupply.in/s/{token_id}/vendor-portal` once signed in |

`{token_id}` is the same store slug used by the public store page. The portal works even before the public store page is published — vendors can be onboarded immediately.

### Multi-store memberships

Vendor accounts are stored in a dedicated `vendor_memberships` table, not on the user's profile. That means:

- **One email can be a vendor on many stores.** Signing in on `/s/genflix/vendor-portal` and `/s/another/vendor-portal` uses the same login, but each portal scopes data to that store only.
- The same email can **also own a TokenSupply store** on the main platform without conflict — the link on the auth page reads "Need your own TokenSupply store? Go to main platform →".

### Invite flow

- Store admin clicks **Invite to Portal** on the vendor detail page
- Vendor receives an email with a setup link
- Setup page asks them to **create a password** for their email
- If the email is already registered (e.g. they are a vendor on another store), setup redirects them to the sign-in page with their email pre-filled — no duplicate account is created
- After signing in, the membership auto-accepts and they land in the portal

### What vendors see

The portal reuses the standard app layout but with a vendor-scoped sidebar:

- **Dashboard** — their KPIs for this store
- **Products** — the store catalog + **Create Offer** for any product they're allowed to bid on
- **Purchase Orders** — only POs assigned to them, with full detail pages, breadcrumb links, **Invoice PDF** download and notes/attachments
- **Inventory** — per-product inventory upload for their POs, with masked keys and the standard reveal modal
- **Tickets** — only tickets that involve them, with the same conversation module (admin/support names visible, role badges, attachments)
- **Messages** — threads they participate in
- **Analytics** — 6-month trend lines and KPIs scoped to their activity
- **Account** — personal profile and security (no Billing, no Team, no Integrations)

Links inside the portal are automatically prefixed with the portal base path via the `use-workspace-path` hook, so detail pages, breadcrumbs and back buttons all stay inside `/s/{token_id}/vendor-portal/...`.

### Auth page

Sign-up is **not** available on the vendor portal — vendors can only join via invite. The auth page mirrors the main platform's styling (white background, dark primary button) and shows a generic "Vendor Portal" pill rather than the store name.

### Security

- Read access to store, product, PO, ticket, inventory and storage objects is granted via RLS policies that check `vendor_memberships` for the current user + store
- Vendors never see other vendors' offers, prices, POs or tickets
- The store's master **Billing** page is explicitly blocked inside the vendor portal route tree