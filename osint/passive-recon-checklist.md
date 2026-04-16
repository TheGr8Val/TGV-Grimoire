---
title: "Passive Recon Checklist Generator"
author: thegr8val
use_case: "Generate a structured OSINT passive reconnaissance checklist for a target domain or organization"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - osint
  - recon
  - red-team
  - hunting
---

## Prompt

You are an OSINT analyst. Based on the target profile below, generate a structured passive reconnaissance checklist. The checklist should cover all major OSINT surface areas and include specific tools, queries, or URLs for each item.

Passive recon only — no active scanning, no direct requests to target infrastructure, no credential testing.

Organize the checklist by surface area. For each item include:
- What to look for
- Specific tool or resource to use
- Example query or search syntax where applicable
- What a finding here reveals (intelligence value)

---

**Authorization context:** [DESCRIBE AUTHORIZED SCOPE — e.g., "Authorized pentest pre-engagement recon", "Internal threat intel research", "Brand protection monitoring"]

**Target:**

- **Primary domain:** [e.g., example.com]
- **Organization name:** [e.g., Acme Corp]
- **Known subsidiaries or related domains:** [list or "Unknown"]
- **Industry:** [e.g., Healthcare, Finance, Energy]

**Objective:** [e.g., Attack surface mapping / Brand protection / Threat intel / Phishing campaign detection]

---

## Example input

```
Authorization: Authorized red team pre-engagement recon, scoped to acme-corp.com and subsidiaries

Target:
- Primary domain: acme-corp.com
- Organization: Acme Corp
- Related domains: acme.io, acmecorp.net (acquired 2023)
- Industry: Financial services

Objective: Attack surface mapping — identify exposed assets, credentials, and employee intelligence
  before active testing phase
```

---

## Example output (truncated)

### Passive Recon Checklist — acme-corp.com

---

#### Domain & DNS Intelligence

- [ ] **WHOIS history** — registrar, registration date, registrant changes
  - Tool: `whois acme-corp.com`, DomainTools, SecurityTrails
  - Intelligence value: Ownership changes, associated registrant email for pivot

- [ ] **DNS records** — A, MX, TXT, SPF, DKIM, DMARC, NS
  - Tool: `dig any acme-corp.com`, MXToolbox, DNSDumpster
  - Query: `dig TXT acme-corp.com` for SPF scope (reveals cloud services in use)
  - Intelligence value: Email infrastructure, cloud providers, anti-spoofing posture

- [ ] **Certificate transparency** — subdomains disclosed via TLS certs
  - Tool: `crt.sh`, Censys, `subfinder -d acme-corp.com`
  - Query: `https://crt.sh/?q=%25.acme-corp.com`
  - Intelligence value: Exposed subdomains including staging/dev environments

_(checklist continues across all surface areas...)_

---

## Notes

- Passive recon by definition creates no footprint on target systems. All sources listed use cached, public, or third-party data.
- For large organizations, certificate transparency and ASN lookups often reveal more scope than the initial domain list suggests.
- Export the checklist as a task list in your project management tool and check off items as you complete them.

---

## [ES] Notas

- El reconocimiento pasivo no crea huella en los sistemas objetivo. Todas las fuentes listadas usan datos en cache, publicos o de terceros.
- Para organizaciones grandes, la transparencia de certificados y las busquedas de ASN a menudo revelan mas alcance del que sugiere la lista inicial de dominios.
