---
title: "Threat Actor Profiling"
author: thegr8val
use_case: "Build a structured intelligence profile of a threat actor from raw reporting, TTPs, or IOCs"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - hunting
  - threat-actor
  - osint
  - enrichment
---

## Prompt

You are a senior threat intelligence analyst. I will provide you with raw intelligence data about a threat actor. Your task is to produce a structured profile using the format below.

Be precise. If information is unknown or unconfirmed, state that explicitly rather than speculating. Use confidence qualifiers: **Confirmed**, **Likely**, **Suspected**, **Unknown**.

---

**Input data:**

```
[PASTE RAW INTEL HERE: reports, IOC lists, MITRE mappings, news articles, vendor advisories, etc.]
```

---

**Output the profile in this exact structure:**

### Threat Actor Profile

**Alias(es):** [Known names and designations]
**Origin:** [Country or region — with confidence level]
**Motivation:** [Financial / Espionage / Hacktivism / Destruction — with confidence level]
**Targeting:** [Industries, geographies, or organizations typically targeted]
**Active since:** [Approximate first observed date]
**Last observed activity:** [Most recent confirmed activity]

---

**TTPs (MITRE ATT&CK)**

| Tactic | Technique ID | Technique Name | Confidence |
|--------|-------------|----------------|------------|
| [tactic] | [Txxxx.xxx] | [name] | [level] |

---

**Infrastructure**

- Known C2 domains/IPs: [list or Unknown]
- Preferred hosting: [providers, ASNs, geographies]
- Infrastructure patterns: [fast-flux, bulletproof hosting, legitimate services abuse, etc.]

---

**Malware / Tooling**

| Tool | Type | Custom/COTS | Notes |
|------|------|-------------|-------|
| [name] | [RAT/loader/stealer/etc.] | [Custom/Open-source/Commercial] | [brief note] |

---

**Notable campaigns**

1. [Campaign name or date] — [One-sentence summary]

---

**Analyst notes**

[Any caveats, gaps in intelligence, or analytical judgments that don't fit the structured fields above.]

---

**References**

- [Source 1]
- [Source 2]

---

## Example input

```
APT29 (Cozy Bear) — associated with Russian SVR. Observed in SolarWinds supply chain attack (2020).
Uses SUNBURST, TEARDROP malware. Targets government, think tanks, healthcare. C2: avsvmcloud[.]com.
MITRE: T1195.002 (Supply Chain Compromise), T1059.001 (PowerShell), T1027 (Obfuscated Files).
```

---

## Example output

### Threat Actor Profile

**Alias(es):** APT29, Cozy Bear, Nobelium, The Dukes
**Origin:** Russia — Confirmed (attributed to SVR by US/UK governments)
**Motivation:** Espionage — Confirmed
**Targeting:** Government, NGOs, think tanks, healthcare, technology
**Active since:** ~2008
**Last observed activity:** 2021 (Microsoft 365 token theft campaigns)

**TTPs (MITRE ATT&CK)**

| Tactic | Technique ID | Technique Name | Confidence |
|--------|-------------|----------------|------------|
| Initial Access | T1195.002 | Supply Chain Compromise: Compromise Software Supply Chain | Confirmed |
| Execution | T1059.001 | Command and Scripting Interpreter: PowerShell | Confirmed |
| Defense Evasion | T1027 | Obfuscated Files or Information | Confirmed |

_(output continues...)_

---

## Notes

- Works best with long-context models (Claude, GPT-4o) when pasting large intel reports.
- For MITRE mappings, the model performs better if you include raw behavior descriptions rather than just technique IDs.
- Cross-reference output against MITRE ATT&CK Navigator for validation before operational use.

---

## [ES] Notas

- Funciona mejor con modelos de contexto largo cuando se pega el reporte completo de inteligencia.
- Para los mapeos de MITRE, el modelo produce mejores resultados con descripciones de comportamiento en lugar de solo IDs de tecnicas.
- Validar el output contra MITRE ATT&CK Navigator antes de uso operacional.
