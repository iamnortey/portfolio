# Ojanaa WhatsApp Trust Loop Demo

## Conversation Flow

This demo shows the WhatsApp conversation between a merchant and customer during the Trust Loop.

### Customer View: Invoice Received

```
┌─────────────────────────────────────┐
│  ← Accra Demo Store                 │
│     Business Account                │
├─────────────────────────────────────┤
│                                     │
│  ┌─────────────────────────────────┐│
│  │                                 ││
│  │  📄 INVOICE                     ││
│  │                                 ││
│  │  Accra Demo Store               ││
│  │  Invoice #INV-DEMO-001          ││
│  │                                 ││
│  │  ─────────────────────────────  ││
│  │                                 ││
│  │  Items:                         ││
│  │  • Widget Pro        GHS 100.00 ││
│  │  • Installation Fee  GHS  50.00 ││
│  │                                 ││
│  │  ─────────────────────────────  ││
│  │  Total:              GHS 150.00 ││
│  │                                 ││
│  │  ─────────────────────────────  ││
│  │                                 ││
│  │  [Pay Now]  [View Details]      ││
│  │                                 ││
│  └─────────────────────────────────┘│
│                               10:31 │
│                                     │
│  ─────────────────────────────────  │
│                                     │
│  Type a message...            📎 🎤 │
└─────────────────────────────────────┘
```

### Customer View: After Payment

```
┌─────────────────────────────────────┐
│  ← Accra Demo Store                 │
│     Business Account                │
├─────────────────────────────────────┤
│                                     │
│  [Previous invoice message...]      │
│                               10:31 │
│                                     │
│  ─────────────────────────────────  │
│                                     │
│  ┌─────────────────────────────────┐│
│  │                                 ││
│  │  ✅ PAYMENT CONFIRMED           ││
│  │                                 ││
│  │  Thank you for your payment!    ││
│  │                                 ││
│  │  Invoice: #INV-DEMO-001         ││
│  │  Amount:  GHS 150.00            ││
│  │  Ref:     PAY-DEMO-001          ││
│  │                                 ││
│  │  Your receipt will be sent      ││
│  │  shortly after merchant         ││
│  │  confirmation.                  ││
│  │                                 ││
│  └─────────────────────────────────┘│
│                               10:45 │
│                                     │
└─────────────────────────────────────┘
```

### Customer View: Receipt Received

```
┌─────────────────────────────────────┐
│  ← Accra Demo Store                 │
│     Business Account                │
├─────────────────────────────────────┤
│                                     │
│  [Previous messages...]             │
│                                     │
│  ─────────────────────────────────  │
│                                     │
│  ┌─────────────────────────────────┐│
│  │                                 ││
│  │  🧾 RECEIPT                     ││
│  │                                 ││
│  │  Accra Demo Store               ││
│  │  Receipt #REC-DEMO-001          ││
│  │                                 ││
│  │  ─────────────────────────────  ││
│  │                                 ││
│  │  Date: Jan 10, 2026             ││
│  │  Invoice: #INV-DEMO-001         ││
│  │                                 ││
│  │  Items:                         ││
│  │  • Widget Pro        GHS 100.00 ││
│  │  • Installation Fee  GHS  50.00 ││
│  │                                 ││
│  │  ─────────────────────────────  ││
│  │  Total Paid:         GHS 150.00 ││
│  │  Payment Ref:        PAY-DEMO-001│
│  │                                 ││
│  │  ─────────────────────────────  ││
│  │                                 ││
│  │  Thank you for your business!   ││
│  │                                 ││
│  │  [Download PDF]                 ││
│  │                                 ││
│  └─────────────────────────────────┘│
│                               10:50 │
│                                     │
└─────────────────────────────────────┘
```

## Trust Loop State Transitions

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│   INVOICE    │────▶│    PAID      │────▶│  CONFIRMED   │
│    SENT      │     │              │     │              │
└──────────────┘     └──────────────┘     └──────────────┘
       │                    │                    │
       ▼                    ▼                    ▼
   Customer             Customer              Both get
   receives             pays via              receipt
   invoice              MoMo/card             (proof)
```

## Evidence Created

| Event | Evidence |
|-------|----------|
| Invoice sent | WhatsApp message ID, timestamp |
| Invoice delivered | WhatsApp delivery receipt |
| Payment received | Payment provider confirmation, reference |
| Receipt sent | WhatsApp message ID, PDF link |

## Message Templates Used

1. **Invoice template:** Structured message with items and payment CTA
2. **Payment confirmation:** Status update with reference
3. **Receipt template:** Complete transaction record

---

*All data shown is synthetic. See [Redaction Policy](../docs/REDACTION_POLICY.md).*
