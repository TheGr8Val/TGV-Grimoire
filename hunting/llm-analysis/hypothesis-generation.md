---
title: "Threat Hunting Hypothesis Generation"
author: thegr8val
use_case: "Generate prioritized hunting hypotheses based on sector, threat landscape, and available log sources"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - hunting
  - hypothesis
  - threat-actor
  - blue-team
---

## Prompt

You are a threat hunting lead. Based on the environment profile below, generate a prioritized list of hunting hypotheses. Each hypothesis should be actionable — something a hunter can test against available log data within a single shift.

For each hypothesis:
1. State the hypothesis clearly (one sentence, "If X is occurring, then Y should be observable")
2. Explain the threat basis (why this is relevant for this sector/environment)
3. Map to a MITRE ATT&CK technique
4. Specify which log sources are needed to test it
5. Provide a concrete starting query or analysis approach
6. Rate feasibility given the available log sources: **High / Medium / Low**

Rank hypotheses by combination of threat relevance and feasibility. Highest impact + highest feasibility at the top.

---

**Organization profile:**

- **Sector:** [e.g., Healthcare, Financial Services, Energy, Government, Tech]
- **Size:** [e.g., 2,000 employees, 3 office locations]
- **Crown jewels:** [e.g., patient records, trading systems, SCADA, source code]
- **Known threat actors targeting this sector:** [e.g., APT41, FIN7, Scattered Spider — or leave blank]
- **Recent threat intel or incidents:** [Any relevant context — or "None"]

**Available log sources:**

```
[LIST WHAT YOU HAVE: e.g., Windows Event Logs, Sysmon, EDR (CrowdStrike/SentinelOne), 
Proxy logs, DNS logs, VPN logs, NetFlow, Office 365 audit logs, etc.]
```

**Out of scope / known gaps:**

[e.g., No EDR on legacy servers, No DNS logging, Cloud environment not monitored]

---

## Example input

```
Organization profile:
- Sector: Healthcare
- Size: 8,000 employees, regional hospital network
- Crown jewels: EHR systems (Epic), medical devices, PII/PHI
- Known threat actors: Ransomware groups (LockBit, ALPHV), nation-state health sector targeting
- Recent threat intel: HC3 advisory on social engineering targeting IT help desks

Available log sources:
- Windows Event Logs (all workstations/servers)
- Sysmon v15 (servers only)
- CrowdStrike Falcon (80% endpoint coverage)
- Palo Alto firewall logs
- Office 365 unified audit log
- No EDR on medical devices

Out of scope: Medical device network not monitored
```

---

## Example output (truncated)

### Hunting Hypotheses

---

**Hypothesis 1 — Adversary-in-the-middle attack via MFA fatigue on help desk accounts**

*If an attacker is conducting MFA fatigue or social engineering against help desk staff, then we should observe unusual account resets followed by logins from new locations or devices within a short window.*

- **Threat basis:** HC3 advisory directly references this TTP against hospital IT help desks. Once help desk is compromised, attacker gains password reset capability for high-privilege accounts.
- **MITRE:** T1078 (Valid Accounts), T1621 (MFA Request Generation)
- **Log sources needed:** O365 audit log, Azure AD sign-in logs, VPN logs
- **Starting approach:** Query O365 for password reset events, then join to subsequent logins from new ASNs within 1 hour.
- **Feasibility:** High

---

## Notes

- The more specific the org profile and threat intel, the more targeted the hypotheses.
- Run this quarterly or after major threat intel publications for your sector.
- Use the output as input to the `splunk-query-gen.md` or `kql-query-gen.md` prompts to build queries for each hypothesis.

---

## [ES] Notas

- Cuanto mas especifico sea el perfil de la organizacion y la inteligencia de amenazas, mas especificas seran las hipotesis.
- Ejecutar trimestral o despues de publicaciones importantes de inteligencia de amenazas para el sector.
- Usar el output como input para los prompts de generacion de queries SPL o KQL.
