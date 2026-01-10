# Data Infrastructure Role Alignment

## What I've Built That Maps to This Role

- **Ninolex Core:** Data pipeline for pronunciation resolution—ingest, transform, store, export
- **650K+ lines of PLpgSQL:** Database procedures, functions, and complex queries
- **Vertical pack architecture:** Domain-specific data structures (AutoLex, DineLex)
- **Multi-format export:** ElevenLabs, AWS Polly, Vapi dictionary generation

## Relevant Artifacts

### Case Studies
- [Ninolex Case Study](../case-studies/ninolex.md) — Data pipeline design
- [Ojanaa Case Study](../case-studies/ojanaa.md) — Transaction data modeling

### Architecture
- [Ninolex Pipeline](../architecture/ninolex-pipeline.md) — Resolution pipeline

### ADRs
- [ADR-003: API-First Surface](../adrs/003-api-first-surface.md) — Data API design

## Operating Model

### How I Think About Data Systems

1. **Schema-first:** Get the data model right before building anything else
2. **Normalization with purpose:** Normalize for integrity, denormalize for performance
3. **Idempotency:** Data operations should be retry-safe
4. **Auditability:** Track what changed, when, and why

### Data Pipeline Principles

```
Source → Ingest → Transform → Store → Serve → Export
   ↓        ↓         ↓          ↓       ↓        ↓
 Raw     Validate   Normalize  Index   API    Formats
 data    + clean    + enrich   + cache
```

**Key considerations:**
- **Data quality:** Validate early, fail fast
- **Idempotent ingestion:** Safe to re-run
- **Incremental processing:** Don't reprocess everything
- **Schema evolution:** Handle changes gracefully

### SQL Philosophy

- **RLS by default:** Row-Level Security for data isolation
- **Stored procedures for complex logic:** Keep business rules in the database
- **Indexes with intent:** Know why each index exists
- **Query analysis:** Understand explain plans

## Key Skills Demonstrated

| Skill | Evidence |
|-------|----------|
| SQL/PostgreSQL | 650K+ lines PLpgSQL |
| Data Modeling | Ninolex entity registry, Ojanaa invoice schema |
| Pipeline Design | Two-tier resolution, multi-format export |
| API Design | `/api/v1/resolve` data endpoint |
| Data Quality | Validation patterns, confidence scoring |

## ClickHouse-Specific Relevance

While my primary database experience is PostgreSQL/Supabase, the patterns translate:

| PostgreSQL Pattern | ClickHouse Equivalent |
|-------------------|----------------------|
| RLS policies | Row-level access controls |
| Materialized views | Materialized views |
| Stored procedures | User-defined functions |
| JSONB for semi-structured | Nested data types |
| Partition pruning | Partition pruning |

**What I'd bring to ClickHouse:**
- Strong SQL fundamentals
- Data pipeline thinking
- API-first approach to data access
- Schema evolution experience
- Query optimization mindset
