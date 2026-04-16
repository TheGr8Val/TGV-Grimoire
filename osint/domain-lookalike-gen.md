---
title: "Lookalike and Typosquat Domain Generation"
author: thegr8val
use_case: "Generate lookalike and typosquat domain variants of a target domain for monitoring or brand protection"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - osint
  - phishing
  - brand-protection
  - hunting
  - automation
---

## Prompt

Generate a comprehensive list of lookalike and typosquat domain variants for the target domain below. The purpose is defensive monitoring and brand protection — identifying domains that could be used for phishing, impersonation, or fraud against the organization or its customers.

Cover the following variation types:
1. **Typosquats** — common keyboard typos (adjacent keys, transpositions, double letters, missing letters)
2. **Homoglyphs** — visually similar characters (rn→m, 0→o, 1→l, vv→w)
3. **TLD variations** — same name, different TLD (.net, .org, .io, .co, .biz, regional TLDs)
4. **Subdomain abuse** — legitimate domain used as subdomain of attacker-controlled domain
5. **Keyword additions** — prefix/suffix patterns common in phishing (secure-, -login, -verify, support-, -update, -helpdesk)
6. **Brand + service combos** — domain + common service names (banking, pay, account, portal)
7. **Unicode/Punycode** — internationalized domain names that render identically in browsers

Output a deduplicated list, grouped by variation type.

---

**Target domain:** [e.g., example.com]

**Organization name (for keyword combos):** [e.g., Example Corp]

**Industry context (optional):** [Helps generate relevant keyword additions — e.g., banking, healthcare, SaaS]

**Output format:** [LIST / JSON]

---

## Example input

```
Target domain: acmecorp.com
Organization name: Acme Corp
Industry: Financial services / online banking
Output format: JSON
```

---

## Example output (truncated)

```json
{
  "target": "acmecorp.com",
  "variants": {
    "typosquats": [
      "acmecprp.com",
      "acmecorp.com",
      "acmecorpp.com",
      "acmecorp.com",
      "acmecor.com",
      "acemcorp.com",
      "acmcorp.com"
    ],
    "homoglyphs": [
      "acrnecorp.com",
      "acmec0rp.com",
      "acmecorp.com"
    ],
    "tld_variations": [
      "acmecorp.net",
      "acmecorp.org",
      "acmecorp.io",
      "acmecorp.co",
      "acmecorp.bank",
      "acmecorp.us"
    ],
    "subdomain_abuse": [
      "acmecorp.com.attacker.io",
      "login.acmecorp.phish.net"
    ],
    "keyword_additions": [
      "secure-acmecorp.com",
      "acmecorp-login.com",
      "acmecorp-verify.com",
      "acmecorp-support.com",
      "acmecorpbank.com",
      "acmecorponline.com",
      "myacmecorp.com",
      "acmecorpportal.com"
    ]
  }
}
```

---

## Notes

- Use this output as input to a monitoring pipeline: check each variant against certificate transparency logs (crt.sh), WHOIS registration, and DNS resolution daily.
- Tools to automate monitoring on this list: `dnstwist`, URLScan.io bulk search, Censys, Shodan.
- JSON output is ready for import into a brand monitoring tool or SOAR playbook.
- For high-value targets, combine with `passive-recon-checklist.md` on any registered variants to assess how they're being used.

---

## [ES] Notas

- Usar este output como input para un pipeline de monitoreo: verificar cada variante contra logs de transparencia de certificados, registro WHOIS, y resolucion DNS.
- Herramientas para automatizar el monitoreo: `dnstwist`, URLScan.io busqueda masiva, Censys.
- Para objetivos de alto valor, combinar con `passive-recon-checklist.md` en cualquier variante registrada.
