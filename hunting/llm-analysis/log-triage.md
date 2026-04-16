---
title: "Log Triage for Suspicious Activity"
author: thegr8val
use_case: "Triage a block of logs to identify suspicious activity, anomalies, and investigation leads"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - hunting
  - log-analysis
  - triage
  - blue-team
---

## Prompt

You are a SOC analyst performing log triage. I will provide you with raw log data. Your task is to:

1. Identify events that are suspicious, anomalous, or worth investigating
2. Explain *why* each flagged event is concerning
3. Suggest the next investigation step for each finding
4. Assign a priority: **P1 (Critical) / P2 (High) / P3 (Medium) / P4 (Low)**

Focus on signal. Do not list every event — only flag what warrants human attention. If nothing is suspicious, say so explicitly.

---

**Log source:** [SPECIFY: Windows Event Log / Sysmon / Zeek / Proxy / Auth log / etc.]

**Time range:** [START — END]

**Context (optional):** [Any known good activity, ongoing incidents, or assets in scope]

**Log data:**

```
[PASTE LOG DATA HERE]
```

---

**Output format:**

### Triage Report

**Log source:** [source]
**Events reviewed:** [approximate count]
**Suspicious findings:** [count]

---

#### Finding [N] — [Short title]

**Priority:** [P1 / P2 / P3 / P4]
**Timestamp(s):** [relevant timestamps]
**Event(s):** [event IDs or log lines]
**Why it's suspicious:** [clear explanation]
**Next step:** [specific investigation action]

---

_(repeat for each finding)_

---

**Summary**

[One paragraph: overall assessment of the log set, whether an incident is likely, and recommended escalation path.]

---

## Example input

```
[Log source: Windows Security Event Log]
[Time range: 2026-04-15 02:00 — 02:30 UTC]

4624 LOGON_SUCCESS user=administrator src=192.168.1.105 logon_type=3 02:04:12
4624 LOGON_SUCCESS user=administrator src=10.0.0.44 logon_type=10 02:04:45
4625 LOGON_FAILURE user=administrator src=185.220.101.45 02:05:01
4625 LOGON_FAILURE user=administrator src=185.220.101.45 02:05:03
4625 LOGON_FAILURE user=administrator src=185.220.101.45 02:05:05
4648 LOGON_EXPLICIT_CREDS user=svc_backup target=DC01 02:07:33
7045 SERVICE_INSTALLED name=WindowsUpdate path=C:\Users\Public\update.exe 02:09:11
```

---

## Example output

### Triage Report

**Log source:** Windows Security Event Log
**Events reviewed:** 7
**Suspicious findings:** 3

#### Finding 1 — Brute force attempt from external IP

**Priority:** P2 (High)
**Timestamp(s):** 02:05:01 — 02:05:05 UTC
**Event(s):** Three consecutive 4625 failures from 185.220.101.45
**Why it's suspicious:** Rapid sequential login failures from an external IP targeting the administrator account. 185.220.101.45 is a known Tor exit node.
**Next step:** Block IP at perimeter. Check if any 4624 success events follow from this IP. Review all auth events for this IP across the environment.

_(output continues...)_

---

## Notes

- Scrub or anonymize real hostnames, usernames, and IPs before pasting into external LLMs.
- For very large log sets, pre-filter to a relevant time window or event ID subset before sending.
- This prompt is most effective for investigations — not a replacement for a SIEM with correlation rules.

---

## [ES] Notas

- Anonimiza nombres de host, usuarios e IPs reales antes de pegar en LLMs externos.
- Para conjuntos de logs muy grandes, pre-filtra por ventana de tiempo o IDs de evento antes de enviar.
- Este prompt es mas efectivo para investigaciones — no reemplaza un SIEM con reglas de correlacion.
