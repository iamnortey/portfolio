# Technical Support Engineering Role Alignment

## What I've Built That Maps to This Role

- **Runbooks:** 15+ operational procedures for debugging and troubleshooting
- **Incident response:** Documented procedures for production issues
- **Deep debugging:** Complex webhook flows, payment integrations, database issues
- **Customer-facing systems:** WhatsApp commerce platform with trust requirements

## Relevant Artifacts

### Case Studies
- [Ojanaa Case Study](../case-studies/ojanaa.md) — Customer-facing system with trust requirements

### Runbooks
- [Incident Response](../runbooks/incident-response.md) — Structured troubleshooting
- [Daily Workflow](../runbooks/daily-workflow.md) — Operational procedures

### ADRs
- [ADR-002: Idempotent Webhooks](../adrs/002-idempotent-webhooks.md) — Understanding integration issues

## Operating Model

### How I Debug Customer Issues

1. **Reproduce first:** Can I see what the customer sees?
2. **Gather context:** Logs, timestamps, recent changes
3. **Isolate the variable:** What's different about this case?
4. **Explain clearly:** Root cause and fix in plain language

### Debugging Philosophy

```
Symptom → Reproduce → Logs → Hypothesis → Test → Fix → Verify → Document
    ↓          ↓        ↓         ↓          ↓      ↓       ↓         ↓
  User      Local     Error    Theory    Minimal  Deploy  Check    KB
  report    env       search   of cause  change          resolved  article
```

**Key principles:**
- **Smallest change first:** Don't rewrite when a config change works
- **Verify before closing:** Confirm the fix actually fixed it
- **Document for next time:** Same issue shouldn't require same investigation

### Technical Communication Style

**For customers:**
- Plain language, no jargon
- Focus on impact and resolution
- Provide timeline and next steps

**For engineers:**
- Detailed technical context
- Reproduction steps
- Log snippets and stack traces

### Common Investigation Patterns

| Issue Type | First Steps |
|------------|-------------|
| **Integration failure** | Check webhook logs, verify signatures |
| **Data inconsistency** | Check idempotency keys, transaction logs |
| **Performance issue** | Check query plans, cache hit rates |
| **Auth problem** | Check RLS policies, session state |

## Key Skills Demonstrated

| Skill | Evidence |
|-------|----------|
| Debugging | Complex webhook flows, payment issues |
| Documentation | Runbooks, incident procedures |
| Customer Communication | WhatsApp platform (customer-facing) |
| System Understanding | Full-stack debugging capability |
| Escalation | Severity classification, escalation paths |

## ClickHouse/Data Support Relevance

Technical support for data systems requires:

| Capability | My Experience |
|------------|---------------|
| **SQL proficiency** | 650K+ lines PLpgSQL |
| **Query debugging** | Explain plans, index analysis |
| **Data pipeline issues** | Ninolex resolution pipeline |
| **Integration debugging** | Webhook handlers, API clients |
| **Clear communication** | Runbooks, documentation |
