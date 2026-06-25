# Source: https://tokensupply.in/docs/account-security

## Account & Security

### Personal settings

Open the user menu in the topbar (or go to **/account**) for the **Profile** and **Security** tabs. Update your name, avatar and email here.

### Two-factor authentication

Under **Security**, enable **TOTP** with any authenticator app (1Password, Authy, Google Authenticator). The issuer is registered as **tokensupply.in** so codes appear under a clear label. Once enabled, the AAL2 step runs at sign-in.

### Sessions & password recovery

Sign-out from any session terminates immediately. Password recovery uses a dedicated **/reset-password** route with MFA-aware bypass logic to avoid lockouts.

### Vendor portal sign-in

The vendor portal has its own sign-in page at `/s/{token_id}/vendor-portal` and does not allow self sign-up — vendors join via invite only. The same email can:

- Sign in to the vendor portal on multiple stores (one membership per store)
- Also own a TokenSupply store on the main platform without conflict

When a vendor with an existing account is invited to a new store and clicks the setup link, they are redirected to the sign-in page with their email pre-filled instead of being asked to create a new password.

### Account deletion

The **Delete Account** option is hidden for Vendors and team members on shared stores — only Super Admins of a store-owning account can delete the account.