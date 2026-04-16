---
title: "Alert Fatigue Triage — Dedup, Cluster, and Prioritize"
author: thegr8val
use_case: "Reduce a large batch of SIEM alerts to a prioritized, deduplicated investigation queue"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - hunting
  - triage
  - blue-team
  - log-analysis
---

## Prompt

You are a SOC analyst facing an alert backlog. I will provide a list of security alerts. Your job is to:

1. **Deduplicate** — group alerts that are almost certainly the same underlying event (same host, same indicator, different timestamps or rule names)
2. **Cluster** — group alerts that likely belong to the same campaign or attacker activity chain
3. **Prioritize** — rank clusters by investigation urgency using: **P1 (Respond now) / P2 (Investigate today) / P3 (Review this week) / P4 (Tune or close)**
4. **Recommend a first action** for each cluster

Be opinionated. It is more useful to commit to a priority call with reasoning than to hedge everything as "needs more investigation."

---

**Alert format note:** [DESCRIBE YOUR ALERT FORMAT — e.g., "CSV export from Splunk with fields: time, rule_name, host, user, src_ip, dest_ip, severity"]

**Environment context (optional):**

[Known good activity, ongoing changes, assets under maintenance, or relevant recent events]

**Alerts:**

```
[PASTE ALERT LIST HERE]
```

---

### Output format:

#### Cluster [N] — [Short title]

**Priority:** [P1 / P2 / P3 / P4]
**Alert count:** [N alerts grouped here]
**Affected hosts/users:** [list]
**Cluster summary:** [2-3 sentences explaining what these alerts collectively suggest]
**MITRE technique(s):** [if applicable]
**First action:** [specific next step for an analyst]
**Disposition recommendation:** [Investigate / Tune / Close as false positive]

---

_(repeat for each cluster)_

---

#### Noise candidates

[Alerts that appear to be pure noise or chronic tuning candidates — list rule names and why]

---

#### Summary

**Total alerts reviewed:** [N]
**Clusters identified:** [N]
**Estimated true positives:** [N clusters worth investigating]
**Recommended tune candidates:** [list rule names]

---

## Notes

- Paste alert exports directly — CSV, JSON, or raw text all work.
- Include as much field data as available: host, user, src IP, dest IP, process, rule name. The more context, the better the clustering.
- For very large batches (500+ alerts), pre-filter to a 4-hour window or a single severity tier before sending.
- This prompt is most valuable during major incidents or after a detection content deployment that caused an alert spike.

---

## [ES] Notas

- Pegar exports de alertas directamente — CSV, JSON o texto plano funcionan.
- Incluir todos los campos disponibles: host, usuario, IP origen/destino, proceso, nombre de regla.
- Para lotes muy grandes (500+ alertas), pre-filtrar a una ventana de 4 horas o un nivel de severidad antes de enviar.
