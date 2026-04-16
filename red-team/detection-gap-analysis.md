---
title: "Detection Gap Analysis"
author: thegr8val
use_case: "Given a list of TTPs, identify which have no current detection coverage and recommend remediation"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - red-team
  - blue-team
  - detection-engineering
  - sigma
  - hunting
---

## Prompt

You are a detection engineer conducting a gap analysis. I will provide:
1. A list of TTPs (MITRE ATT&CK technique IDs or behavioral descriptions)
2. The current detection coverage (rules, log sources, and monitoring capabilities)

For each TTP:
1. Assess whether it is covered, partially covered, or uncovered by current detection capability
2. If uncovered or partial: explain the gap and what log source or detection logic would close it
3. Prioritize the gaps by: **Critical (actively exploited, high impact) / High / Medium / Low**
4. Recommend a specific detection approach for each gap (Sigma rule concept, SIEM query pattern, behavioral analytic)

At the end, produce a prioritized remediation roadmap.

---

**Environment:**

- **SIEM:** [Splunk / Sentinel / Elastic / QRadar / etc.]
- **EDR:** [CrowdStrike / SentinelOne / Defender / Carbon Black / None]
- **Available log sources:** [list]
- **Known detection rules/content:** [list existing rules or "Vendor default content only"]

**TTPs to analyze:**

```
[LIST MITRE TECHNIQUE IDs OR BEHAVIOR DESCRIPTIONS — one per line]
```

**Context (optional):** [Threat actor, recent incident, red team findings driving this analysis]

---

### Output format:

#### Coverage Assessment

| TTP | Technique Name | Coverage | Gap Description | Priority |
|-----|---------------|----------|-----------------|----------|
| T1059.001 | PowerShell | Partial | No detection on encoded commands (-EncodedCommand flag) | High |

---

#### Gap detail + remediation (one block per uncovered/partial TTP)

**TTP:** Txxxx.xxx — [Name]
**Coverage:** Uncovered / Partial
**Gap:** [What is not being detected and why]
**Required log source:** [What you need to enable]
**Detection approach:** [Sigma rule concept, query pattern, or behavioral analytic description]
**Effort to close:** [Low (rule exists, just enable) / Medium (new rule needed) / High (log source gap, requires infra work)]

---

#### Remediation roadmap

| Priority | TTP | Action | Effort | Owner |
|----------|-----|--------|--------|-------|
| 1 | [TTP] | [specific action] | [Low/Med/High] | [SOC/Detection Eng/IT Ops] |

---

## Notes

- Pair this prompt with `hypothesis-generation.md` to build a full hunting and detection program: generate hypotheses, find the gaps, close them.
- For large TTP lists (full threat actor profile), break into tactics (Initial Access, Execution, etc.) and run one section at a time.
- The remediation roadmap output can be converted to Jira/Linear tickets directly — pair with `findings-to-remediation.md`.

---

## [ES] Notas

- Combinar con `hypothesis-generation.md` para construir un programa completo de hunting y deteccion.
- Para listas grandes de TTPs, dividir por tactica y ejecutar una seccion a la vez.
- El roadmap de remediacion se puede convertir directamente en tickets de Jira/Linear con `findings-to-remediation.md`.
