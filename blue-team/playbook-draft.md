---
title: "Analyst Response Playbook Draft"
author: thegr8val
use_case: "Generate a structured SOC analyst response playbook for a given alert type or incident scenario"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - blue-team
  - incident-response
  - automation
  - reporting
---

## Prompt

You are a SOC engineer building analyst response playbooks. Based on the alert type and environment below, generate a structured response playbook. The playbook should be executable by a Tier 1 analyst with intermediate experience — it should not require expert judgment to follow, but it should produce expert-quality triage outcomes.

Structure the playbook as a decision tree where possible. Include explicit escalation criteria.

---

**Alert type / scenario:** [e.g., "Possible ransomware pre-encryption activity", "BEC — suspicious email forwarding rule", "Lateral movement detected by EDR", "Privileged account login from new country"]

**SIEM/SOAR platform:** [Splunk / Sentinel / Chronicle / QRadar / None]

**EDR platform:** [CrowdStrike / SentinelOne / Defender XDR / Carbon Black / None]

**Environment context:**

- **OS environment:** [Windows / Linux / macOS / Mixed]
- **Key assets:** [e.g., AD Domain Controllers, critical servers, cloud workloads]
- **On-call escalation path:** [e.g., L1 → L2 → IR Lead → CISO]

---

### Output format:

---

## Playbook: [Alert Type]

**Version:** 1.0 (draft)
**Trigger:** [Exact alert name or condition that activates this playbook]
**Severity:** [Default severity — may change based on triage]
**SLA:** [Target response time]
**Owner:** [SOC Tier / IR Team]

---

### Step 1 — Initial triage (target: < X minutes)

[What to look at first, what questions to answer]

**Queries to run:**

```
[Specific SIEM/EDR queries]
```

**Decision:**
- If [condition A] → proceed to Step 2
- If [condition B] → escalate to L2, proceed to Step 4
- If [condition C] → close as false positive, document reason

---

### Step 2 — [Next investigation phase]

_(steps continue through containment and escalation)_

---

### Escalation criteria

Escalate immediately to L2/IR if ANY of the following are true:
- [ ] [specific condition — e.g., "Evidence of lateral movement to more than 2 hosts"]
- [ ] [specific condition]

---

### Containment actions (L2+)

[Actions that require elevated authorization]

---

### False positive criteria

Document and close if ALL of the following are true:
- [ ] [specific condition]
- [ ] [specific condition]

---

### Evidence to collect before closing or escalating

- [ ] [specific artifact]
- [ ] [specific log or screenshot]

---

## Notes

- Playbooks generated here are first drafts — run them through a tabletop with your team before deploying to production.
- Add your specific host/user allowlists and known-good patterns to the false positive criteria section.
- Pair with `ttx-scenario-builder.md` to test the playbook in a tabletop exercise before it goes live.

---

## [ES] Notas

- Los playbooks generados aqui son borradores iniciales — ejecutarlos a traves de un tabletop con el equipo antes de desplegar en produccion.
- Agregar listas de hosts/usuarios permitidos y patrones conocidos buenos a la seccion de criterios de falsos positivos.
