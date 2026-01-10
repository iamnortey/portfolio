# ADR-003: API-First Surface Design

**Status:** Accepted
**Date:** 2025-12-15
**Context:** Ninolex Core architecture

---

## Context

Ninolex provides pronunciation resolution for external integrations:
- Voice AI applications
- TTS pipeline preprocessors
- Customer-facing voice agents

External consumers need:
- Stable endpoints that don't change
- Predictable response formats
- Clear versioning for breaking changes
- Good documentation

---

## Decision

**Design API-first:** Define the API contract before implementation, version from day one.

Principles:
1. **Versioned endpoints:** `/api/v1/resolve`, not `/api/resolve`
2. **Stable contracts:** Response shape documented and frozen per version
3. **Breaking changes = new version:** Never change existing version behavior
4. **Deprecation policy:** Minimum 6 months notice before removing a version

---

## Consequences

### Positive
- External integrations can rely on stability
- Clear upgrade path for consumers
- Forces thoughtful API design upfront

### Negative
- More upfront design work
- Must maintain multiple versions during transitions
- Can't "just fix" API issues without versioning

### Mitigation
- Start with v1 that covers core use cases
- Document edge cases before they become bugs
- Use feature flags within versions for non-breaking additions

---

## Evidence

- `/api/v1/resolve` endpoint documented with OpenAPI-style spec
- Response schema validated in tests
- Changelog tracks all API changes

---

## API Contract Example

```yaml
# /api/v1/resolve
POST:
  summary: Resolve pronunciation for entities
  request:
    body:
      entities: string[]
      format: "elevenlabs" | "polly" | "vapi"
  response:
    results:
      - grapheme: string
        phoneme: string
        source: "cmudict" | "phonemizer" | "override"
        confidence: number
    export:
      format: string
      dictionary_url: string
```

---

## Alternatives Considered

1. **GraphQL:** Flexible queries, single endpoint
   - Rejected: Overkill for our use case; REST is simpler and well-understood

2. **Versionless API:** Evolve carefully, never break
   - Rejected: Inevitably something breaks; explicit versions are honest

3. **RPC-style:** Method-based calls
   - Rejected: REST is more standard for external APIs
