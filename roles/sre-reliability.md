# SRE / Reliability Engineering Role Alignment

## What I've Built That Maps to This Role

- **Ojanaa:** Production system with runbooks, incident response procedures, and phase gates
- **Idempotent webhooks:** Retry-safe payment and messaging handlers
- **Monitoring patterns:** Structured logging, error tracking, alerting
- **Quality gates:** Explicit criteria for phase transitions

## Relevant Artifacts

### Case Studies
- [Ojanaa Case Study](../case-studies/ojanaa.md) — Reliability patterns in production

### ADRs
- [ADR-001: Phase-Gated Development](../adrs/001-phase-gated-development.md) — Quality control
- [ADR-002: Idempotent Webhooks](../adrs/002-idempotent-webhooks.md) — Retry safety

### Runbooks
- [Incident Response](../runbooks/incident-response.md) — Standard incident procedure
- [Daily Workflow](../runbooks/daily-workflow.md) — Operational hygiene

## Operating Model

### How I Debug Production Issues

1. **Stabilize first:** Get the system working, then investigate
2. **Check the basics:** Logs, metrics, recent changes
3. **Isolate the variable:** What changed? What's different?
4. **Verify the fix:** Don't declare victory until you're sure

### Incident Response Philosophy

```
Detection → Triage → Stabilize → Investigate → Resolve → Review
     ↓          ↓          ↓           ↓           ↓         ↓
  Alerts    Severity    Rollback     Logs       Fix      Post-
            assess      or scale     + metrics           mortem
```

**Key principles:**
- Stabilization over investigation
- Communication throughout
- Blameless post-mortems
- Action items with owners

### How I Think About Reliability

- **Error budgets:** Some failure is acceptable; zero is impossible
- **Defense in depth:** Multiple layers of protection (RLS, auth, validation)
- **Graceful degradation:** Better to be slow than broken
- **Observability:** You can't fix what you can't see

## Key Skills Demonstrated

| Skill | Evidence |
|-------|----------|
| Incident Response | Documented procedures, runbooks |
| Monitoring | Structured logging, alerting patterns |
| Reliability Patterns | Idempotency, retry safety, RLS |
| Documentation | Runbooks, ADRs, operational guides |
| Root Cause Analysis | Post-mortem templates and processes |
