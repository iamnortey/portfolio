# Ojanaa System Architecture

## Overview

Ojanaa is a WhatsApp-native POS super-app built with a monorepo architecture. The system consists of a mobile app (Expo), web admin (Next.js), and a shared database layer (Supabase).

## System Diagram

```mermaid
flowchart TB
    subgraph Users["Users"]
        MER[Merchant]
        CUS[Customer]
    end

    subgraph Mobile["Mobile Layer"]
        APP[React Native App<br/>Expo]
    end

    subgraph Web["Web Layer"]
        ADMIN[Web Admin<br/>Next.js]
        API[API Routes<br/>Next.js App Router]
    end

    subgraph External["External Services"]
        WA[WhatsApp<br/>Business API]
        PAY[Payment<br/>Providers]
    end

    subgraph Data["Data Layer"]
        DB[(PostgreSQL<br/>Supabase)]
        RLS[Row-Level<br/>Security]
        RT[Realtime<br/>Subscriptions]
    end

    MER --> APP
    CUS --> WA

    APP --> API
    ADMIN --> API

    API --> DB
    API --> WA
    API --> PAY

    DB --> RLS
    DB --> RT
    RT -.-> APP

    WA --> API
    PAY --> API
```

## Component Details

### Mobile App (apps/app)
- **Technology:** React Native with Expo
- **Purpose:** Merchant interface for creating invoices, managing orders
- **Real-time:** Supabase Realtime for instant updates
- **Offline:** (Planned) Queue transactions when connectivity is poor

### Web Admin (apps/web)
- **Technology:** Next.js App Router
- **Purpose:** Dashboard for analytics, settings, admin functions
- **API Routes:** All backend logic lives in `apps/web/src/app/api/*`

### API Layer
- **Pattern:** Single backend surface (no separate API service)
- **Auth:** Supabase Auth with session validation
- **Webhooks:** Idempotent handlers for WhatsApp and payment providers

### Data Layer
- **Database:** PostgreSQL via Supabase
- **Security:** Row-Level Security (RLS) on all tables
- **Isolation:** Organization-scoped data access
- **Real-time:** Supabase Realtime for live updates

### External Integrations
- **WhatsApp Business API:** Invoice delivery, customer communication
- **Payment Providers:** Mobile Money, card payments

## Data Flow: Invoice Creation

```mermaid
sequenceDiagram
    participant M as Merchant
    participant APP as Mobile App
    participant API as API Routes
    participant DB as Database
    participant WA as WhatsApp

    M->>APP: Create invoice
    APP->>API: POST /api/invoices
    API->>DB: Insert invoice
    DB-->>API: Invoice created
    API->>WA: Send invoice message
    WA-->>API: Delivery confirmed
    API-->>APP: Success response
    APP-->>M: Invoice sent
```

## Security Architecture

```mermaid
flowchart LR
    subgraph Request["Incoming Request"]
        REQ[Request]
    end

    subgraph Auth["Authentication"]
        SESS[Session<br/>Validation]
        JWT[JWT<br/>Verification]
    end

    subgraph AuthZ["Authorization"]
        RLS[Row-Level<br/>Security]
        ORG[Organization<br/>Scope]
    end

    subgraph Data["Data Access"]
        DB[(Database)]
    end

    REQ --> SESS
    SESS --> JWT
    JWT --> RLS
    RLS --> ORG
    ORG --> DB
```

**Security layers:**
1. **Session validation:** Every request validates user session
2. **JWT verification:** Token integrity checked
3. **RLS policies:** Database enforces organization scope
4. **Organization isolation:** Users only access their org's data

## Key Architectural Decisions

| Decision | Rationale |
|----------|-----------|
| Single backend surface | Reduces operational complexity |
| Monorepo structure | Shared types, coordinated deployments |
| RLS by default | Defense in depth |
| Idempotent webhooks | Safe retries from external services |
| Real-time subscriptions | Instant updates without polling |

## Related Documents

- [Trust Loop Flow](./ojanaa-trust-loop.md)
- [ADR-001: Phase-Gated Development](../adrs/001-phase-gated-development.md)
- [ADR-002: Idempotent Webhooks](../adrs/002-idempotent-webhooks.md)
