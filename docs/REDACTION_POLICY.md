# Redaction Policy

This document defines what MUST be redacted before any content is published publicly.

---

## Classification Levels

### NEVER PUBLISH (Hard Block)

These items must NEVER appear in any public repository:

| Category | Examples | Risk |
|----------|----------|------|
| **API Keys** | `sk-*`, `pk-*`, Supabase keys, OpenAI keys | Account compromise |
| **Tokens** | JWT tokens, session tokens, webhook secrets | Unauthorized access |
| **Credentials** | Passwords, connection strings | Data breach |
| **Environment Files** | `.env`, `.env.local`, `.envrc` | Full system compromise |
| **Internal URLs** | Staging servers, admin panels | Attack surface exposure |
| **Customer Data** | Names, emails, phones, addresses | Privacy violation |
| **Financial Data** | Revenue, pricing, invoices | Business intelligence leak |
| **Infrastructure** | IPs, ports, topology | Security vulnerability |

### REDACT BEFORE PUBLISH

These items can be published after proper redaction:

| Category | Redaction Method |
|----------|------------------|
| Screenshots | Blur/black-out identifiers, use synthetic data |
| Logs | Replace real IDs with `<PLACEHOLDER>` |
| Config examples | Use `YOUR_VALUE_HERE` patterns |
| Architecture diagrams | Generic names, no hostnames |
| Error messages | Remove stack traces with file paths |

### SAFE TO PUBLISH

| Category | Notes |
|----------|-------|
| Architecture decisions | High-level design rationale |
| Engineering principles | Process and methodology |
| Tech stack descriptions | Public knowledge |
| Runbook structures | Process without secrets |
| API shapes | Interface design without implementation |
| Metrics (counts/ranges) | Aggregate numbers only |

---

## Synthetic Data Standards

When demonstrating functionality, use ONLY these patterns:

### Personal Information
```
Name: Kwame Asante, Ama Mensah, Kofi Boateng
Email: demo@example.com, test@example.com
Phone: +233 XX XXX XXXX
```

### Business Information
```
Organization: Accra Demo Store, Kumasi Test Shop
Address: 123 Oxford Street, Osu, Accra
Invoice ID: INV-DEMO-001, INV-DEMO-002
Order ID: ORD-DEMO-001
```

### Financial
```
Amount: GHS 150.00, GHS 500.00, $25.00
Currency: GHS, USD (never real transaction amounts)
```

### Technical
```
API Key: YOUR_API_KEY_HERE
Database: postgres://localhost/demo_db
URL: https://api.example.com/v1/resource
```

---

## Screenshot Redaction Procedure

### Step 1: Prepare Environment
- Clear all real data from view
- Log into demo/test account if available
- Use incognito browser

### Step 2: Capture
- Capture only the necessary area
- Avoid browser chrome if possible
- Prefer application windows over full screen

### Step 3: Redact
Tools: Preview (macOS), Figma, or ImageMagick

Required redactions:
- [ ] URL bar
- [ ] Any text containing real names
- [ ] Any text containing real emails/phones
- [ ] Any numeric IDs
- [ ] Any amounts (replace with synthetic)
- [ ] Tab titles that reveal internal tools
- [ ] Bookmarks bar

### Step 4: Verify
- Zoom to 200% and scan for missed data
- Check corners and edges
- Verify no metadata in image file (strip EXIF)

---

## Code Snippet Redaction

### Before
```typescript
const supabase = createClient(
  'https://abc123xyz.supabase.co',
  'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...'
);
```

### After
```typescript
const supabase = createClient(
  process.env.SUPABASE_URL,
  process.env.SUPABASE_ANON_KEY
);
```

---

## Violation Response

If sensitive data is accidentally published:

1. **Immediately** remove the commit (force push if necessary)
2. **Rotate** any exposed credentials
3. **Document** the incident
4. **Review** how it passed the checklist

---

## Policy Version

**Version:** 1.0
**Last Updated:** 2026-01-10
**Owner:** Isaac Nortey
