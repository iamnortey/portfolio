# Demo Assets

This directory contains demo screenshots and visualizations using **synthetic data only**.

All demos follow the [Redaction Policy](../docs/REDACTION_POLICY.md):
- No real customer names, emails, or phone numbers
- No real invoice IDs or transaction amounts
- No internal URLs or API endpoints
- Synthetic data patterns used throughout

## Available Demos

### Ojanaa

| Demo | Description |
|------|-------------|
| [ojanaa_invoice_ui.md](./ojanaa_invoice_ui.md) | Mobile invoice creation interface |
| [ojanaa_whatsapp_flow.md](./ojanaa_whatsapp_flow.md) | WhatsApp trust loop conversation |

### Ninolex

| Demo | Description |
|------|-------------|
| [ninolex_generator_ui.md](./ninolex_generator_ui.md) | Dictionary generator interface |
| [ninolex_api_response.md](./ninolex_api_response.md) | API response example |

## Synthetic Data Used

All demos use these synthetic patterns:

```
Customer: Kwame Asante, Ama Mensah
Phone: +233 XX XXX XXXX
Email: demo@example.com
Organization: Accra Demo Store
Invoice ID: INV-DEMO-001
Amount: GHS 150.00
```

## Generating Real Screenshots

To create actual screenshot demos:

1. Set up a demo/sandbox environment
2. Populate with synthetic data
3. Capture screenshots
4. Verify redaction checklist passes
5. Export and add to this directory

See [Publishing Checklist](../docs/PUBLISHING_CHECKLIST.md) for verification steps.
