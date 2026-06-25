# Source: https://tokensupply.in/docs/smtp-email-setup

## Email & SMTP Setup

### Configuring SMTP

- Go to **Settings → Email Setup**
- Enter SMTP host, port, username, password, from-email and from-name
- Choose encryption (TLS / SSL / None)
- Click **Send Test Email** to verify

### Fallback

If SMTP is not configured or fails, TokenSupply falls back to Resend for critical transactional emails (vendor invites, delivery, notifications) so customers and vendors are never blocked.

### Tips

- Use app-specific passwords for Gmail / Workspace
- TLS on port **587** is the most reliable default
- Always send a test after changing credentials