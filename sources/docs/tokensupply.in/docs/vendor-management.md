# Source: https://tokensupply.in/docs/vendor-management

## Managing Vendors

Vendors live under **Purchases → Vendors** (`/vendors`). The list shows every vendor with status (Active / Inactive), country, currency, payment terms and total POs.

### Add a vendor

- Click **Add Vendor** (top right of the list)
- Fill in the form — the layout is grouped, not stepped:
- **Basic** — name, vendor type (**Individual** or **Business**), country, default currency, status
- **Contact** — primary email, phone, address. Add chat handles (Telegram, WhatsApp, Instagram) as needed
- **Catalogue** — what they supply (Gift Cards, Gaming/Software Keys, Subscriptions, Licenses, In-game Currency, DLCs, Other)
- **Commercial** — default **Payment Terms** (Net 7 / 15 / 30 / 45 / 60 / 90, Due on Receipt, COD, Advance)
- **Banking** — fields adapt to the vendor's country (IFSC for IN, Routing for US, Sort Code for UK, BSB for AU, IBAN/SWIFT for EU, etc.)

The vendor is saved with a sequential code (`SLR-001`, `SLR-002`…). This code is used as the prefix in every PO number.

### Vendor types & tax

- **Individual** vendors are treated as unregistered — POs to them carry **no tax**, and the PDF prints a "Tax Declaration" notice.
- **Business** vendors get automatic tax based on the vendor country vs your store country (see the Purchase Orders guide for the full matrix).

The badge on every vendor card and PO header shows **Individual** (blue) or **Business** (orange) at a glance.

### Detail page

Open any vendor to see the standard detail layout — breadcrumb, profile header, quick stats (total POs, total spend, open tickets) and tabs for **Overview**, **Purchase Orders**, **Products**, **Offers**, **Agreements**, **Tickets** and **Activity**.

### Invite to the vendor portal

From the vendor detail page, click **Invite to Portal**. TokenSupply emails the vendor a setup link — sent via your SMTP if configured, with Resend as an automatic fallback.

The card shows one of three states:

- **Pending Access** — invite sent, vendor has not signed up yet. You can **Resend invite** or **Revoke invite**.
- **Active** — vendor accepted and can sign in. You can **Revoke access** (uses the `revoke_vendor_membership` RPC to cleanly remove the membership without touching their account).
- **No portal access** — no invite is currently pending. Click **Invite to Portal** to start.

Revoking and re-inviting is safe — the new invite supersedes the old one and the UI updates to **Pending Access** immediately.

### Agreements

The **Agreements** tab lets you upload signed contracts (PDF/DOCX). Files live in a private storage bucket and are served via short-lived signed URLs — they never become permanently public.

### Editing & deleting

Use **Edit** in the header to update vendor details. Deleting a vendor is destructive: it requires you to type **DELETE**, and any linked POs, offers and transactions are unlinked (not cascaded).

See the **Vendor Portal** guide for the full vendor-side experience.