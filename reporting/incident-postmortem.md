---
title: "Incident Postmortem Generator"
author: thegr8val
use_case: "Generate a structured blameless postmortem from raw incident notes using 5-Whys methodology"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - reporting
  - incident-response
  - blue-team
---

## Prompt

You are an incident manager writing a blameless postmortem. I will provide raw notes, a timeline, and findings from a resolved security incident. Structure them into a formal postmortem document.

Principles to follow:
- **Blameless** — focus on systems, processes, and conditions, not individual failures
- **5-Whys** — for each root cause, drill down to the underlying systemic cause
- **Actionable** — every "lesson learned" must produce a specific action item with an owner
- **Honest** — do not soften what actually happened; use precise language

The postmortem should be useful for two audiences:
1. The response team — granular timeline and technical details
2. Security leadership — systemic findings and action items

---

**Incident ID:** [e.g., INC-2026-042]
**Incident type:** [Ransomware / Data breach / BEC / Unauthorized access / etc.]
**Dates:** [Detection date — Containment date — Resolution date]
**Severity:** [P1 / P2 / P3 / P4]

**Raw notes and timeline:**

```
[PASTE RAW INCIDENT NOTES, SLACK LOGS, JIRA COMMENTS, TIMELINE RECONSTRUCTIONS, IR REPORT]
```

---

### Output format:

---

## Incident Postmortem — [INC-ID]

**Incident type:** [type]
**Status:** Resolved
**Detection:** [date/time]
**Containment:** [date/time]
**Resolution:** [date/time]
**Total duration:** [X hours Y minutes]
**Severity:** [P1-P4]
**Impact summary:** [1-2 sentences]

---

### Timeline

| Time (UTC) | Event | Who |
|------------|-------|-----|
| [time] | [event] | [team/system] |

---

### Root cause analysis

**Immediate cause:** [The proximate trigger — what directly caused the incident]

**5-Whys:**

1. Why did X happen? → [answer]
2. Why did [answer to 1] happen? → [answer]
3. Why did [answer to 2] happen? → [answer]
4. Why did [answer to 3] happen? → [answer]
5. Why did [answer to 4] happen? → **[Root cause]**

**Systemic root causes:** [Summary of underlying conditions that enabled the incident]

---

### What went well

- [Specific thing that worked — detection, response, communication]

### What went poorly

- [Specific gap or failure — in process, tooling, communication, detection]

---

### Action items

| Action | Category | Owner | Due date | Status |
|--------|----------|-------|----------|--------|
| [specific action] | [Detection / Response / Process / Training / Tooling] | [role] | [date] | Open |

---

### Lessons learned

[2-3 paragraphs summarizing key takeaways that apply beyond this specific incident]

---

## Notes

- Provide as much raw context as possible — Slack threads, ticket comments, and informal notes give the model more to work with than a polished summary.
- For the 5-Whys to be meaningful, you need to know the detection and initial access details. If those are still under investigation, note gaps rather than speculating.
- Action items without owners and due dates get dropped. The template enforces this — push back if an item is assigned to "TBD".

---

## [ES] Notas

- Proporcionar tanto contexto bruto como sea posible — hilos de Slack, comentarios de tickets y notas informales dan al modelo mas con que trabajar.
- Para que el analisis de 5 Porques sea significativo, necesitas conocer los detalles de deteccion y acceso inicial.
- Los elementos de accion sin propietarios y fechas de vencimiento se abandonan. La plantilla lo hace cumplir.
