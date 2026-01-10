# Incident Response Runbook

## Purpose

This runbook defines the standard operating procedure for responding to production incidents.

---

## Severity Levels

| Level | Definition | Response Time | Examples |
|-------|------------|---------------|----------|
| **SEV1** | Complete service outage | Immediate | API down, database unreachable |
| **SEV2** | Partial outage or degraded service | <30 min | Slow responses, payment failures |
| **SEV3** | Non-critical issue | <4 hours | UI bugs, minor data inconsistencies |
| **SEV4** | Cosmetic or low-impact | Next business day | Typos, styling issues |

---

## Incident Response Protocol

### Phase 1: Detection & Triage (0-5 minutes)

1. **Acknowledge the alert**
   - Confirm you're responding
   - Update status page if applicable

2. **Assess severity**
   - Is the service completely down?
   - How many users are affected?
   - Is data at risk?

3. **Gather initial information**
   - When did it start?
   - What changed recently? (deployments, config)
   - Any correlated alerts?

### Phase 2: Stabilization (5-30 minutes)

1. **Prioritize stabilization over root cause**
   - Can we rollback?
   - Can we disable the failing component?
   - Can we route around the issue?

2. **Common stabilization actions**
   ```bash
   # Rollback deployment
   git revert HEAD && git push

   # Restart service
   # (platform-specific commands)

   # Scale up if load-related
   # (platform-specific commands)
   ```

3. **Communicate status**
   - Internal: Team channel update
   - External: Status page update (if applicable)

### Phase 3: Investigation (30 min - 2 hours)

1. **Check logs**
   - Application logs for errors
   - Database logs for query issues
   - Infrastructure logs for resource problems

2. **Check metrics**
   - Error rates
   - Response times
   - Resource utilization

3. **Correlate with changes**
   - Recent deployments
   - Configuration changes
   - External service issues

### Phase 4: Resolution

1. **Apply fix**
   - Hotfix if simple
   - Rollback if complex

2. **Verify resolution**
   - Confirm service is healthy
   - Check error rates are normal
   - Verify affected functionality

3. **Update status**
   - Mark incident as resolved
   - Update status page

### Phase 5: Post-Incident (within 48 hours)

1. **Create incident report**
   - Timeline of events
   - Root cause analysis
   - Impact assessment

2. **Identify action items**
   - What could have prevented this?
   - What would have detected it faster?
   - What would have resolved it faster?

3. **Schedule post-mortem** (for SEV1/SEV2)
   - Blameless review
   - Document learnings
   - Assign follow-up tasks

---

## Communication Templates

### Internal Update
```
🔴 INCIDENT: [Brief description]
Status: [Investigating/Mitigating/Resolved]
Impact: [Who/what is affected]
Current action: [What we're doing now]
ETA: [If known]
```

### External Update (Status Page)
```
We are currently experiencing [issue description].
[X]% of users may be affected.
Our team is actively working on resolution.
Last updated: [timestamp]
```

---

## Escalation Path

| Condition | Action |
|-----------|--------|
| SEV1 not stabilized in 15 min | Escalate to senior engineer |
| Customer-facing data issue | Notify product/support |
| Security-related | Notify security lead |
| External service issue | Contact vendor support |

---

## Post-Incident Checklist

- [ ] Incident timeline documented
- [ ] Root cause identified
- [ ] Impact quantified
- [ ] Customer communication sent (if applicable)
- [ ] Action items created
- [ ] Post-mortem scheduled (SEV1/SEV2)
- [ ] Monitoring improved (if gap identified)

---

## Related Documents

- [Daily Workflow Runbook](./daily-workflow.md)
- [ADR-002: Idempotent Webhooks](../adrs/002-idempotent-webhooks.md)
