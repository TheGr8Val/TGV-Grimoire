---
title: "Crown Jewels Mapping and Monitoring Recommendations"
author: thegr8val
use_case: "Identify high-value assets and recommend monitoring controls tailored to an organization's profile"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - blue-team
  - detection-engineering
  - hunting
  - reporting
---

## Prompt

You are a security architect conducting a crown jewels analysis. Based on the organization profile below, identify the most likely high-value targets for an attacker and recommend specific monitoring controls for each.

For each crown jewel:
1. Identify the asset/system/data type
2. Explain why it's high value (what an attacker gains from compromising it)
3. List the most likely attack paths to reach it
4. Recommend specific detection controls (log sources, alerts, behavioral analytics)
5. Note any current monitoring gap that leaves it exposed

Prioritize by: **Tier 1 (catastrophic if compromised) / Tier 2 (significant impact) / Tier 3 (material but recoverable)**

---

**Organization profile:**

- **Sector:** [e.g., Healthcare, Finance, Manufacturing, Technology]
- **Size:** [employees, locations, revenue range if relevant]
- **Core business function:** [what the org actually does — 1-2 sentences]
- **Key systems/platforms:** [e.g., Epic EHR, SAP ERP, Salesforce, Active Directory, AWS, Azure, OT/SCADA]
- **Regulatory environment:** [e.g., HIPAA, PCI-DSS, SOX, NERC CIP, GDPR]
- **Known threat actors targeting this sector:** [or "Unknown"]

**Current monitoring capabilities:**

```
[LIST WHAT YOU HAVE: SIEM, EDR, DLP, CASB, network monitoring, cloud security tooling, etc.]
```

**Known monitoring gaps (optional):**

[e.g., No EDR on OT network, No DLP on email, Cloud not integrated into SIEM]

---

### Output format:

#### Crown Jewels Analysis

---

##### Tier 1 Asset: [Asset Name]

**Asset type:** [Data / System / Process / Infrastructure]
**Why it's high value:** [attacker objective if compromised]
**Likely attack paths:**
1. [Path 1 — e.g., "Phishing → credential theft → VPN access → lateral movement to EHR database server"]
2. [Path 2]

**Recommended monitoring controls:**

| Control | Log source | Specific detection | Priority |
|---------|------------|-------------------|----------|
| [control name] | [log source] | [specific alert or analytic] | [High/Med] |

**Current gap:** [What's missing from current monitoring for this asset]

---

_(repeat for each tier)_

---

#### Prioritized monitoring roadmap

| Priority | Asset | Gap | Recommended action | Effort |
|----------|-------|-----|--------------------|--------|
| 1 | [asset] | [gap] | [specific action] | [Low/Med/High] |

---

## Notes

- The more specific the org profile, the more targeted and useful the output.
- Use the monitoring roadmap output as input to `detection-gap-analysis.md` for TTP-level coverage mapping.
- Crown jewels change as the business evolves — revisit this analysis annually or after major M&A or infrastructure changes.

---

## [ES] Notas

- Cuanto mas especifico sea el perfil de la organizacion, mas especifico y util sera el output.
- Usar el roadmap de monitoreo como input para `detection-gap-analysis.md` para mapeo de cobertura a nivel de TTPs.
- Las joyas de la corona cambian a medida que evoluciona el negocio — revisar anualmente o despues de M&A o cambios de infraestructura importantes.
