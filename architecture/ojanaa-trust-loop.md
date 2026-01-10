# Ojanaa Invoice Trust Loop

## Overview

The Trust Loop is the core flow of Ojanaa: a verifiable transaction cycle that creates mutual proof between merchant and customer.

## The Trust Problem

In informal commerce:
- Customers dispute payments they actually made
- Merchants claim deliveries they didn't make
- Neither party has proof
- Trust is low, transactions are risky

## The Solution: Trust Protocol

```mermaid
flowchart LR
    subgraph Merchant
        M1[Create Invoice]
        M4[Confirm Receipt]
    end

    subgraph System
        S1[Store Invoice]
        S2[Deliver via WA]
        S3[Process Payment]
        S4[Generate Receipt]
    end

    subgraph Customer
        C1[Receive Invoice]
        C2[Make Payment]
        C3[Receive Receipt]
    end

    M1 --> S1
    S1 --> S2
    S2 --> C1
    C1 --> C2
    C2 --> S3
    S3 --> M4
    M4 --> S4
    S4 --> C3
```

## Detailed Flow

### Phase 1: Invoice Creation

```mermaid
sequenceDiagram
    participant M as Merchant
    participant APP as Mobile App
    participant API as API
    participant DB as Database

    M->>APP: Enter invoice details
    Note over M,APP: Customer, items, amounts
    APP->>API: POST /api/invoices
    API->>API: Validate input
    API->>DB: Create invoice record
    DB-->>API: Invoice ID
    API-->>APP: Invoice created
    APP-->>M: Ready to send
```

### Phase 2: Invoice Delivery

```mermaid
sequenceDiagram
    participant M as Merchant
    participant API as API
    participant WA as WhatsApp
    participant C as Customer

    M->>API: Send invoice
    API->>WA: Send message template
    Note over API,WA: Invoice details + payment link
    WA-->>API: Message ID
    API->>API: Update: status=sent
    WA->>C: Invoice message
    C-->>WA: Read receipt
    WA-->>API: Delivery webhook
    API->>API: Update: status=delivered
```

### Phase 3: Payment

```mermaid
sequenceDiagram
    participant C as Customer
    participant WA as WhatsApp
    participant PAY as Payment Provider
    participant API as API
    participant DB as Database

    C->>WA: Click payment link
    WA->>PAY: Redirect to payment
    C->>PAY: Complete payment
    PAY->>API: Payment webhook
    Note over API: Idempotency check
    API->>DB: Update: status=paid
    API-->>PAY: Acknowledge webhook
```

### Phase 4: Confirmation & Receipt

```mermaid
sequenceDiagram
    participant M as Merchant
    participant APP as Mobile App
    participant API as API
    participant WA as WhatsApp
    participant C as Customer

    APP-->>M: Payment notification
    M->>APP: Confirm receipt
    APP->>API: POST /api/invoices/{id}/confirm
    API->>API: Generate receipt
    API->>WA: Send receipt to customer
    WA->>C: Receipt message
    API->>WA: Send confirmation to merchant
    WA->>M: Confirmation message
```

## State Machine

```mermaid
stateDiagram-v2
    [*] --> Draft: Create
    Draft --> Sent: Send via WhatsApp
    Sent --> Delivered: Delivery confirmed
    Delivered --> Paid: Payment received
    Paid --> Confirmed: Merchant confirms
    Confirmed --> [*]: Complete

    Sent --> Failed: Delivery failed
    Paid --> Disputed: Customer disputes
    Failed --> Sent: Retry
    Disputed --> Resolved: Resolution
```

## Trust Evidence

Each state transition creates evidence:

| State | Evidence Created |
|-------|------------------|
| Draft → Sent | Timestamp, WA message ID |
| Sent → Delivered | Delivery receipt from WA |
| Delivered → Paid | Payment provider confirmation |
| Paid → Confirmed | Merchant confirmation timestamp |
| Confirmed → Complete | Receipt sent, mutual acknowledgment |

## Why This Works

1. **Third-party timestamps:** WhatsApp and payment providers provide independent proof
2. **Immutable records:** State transitions are logged, not overwritten
3. **Mutual receipts:** Both parties receive proof at each step
4. **Dispute resolution:** Clear evidence chain for any disputes

## Related Documents

- [System Architecture](./ojanaa-system.md)
- [Ojanaa Case Study](../case-studies/ojanaa.md)
- [ADR-002: Idempotent Webhooks](../adrs/002-idempotent-webhooks.md)
