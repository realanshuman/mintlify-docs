# Source: https://tokensupply.in/trust

Trust · Security & Privacy

# Trust, Security & Privacy

A plain-English summary of the security, privacy, and operational controls available today across the TokenSupply platform.

Document Info

EFFECTIVE

June 17, 2026

VERSION

1.0

JURISDICTION

India

Print / Save PDF

§ 01

## Overview

This page is maintained by GENFLIX COMMERCE PRIVATE LIMITED to answer common security and privacy questions about the TokenSupply platform. It describes the in-product controls and operational practices currently enabled for customers of the Service.

This page is informational and does not constitute an independent certification, audit attestation, or warranty. For contractual commitments, please refer to our Terms of Service, Privacy Policy, and any data processing addendum signed with your organization.

NoteShared responsibility — TokenSupply is responsible for platform security, infrastructure controls, and the integrity of the hosted application. Store Owners are responsible for managing their own users, configuring access, protecting credentials, and meeting their own regulatory obligations for the data they upload.

§ 02

## Authentication & Access Control

Access to TokenSupply requires an email and password, with optional Google sign-in. Anonymous sign-up is disabled.

- Two-factor authentication (TOTP) is available for every account; admins can enable it from Account → Security.
- Password reset flows require email ownership and invalidate existing sessions on completion.
- Sessions are validated on every request and expire when refresh tokens are revoked.
- Role-based access is enforced through a dedicated user-roles model (superadmin, admin, support, vendor) rather than client-side flags.

§ 03

## Data Isolation & Tenancy

TokenSupply is multi-tenant. Each Store is scoped by a unique store identifier, and every customer-facing table enforces row-level access policies tied to that identifier.

- Row-level security policies restrict reads and writes to the user's own store.
- Privileged operations that need to bypass row-level security run inside controlled, security-definer database functions with explicit input validation.
- Vendor accounts see a restricted view of the application limited to the listings, offers, and tickets they are assigned to.

§ 04

## Encryption in Transit & at Rest

All traffic to tokensupply.in and the API is served over HTTPS using TLS. Inventory keys are masked in the application UI and revealed only through audited reveal flows; reveal and copy actions are logged to the inventory activity log.

The database, object storage, and backups are managed on Lovable Cloud infrastructure with encryption at rest provided by the underlying platform.

NoteWe do not claim end-to-end encryption. Authorized personnel and platform operators can access data when required to operate the Service or respond to lawful requests.

§ 05

## What We Collect & How We Use It

We collect only the information needed to operate the Service: account profile data, store configuration, operational records (products, inventory, customers, vendors, orders, tickets, messages), billing history, and standard request metadata used for diagnostics and abuse prevention.

Detailed categories, controller and processor responsibilities, retention periods, and user rights are described in the Privacy Policy.

- Inventory keys are stored masked and revealed only on demand to authorized roles.
- Card details are processed by our payment processor and are never stored on TokenSupply servers.
- Customer-portal links are tokenized; refunded orders auto-revoke delivery tokens.

§ 06

## Subprocessors & Integrations

TokenSupply relies on a small set of vetted subprocessors to run the Service. The active marketplace and operational integrations available in-product include:

- Lovable Cloud — application hosting, database, authentication, storage, and edge functions.
- Marketplace connectors — G2A, Eneba, Driffle, Kinguin, Gamivo, Hood, Shopify, WooCommerce, and similar channels enabled per Store.
- Distributor sourcing — Bamboo Card (IP-allowlisted).
- Payments — Razorpay, Stripe, PayPal, and Paddle for billing and checkout flows.
- Email delivery — Store-configured SMTP with Resend as a managed fallback.

The exact set of active integrations for a Store is visible in Settings → Integrations. Enabling an integration shares the data needed for that workflow with the corresponding provider.

§ 07

## Retention & Deletion

Operational records remain available while a Store is active so that orders, invoices, tickets, and audit trails stay intact for the people who need them.

- Destructive actions (such as deleting a vendor or a store) require typing 'DELETE' to confirm and unlink dependent transactions where applicable.
- Account deletion is performed by support on request from a verified Store Owner; vendor users cannot self-delete the workspace they belong to.
- Backups are retained on the underlying Lovable Cloud platform and rotated on the platform's standard schedule.

§ 08

## Audit Logging & Activity Trails

Sensitive actions are logged so that Store Owners can review them later:

- Team activity log — invites, role changes, and administrative events.
- Inventory activity log — key reveal, copy, replacement, and bulk operations.
- Order, purchase order, and ticket timelines — state transitions and message history with author attribution.
- Marketplace activity logs — sync runs and connector-specific events per integration.

§ 09

## Incident Response & Status

Operational status and known incidents are published at /status. If you believe you are experiencing a security incident affecting your Store, contact us immediately at security@tokensupply.in so we can investigate.

We will notify affected Store Owners of confirmed incidents materially affecting their data via email and in-product notifications, in accordance with applicable law and our agreements.

§ 10

## Reporting a Vulnerability

We welcome reports from security researchers. Please email security@tokensupply.in with reproduction steps and a way for us to contact you. Do not test against other customers' data, perform denial-of-service testing, or access data that is not your own.

We will acknowledge confirmed reports and work with you on remediation timelines. We do not currently operate a paid bug-bounty program.

§ 11

## Compliance Posture

TokenSupply is operated from India by GENFLIX COMMERCE PRIVATE LIMITED. We process data in line with our Privacy Policy and applicable Indian law, and we honor data-subject requests described there.

ImportantTokenSupply does not currently advertise SOC 2, ISO 27001, PCI-DSS, HIPAA, or GDPR adequacy certifications. If your procurement process requires specific contractual commitments, contact legal@tokensupply.in.

§ 12

## Contact

Security issues — security@tokensupply.in

Privacy requests — privacy@tokensupply.in

Legal and contracts — legal@tokensupply.in

General support — through the Help Centre in your TokenSupply workspace.

— End of document —

TRUST-1.0 · June 17, 2026

[Read Privacy Policy](https://tokensupply.in/privacy) [Contact legal team](mailto:legal@tokensupply.in)