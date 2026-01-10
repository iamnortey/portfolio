# Security Engineering Role Alignment

## What I've Built That Maps to This Role

- **Row-Level Security (RLS):** Organization-scoped data isolation across all tables
- **Webhook signature verification:** Cryptographic validation of inbound requests
- **Secrets management:** No hardcoded credentials, environment-based configuration
- **Security documentation:** SECURITY.md, threat model considerations

## Relevant Artifacts

### Case Studies
- [Ojanaa Case Study](../case-studies/ojanaa.md) — RLS, auth, payment security
- [Ninobyte Case Study](../case-studies/ninobyte.md) — Security policy and governance

### ADRs
- [ADR-002: Idempotent Webhooks](../adrs/002-idempotent-webhooks.md) — Safe external integrations

### Documentation
- [Redaction Policy](../docs/REDACTION_POLICY.md) — Data classification
- [Publishing Checklist](../docs/PUBLISHING_CHECKLIST.md) — Secret detection

## Operating Model

### Security-by-Design Approach

1. **Defense in depth:** Multiple layers of protection
2. **Least privilege:** Access only what's needed
3. **Fail secure:** Errors should deny, not allow
4. **Audit everything:** Log security-relevant events

### How I Think About Threats

| Layer | Threat | Mitigation |
|-------|--------|------------|
| **Application** | Injection, XSS | Input validation, output encoding |
| **Authentication** | Credential theft | Secure sessions, MFA where possible |
| **Authorization** | Privilege escalation | RLS, RBAC, explicit checks |
| **Data** | Exposure, tampering | Encryption, integrity checks |
| **Network** | MITM, interception | HTTPS everywhere, cert pinning |

### RLS Implementation Pattern

```sql
-- Every table has org_id
-- Every policy checks org_id against user's org

CREATE POLICY "org_isolation" ON invoices
FOR ALL
USING (org_id = auth.jwt() ->> 'org_id');
```

**Benefits:**
- Defense even if application code has bugs
- Single policy per table, not per query
- Easier audit (check policies, not code)

### Secrets Management Rules

1. **Never in code:** Not even "just for testing"
2. **Environment variables:** Configuration, not code
3. **Rotation capability:** Design for credential rotation
4. **Audit access:** Know who can see secrets

## Key Skills Demonstrated

| Skill | Evidence |
|-------|----------|
| Access Control | RLS policies, RBAC patterns |
| Secure Development | Webhook verification, input validation |
| Secrets Management | Environment-based config, no hardcoding |
| Security Documentation | SECURITY.md, threat considerations |
| Data Classification | Redaction policies, safe/unsafe categorization |
