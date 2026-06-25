# Source: https://tokensupply.in/docs/invoices

## Invoices

### Creating an invoice

- Go to **Sales → Invoices → Create Invoice**
- Pick a customer and add line items
- Choose **Inclusive** or **Exclusive** tax — totals recalculate live
- Save as **Draft** or move to **Confirmed**

### Status rules

Once an invoice is **Confirmed**, it cannot be moved back to **Draft**. This protects financial records and the underlying PDF.

### PDF mappings

The invoice PDF uses your **Company Name**, **Legal Name**, GST/PAN, address and logo from **Settings → General**.

### Sending

Use **Send** to email the invoice to the customer. SMTP is preferred; Resend is the fallback when SMTP is not configured or fails.