# Source: https://tokensupply.in/docs/order-id-format

## Custom Order ID Format

### Where

Go to **Settings → General → Order ID Format**.

### Configuration

- **Prefix** — alphanumeric (e.g. `ORD`, `TS2026`)
- **Sequence** — fixed 5 digits, zero-padded (`00001` → `99999`)

The full format becomes `{PREFIX}-{00001}`. Sequences are scoped per store and never reuse a number.