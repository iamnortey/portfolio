# Publishing Checklist

Use this checklist before pushing ANY content to a public repository.

---

## Pre-Publish Security Scan

### 1. Secrets Detection
- [ ] No API keys (patterns: `sk-*`, `pk-*`, `key-*`, `apikey`)
- [ ] No tokens (patterns: `token`, `bearer`, `auth`)
- [ ] No secrets (patterns: `secret`, `password`, `passwd`)
- [ ] No webhook verification tokens (`verify_token`)
- [ ] No base64-encoded credentials

### 2. Connection Strings
- [ ] No database URLs (`postgres://`, `mysql://`, `mongodb://`)
- [ ] No Supabase URLs (`*.supabase.co`)
- [ ] No internal hostnames or IP addresses
- [ ] No port numbers in production context

### 3. Identifiers
- [ ] No UUIDs that could be org/user/resource IDs
- [ ] No invoice/order IDs (real patterns)
- [ ] No customer IDs
- [ ] No session IDs

### 4. Personal Data
- [ ] No real email addresses
- [ ] No real phone numbers
- [ ] No real names (customer/user)
- [ ] No physical addresses

### 5. URLs
- [ ] No internal endpoints
- [ ] No staging/dev environment URLs
- [ ] No admin panel URLs
- [ ] Browser URL bars redacted in screenshots

---

## Screenshot/Demo Redaction

### Before Capture
- [ ] Use synthetic/demo data in the application
- [ ] Clear any real user sessions
- [ ] Use incognito mode to avoid showing bookmarks/history

### After Capture
- [ ] Blur/black-out any identifiable text
- [ ] Remove URL bar or blur it
- [ ] Remove any visible timestamps that could be traced
- [ ] Verify no console/network tab is visible with requests

### Synthetic Data Patterns (USE THESE)
| Type | Pattern |
|------|---------|
| Name | Kwame Asante, Ama Mensah |
| Email | demo@example.com |
| Phone | +233 XX XXX XXXX |
| Invoice | INV-DEMO-001 |
| Amount | GHS 150.00, $25.00 |
| Org | Accra Demo Store |
| Address | 123 Oxford Street, Osu, Accra |

---

## Content Review

### Documentation
- [ ] No internal meeting notes or decisions with names
- [ ] No revenue figures or financial projections
- [ ] No customer names or case references
- [ ] No internal Slack/email links

### Code Snippets
- [ ] No hardcoded values from production
- [ ] No real endpoint paths if sensitive
- [ ] Configuration examples use placeholders (`YOUR_API_KEY_HERE`)

### Architecture Diagrams
- [ ] Use generic component names ("Database", "API", "Mobile App")
- [ ] No internal hostnames or IPs
- [ ] No real port numbers for internal services

---

## Final Verification

- [ ] Run `scan_for_secrets.sh` against the folder
- [ ] Manual review of all markdown files
- [ ] Manual review of all image files
- [ ] Verify all links point to public resources
- [ ] Test README renders correctly on GitHub

---

## Sign-Off

**Reviewer:** _____________
**Date:** _____________
**Status:** [ ] APPROVED FOR PUBLISH / [ ] BLOCKED - NEEDS FIXES
