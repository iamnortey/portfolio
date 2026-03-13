# Isaac Nortey — Engineering Portfolio

> Case studies, architecture, decision records, and operational artifacts from production systems.

[![GitHub](https://img.shields.io/badge/GitHub-iamnortey-black?style=flat&logo=github)](https://github.com/iamnortey)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-inortey-blue?style=flat&logo=linkedin)](https://linkedin.com/in/inortey/)
[![Website](https://img.shields.io/badge/Website-inortey.com-black?style=flat)](https://inortey.com)

---

## Featured Projects

| Project | Description | Stack | Links |
|---------|-------------|-------|-------|
| **Ojanaa** | WhatsApp-native POS super-app with invoice trust loop | TypeScript, React Native, Next.js, Supabase | [Case Study](./case-studies/ojanaa.md) · [Docs](https://github.com/iamnortey/ojanaa-docs) |
| **Ninolex** | Pronunciation infrastructure for AI voice applications | TypeScript, Python, Next.js, Modal | [Case Study](./case-studies/ninolex.md) · [Docs](https://github.com/iamnortey/ninolex-docs) |
| **Ninobyte** | Enterprise tooling for Claude agent ecosystems | Python, Claude Skills, MCP | [Case Study](./case-studies/ninobyte.md) · [Docs](https://github.com/iamnortey/ninobyte-docs) |
| **Ninolex-GH** | Open Ghanaian pronunciation dictionary | Python, W3C PLS | [Repo](https://github.com/iamnortey/ninolex-gh) |
| **Prepnest** | Educational content platform for exam preparation | React Native, Sanity CMS, Manim | [Case Study](./case-studies/prepnest.md) · [Docs](https://github.com/iamnortey/prepnest-docs) |

---

## Engineering Principles

### Phase-Gated Development
No Phase 2 features until Phase 1 passes all quality gates. Every phase has explicit acceptance criteria. Scope creep is prevented by design.

### Data-First Thinking
Get the schema and domain model right before building features. The data model is the foundation everything else builds on.

### Validation-First
Every claim traces back to evidence. Skills are validated against official documentation. Decisions are logged in ADRs.

### Operational Clarity
Runbooks, decision logs, and audit trails are first-class citizens — not afterthoughts. Systems are designed to be observable, debuggable, and maintainable.

---

## Technical Stack

| Layer | Technologies |
|-------|-------------|
| **Languages** | TypeScript, Python, SQL (PostgreSQL / PLpgSQL) |
| **Frontend** | React, Next.js, React Native, Expo |
| **Backend** | Node.js, Next.js API Routes, Modal (serverless) |
| **Data** | PostgreSQL, Supabase, Typesense |
| **AI / Voice** | Claude, ElevenLabs, Vapi, CMUdict |
| **Infrastructure** | GitHub Actions, Supabase, Modal |

---

## Role Alignment

Evidence mapped to specific engineering roles:

- [Platform Engineering](./roles/platform-engineering.md)
- [SRE / Reliability Engineering](./roles/sre-reliability.md)
- [Data Infrastructure](./roles/data-infrastructure.md)
- [Security Engineering](./roles/security-corporate.md)
- [Full-Stack / Product Engineering](./roles/fullstack-product.md)
- [Technical Support Engineering](./roles/technical-support-engineering.md)

---

## Architecture Samples

- [Ojanaa System Architecture](./architecture/ojanaa-system.md)
- [Invoice Trust Loop Flow](./architecture/ojanaa-trust-loop.md)
- [Ninolex Pronunciation Pipeline](./architecture/ninolex-pipeline.md)

---

## Decision Records

Sample ADRs demonstrating technical decision-making:

- [ADR-001: Phase-Gated Development](./adrs/001-phase-gated-development.md)
- [ADR-002: Idempotent Webhook Handlers](./adrs/002-idempotent-webhooks.md)
- [ADR-003: API-First Surface Design](./adrs/003-api-first-surface.md)

---

## Operational Artifacts

- [Incident Response Runbook](./runbooks/incident-response.md)
- [Daily Workflow Runbook](./runbooks/daily-workflow.md)

---

*Core implementations remain in private repositories. This portfolio showcases architecture, decisions, and operational artifacts.*
