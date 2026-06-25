# Source: https://tokensupply.in/docs/team-management

## Team Management

### Tabs

The **Team** page has four tabs:

- **Members** — staff with roles
- **Vendors** — linked vendor accounts
- **Invites** — pending invitations (Admin only)
- **Activity** — administrative event audit log (Admin only)

### Inviting

Click **Invite Member**, enter an email and pick a role (Admin or Support). Only **Super Admins** and **Admins** can send invites.

Vendor invites are **not sent from this page** — they go through the dedicated **Invite to Portal** action on the vendor detail page, which creates a `vendor_memberships` row instead of a staff account. See the **Vendor Portal** guide for the full flow.

### Permissions

| Role | Where they sign in | Team | Products | Analytics | Billing |
| --- | --- | --- | --- | --- | --- |
| Super Admin | Main platform | ✅ | ✅ | ✅ | ✅ |
| Admin | Main platform | ✅ | ✅ | ✅ | ✅ |
| Support | Main platform | ❌ | ✅ | ❌ | ❌ |
| Vendor | `/s/{token_id}/vendor-portal` | ❌ | Own offers + store catalog | Own only | ❌ |

### Activity log

Database triggers capture role changes, invites, removals and other administrative events for full audit traceability. Vendor-join and staff-join events emit distinct notifications.