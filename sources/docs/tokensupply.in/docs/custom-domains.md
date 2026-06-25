# Source: https://tokensupply.in/docs/custom-domains

## Custom Domains

### Adding a domain

- Go to **Settings → Domain → Add Domain**
- Enter your domain (e.g. `store.yourbrand.com`)
- Add the DNS records shown:

| Type | Name | Value |
| --- | --- | --- |
| **A** | @ | 185.158.133.1 |
| **A** | www | 185.158.133.1 |
| **TXT** | \_lovable | The verification value shown on the page |

- Click **Verify & Connect** — SSL is provisioned automatically once DNS is verified

### Statuses

- **Verifying** — waiting for DNS propagation
- **Active** — live and serving your storefront
- **Failed** — DNS check failed; review your records

DNS can take up to 72 hours to propagate; use \[DNSChecker.org\](https://dnschecker.org) to track it.