# ADR-002: Idempotent Webhook Handlers

**Status:** Accepted
**Date:** 2025-12-29
**Context:** Ojanaa payment and messaging integration

---

## Context

Ojanaa integrates with external services that deliver webhooks:
- WhatsApp Business API (message status, incoming messages)
- Payment providers (transaction status updates)

These services will retry webhook delivery if they don't receive acknowledgment. This creates risk:
- Double-processing payments (charging twice, crediting twice)
- Duplicate messages sent to users
- Inconsistent state between systems

---

## Decision

**All webhook handlers must be idempotent:** Processing the same webhook multiple times produces the same result as processing it once.

Implementation patterns:
1. **Idempotency keys:** Store webhook ID, check before processing
2. **State machine guards:** Only process if current state allows transition
3. **Unique constraints:** Database enforces uniqueness where applicable

---

## Consequences

### Positive
- Safe retries from external services
- Resilient to network issues
- Consistent state regardless of delivery duplicates

### Negative
- More complex handler logic
- Requires idempotency key storage
- Additional database queries per webhook

### Mitigation
- Idempotency check is fast (indexed lookup)
- Pattern is well-documented in runbooks
- Tests verify idempotency behavior

---

## Evidence

- All payment webhook handlers implement idempotency check
- WhatsApp handlers check message ID before processing
- Database has unique constraints on transaction IDs

---

## Implementation Pattern

```typescript
async function handleWebhook(payload: WebhookPayload) {
  // 1. Extract idempotency key
  const key = payload.webhook_id;

  // 2. Check if already processed
  const existing = await db.webhookLog.findUnique({ where: { key } });
  if (existing) {
    return { status: 'already_processed' };
  }

  // 3. Process within transaction
  await db.$transaction(async (tx) => {
    // Record the webhook
    await tx.webhookLog.create({ data: { key, payload } });

    // Do the actual work
    await processPayment(tx, payload);
  });

  return { status: 'processed' };
}
```

---

## Alternatives Considered

1. **Exactly-once delivery assumption:** Trust the webhook provider
   - Rejected: No provider guarantees exactly-once; at-least-once is standard

2. **Deduplication at message queue:** Use a queue that handles duplicates
   - Rejected: Adds infrastructure complexity; simpler to handle in application

3. **Accept duplicates, reconcile later:** Process everything, fix inconsistencies
   - Rejected: Customer-facing payments must be correct immediately
