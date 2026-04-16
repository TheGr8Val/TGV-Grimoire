---
title: "IOC Enrichment and Classification"
author: thegr8val
use_case: "Enrich a list of IOCs with context, classification, and hunting recommendations"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - hunting
  - ioc
  - enrichment
  - triage
---

## Prompt

You are a threat intelligence analyst specializing in IOC enrichment. I will provide a list of indicators. For each one:

1. Identify the IOC type (IP, domain, URL, hash, email, etc.)
2. Classify it based on known threat context if available
3. Assign a severity: **Critical / High / Medium / Low / Unknown**
4. Suggest a hunting action

If you do not have context on a specific IOC, say so. Do not fabricate threat associations.

---

**IOC list:**

```
[PASTE IOC LIST HERE — one per line, mixed types accepted]
```

---

**Output format (one block per IOC):**

```
IOC: <value>
Type: <IP | Domain | URL | FileHash-MD5/SHA1/SHA256 | Email | Other>
Context: <Known association or "No known context">
Severity: <Critical | High | Medium | Low | Unknown>
Hunting action: <Specific recommended query or investigation step>
```

---

## Example input

```
185.220.101.45
update-service[.]com
3395856ce81f2b7382dee72602f798b642f14140
malware@evil-domain.ru
hxxps://cdn.badsite[.]net/payload.exe
```

---

## Example output

```
IOC: 185.220.101.45
Type: IP
Context: Known Tor exit node. Frequently appears in scanning and credential stuffing campaigns.
Severity: Medium
Hunting action: Search for this IP in authentication logs, proxy logs, and firewall denies over the last 30 days.

IOC: update-service[.]com
Type: Domain
Context: Generic typosquat pattern. No confirmed malicious association in training data.
Severity: Unknown
Hunting action: Check DNS resolution history, certificate transparency logs (crt.sh), and WHOIS for registration date under 90 days.

IOC: 3395856ce81f2b7382dee72602f798b642f14140
Type: FileHash-SHA1
Context: Associated with Emotet loader variants circa 2021.
Severity: High
Hunting action: Search EDR telemetry for file creation or process execution matching this hash. Pivot to parent process and network connections.
```

---

## Notes

- The model will not have real-time threat intel. Use this prompt to structure and reason about IOCs you've already pulled from feeds (VirusTotal, MISP, etc.), not as a substitute for live lookups.
- Defang URLs and domains in your input (`[.]` notation) to avoid accidental resolution. The model handles defanged IOCs correctly.
- For large IOC lists (100+), break into batches of 20-30 for better output quality.

---

## [ES] Notas

- El modelo no tiene inteligencia de amenazas en tiempo real. Usa este prompt para estructurar y razonar sobre IOCs que ya obtuviste de feeds (VirusTotal, MISP, etc.).
- Defensiviza URLs y dominios con notacion `[.]` antes de pegar.
- Para listas grandes (100+ IOCs), divide en lotes de 20-30 para mejor calidad de output.
