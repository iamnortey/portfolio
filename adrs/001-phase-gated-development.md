# ADR-001: Phase-Gated Development

**Status:** Accepted
**Date:** 2025-12-28
**Context:** Ojanaa project initiation

---

## Context

Ojanaa is a complex multi-phase project:
- Phase 0: Infrastructure setup
- Phase 1: Invoice Trust Loop (POS core)
- Phase 2: Logistics & Tracking
- Phase 3: Services & Booking

The temptation is always to build features from later phases while Phase 1 is "almost done." This leads to:
- Incomplete Phase 1 functionality
- Technical debt from premature abstractions
- Scope creep that delays actual shipping

---

## Decision

**Enforce phase gates:** No Phase N+1 features until Phase N passes all quality gates.

Quality gates are explicit and measurable:
- Phase 0: Webhook verifies, logs write safely, CI green
- Phase 1: Invoice Trust Loop E2E functional with tests
- Phase 2: Smart Scan & Tracking stable
- Phase 3: Booking logic correct

---

## Consequences

### Positive
- Forces completion before expansion
- Prevents scope creep
- Ensures solid foundation
- Makes progress measurable

### Negative
- Slower perceived velocity
- Frustrating when "cool Phase 2 idea" must wait
- Requires discipline to enforce

### Mitigation
- Document Phase 2+ ideas in backlog, don't ignore them
- Review gate criteria at phase transitions
- Celebrate phase completions

---

## Evidence

- Engineering Charter enforces this pattern
- Project Operating Guide documents gates
- Phase completion requires explicit sign-off

---

## Alternatives Considered

1. **Feature flags:** Build everything, release incrementally
   - Rejected: Increases complexity, tempts premature building

2. **Parallel development:** Multiple phases at once
   - Rejected: Spreads focus, increases risk of incomplete features

3. **No formal gates:** Ship when ready
   - Rejected: "Ready" is subjective, leads to eternal beta
