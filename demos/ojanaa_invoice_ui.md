# Ojanaa Invoice Creation UI Demo

## Mobile App Interface (React Native / Expo)

This demo shows the invoice creation flow in the Ojanaa mobile app.

### Screen 1: New Invoice

```
┌─────────────────────────────────────┐
│  ←  New Invoice                     │
├─────────────────────────────────────┤
│                                     │
│  Customer                           │
│  ┌─────────────────────────────────┐│
│  │ Kwame Asante                    ││
│  │ +233 XX XXX XXXX                ││
│  └─────────────────────────────────┘│
│                                     │
│  Items                              │
│  ┌─────────────────────────────────┐│
│  │ Widget Pro            GHS 100.00││
│  │ Qty: 1                          ││
│  └─────────────────────────────────┘│
│  ┌─────────────────────────────────┐│
│  │ Installation Fee      GHS  50.00││
│  │ Qty: 1                          ││
│  └─────────────────────────────────┘│
│                                     │
│  [ + Add Item ]                     │
│                                     │
│  ─────────────────────────────────  │
│                                     │
│  Subtotal                 GHS 150.00│
│  Tax (0%)                 GHS   0.00│
│  ─────────────────────────────────  │
│  Total                    GHS 150.00│
│                                     │
│  ┌─────────────────────────────────┐│
│  │        Send via WhatsApp        ││
│  └─────────────────────────────────┘│
│                                     │
└─────────────────────────────────────┘
```

### Screen 2: Invoice Sent Confirmation

```
┌─────────────────────────────────────┐
│  ←  Invoice Details                 │
├─────────────────────────────────────┤
│                                     │
│            ✓                        │
│                                     │
│     Invoice Sent                    │
│                                     │
│  INV-DEMO-001                       │
│                                     │
│  To: Kwame Asante                   │
│  Amount: GHS 150.00                 │
│  Status: Delivered                  │
│                                     │
│  ─────────────────────────────────  │
│                                     │
│  Timeline                           │
│                                     │
│  ● Created      10:30 AM            │
│  ● Sent         10:30 AM            │
│  ● Delivered    10:31 AM            │
│  ○ Paid         Awaiting...         │
│  ○ Confirmed    --                  │
│                                     │
│  ┌─────────────────────────────────┐│
│  │         View in WhatsApp        ││
│  └─────────────────────────────────┘│
│                                     │
└─────────────────────────────────────┘
```

### Screen 3: Payment Received

```
┌─────────────────────────────────────┐
│  ←  Invoice Details                 │
├─────────────────────────────────────┤
│                                     │
│            💰                       │
│                                     │
│     Payment Received                │
│                                     │
│  INV-DEMO-001                       │
│                                     │
│  From: Kwame Asante                 │
│  Amount: GHS 150.00                 │
│  Status: Paid                       │
│                                     │
│  ─────────────────────────────────  │
│                                     │
│  Timeline                           │
│                                     │
│  ● Created      10:30 AM            │
│  ● Sent         10:30 AM            │
│  ● Delivered    10:31 AM            │
│  ● Paid         10:45 AM            │
│  ○ Confirmed    Awaiting...         │
│                                     │
│  ┌─────────────────────────────────┐│
│  │       Confirm & Send Receipt    ││
│  └─────────────────────────────────┘│
│                                     │
└─────────────────────────────────────┘
```

## Key UI/UX Elements

| Element | Purpose |
|---------|---------|
| Customer card | Quick view of recipient |
| Item list | Add/remove line items |
| Running total | Real-time calculation |
| Timeline | Visual progress indicator |
| Primary action button | Clear next step |

## Technologies

- React Native for cross-platform UI
- Expo for development tooling
- Supabase Realtime for live updates
- WhatsApp deep linking for send action

---

*All data shown is synthetic. See [Redaction Policy](../docs/REDACTION_POLICY.md).*
