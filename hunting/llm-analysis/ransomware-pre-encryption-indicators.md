---
title: "Ransomware Pre-Encryption Indicator Analysis"
author: thegr8val
use_case: "Identify ransomware staging behaviors in logs before encryption executes"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - hunting
  - ransomware
  - log-analysis
  - blue-team
  - triage
---

## Prompt

You are a threat hunter specializing in ransomware detection. I will provide log data from a potentially compromised environment. Analyze it for pre-encryption staging behaviors — the actions ransomware operators take before deploying the encryptor.

Focus on:
- **Discovery** — network scanning, AD enumeration, share enumeration
- **Credential access** — LSASS dumping, SAM access, credential tools
- **Defense evasion** — AV/EDR tampering, log clearing, safe mode abuse
- **Persistence staging** — scheduled tasks, services, RMM tool installation
- **Data staging** — mass file access, exfiltration prep, archive creation
- **Pre-encryption markers** — shadow copy deletion, BCDedit modifications, wbadmin tampering

For each behavior found:
1. Identify the specific log evidence
2. Map to MITRE ATT&CK
3. Assess whether it is likely operator activity (hands-on-keyboard) or automated
4. Estimate time-to-encryption if patterns suggest imminent deployment

Conclude with a **blast radius estimate**: how many systems appear to be in scope for encryption based on the evidence.

---

**Log sources:** [SPECIFY WHAT YOU HAVE]

**Time range:** [START — END UTC]

**Known context:** [Any confirmed compromise details, initial access vector if known, affected BU or site]

**Log data:**

```
[PASTE LOG DATA HERE]
```

---

### Output format:

#### Pre-Encryption Behavior Analysis

**Overall assessment:** [Ransomware staging confirmed / Suspected / Insufficient evidence]
**Estimated time to encryption:** [Imminent / Hours / Unknown — with reasoning]
**Blast radius estimate:** [Number of hosts likely targeted]

---

#### Behavior findings

| Behavior Category | Evidence | MITRE | Operator vs Automated | Confidence |
|-------------------|----------|-------|----------------------|------------|
| [category] | [specific log evidence] | [Txxxx] | [Operator/Auto/Unknown] | [H/M/L] |

---

#### Recommended immediate containment actions

1. [Specific action — e.g., "Isolate DC01 — evidence of credential dumping at 03:14 UTC"]
2. [Next action]

---

#### What to look for next

[Specific log sources or queries that would confirm or deny imminent encryption]

---

## Notes

- Time matters with ransomware. If you see shadow copy deletion or BCDedit in the logs, treat it as P1 regardless of other uncertainty.
- Key LOLBins to watch for in log input: `vssadmin.exe delete shadows`, `wbadmin delete catalog`, `bcdedit /set {default} safeboot`, `net stop` loops, `taskkill /IM` against AV processes.
- If you have EDR telemetry, it's more valuable than Windows Event Logs alone for this use case — process trees and parent-child relationships are critical.

---

## [ES] Notas

- El tiempo es critico con ransomware. Si ves eliminacion de shadow copies o BCDedit en los logs, tratar como P1 independientemente de otras incertidumbres.
- LOLBins clave a buscar: `vssadmin.exe delete shadows`, `wbadmin delete catalog`, `bcdedit /set safeboot`, bucles de `net stop`, `taskkill /IM` contra procesos AV.
- La telemetria de EDR es mas valiosa que los Windows Event Logs solos para este caso de uso.
