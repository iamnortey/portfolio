# Daily Workflow Runbook

## Purpose

This runbook defines the standard daily operating procedures for maintaining production systems and making progress on development.

---

## Morning Check (First 15 minutes)

### 1. System Health Review

```bash
# Check service status
# (Platform-specific health endpoints)

# Review overnight alerts
# (Check alerting dashboard)

# Check error rates
# (Check monitoring dashboard)
```

**Look for:**
- Elevated error rates
- Unusual traffic patterns
- Failed background jobs
- Database connection issues

### 2. Queue Status

- Are there any stuck jobs?
- Is the queue depth normal?
- Any jobs failing repeatedly?

### 3. External Service Status

Check status pages for critical dependencies:
- Database provider
- Payment providers
- Messaging services

---

## Development Workflow

### Before Starting Work

1. **Pull latest changes**
   ```bash
   git checkout main
   git pull origin main
   ```

2. **Check CI status**
   - Is main branch green?
   - Any pending PRs that need review?

3. **Review today's priorities**
   - What's the most important task?
   - Any blockers from yesterday?

### During Development

1. **Follow phase gates**
   - Confirm current phase
   - Don't work on future-phase features

2. **Write tests alongside code**
   - Not after, alongside
   - Test the behavior, not the implementation

3. **Commit frequently**
   - Small, logical commits
   - Descriptive commit messages

### Before Pushing

1. **Run local tests**
   ```bash
   npm test
   # or
   pytest
   ```

2. **Check for secrets**
   - No API keys in code
   - No hardcoded credentials
   - Environment variables for config

3. **Self-review the diff**
   ```bash
   git diff --staged
   ```

---

## PR Workflow

### Creating a PR

1. **Clear title and description**
   - What does this change?
   - Why is it needed?
   - How was it tested?

2. **Link related issues**
   - Closes #XXX
   - Related to #YYY

3. **Add appropriate reviewers**
   - At least one reviewer for all PRs
   - Additional reviewers for sensitive changes

### Reviewing PRs

1. **Understand the context**
   - Read the issue/task first
   - Understand what problem is being solved

2. **Review for:**
   - Correctness (does it work?)
   - Security (any vulnerabilities?)
   - Performance (any obvious issues?)
   - Maintainability (will this be clear in 6 months?)

3. **Be constructive**
   - Explain why, not just what
   - Offer alternatives
   - Distinguish blocking vs. nice-to-have

---

## Deployment Checklist

### Pre-Deployment

- [ ] All tests passing
- [ ] PR approved
- [ ] No unresolved comments
- [ ] Database migrations ready (if any)
- [ ] Feature flags configured (if applicable)

### Deployment

- [ ] Deploy to staging first
- [ ] Verify staging functionality
- [ ] Deploy to production
- [ ] Verify production functionality

### Post-Deployment

- [ ] Monitor error rates for 15 minutes
- [ ] Check key user flows
- [ ] Confirm no alerts triggered

---

## End of Day

### 1. Document Progress

- What was accomplished?
- Any blockers for tomorrow?
- Update task/issue status

### 2. Clean Up

- Commit work-in-progress (or stash)
- Close unused browser tabs
- Update notes for tomorrow

### 3. Final Health Check

- Any new alerts?
- Error rates normal?
- Queues healthy?

---

## Weekly Tasks

### Monday
- Review week's priorities
- Check dependency updates
- Review any weekend alerts

### Friday
- Clean up stale branches
- Review metrics for the week
- Document any tech debt discovered

---

## Related Documents

- [Incident Response Runbook](./incident-response.md)
- [ADR-001: Phase-Gated Development](../adrs/001-phase-gated-development.md)
