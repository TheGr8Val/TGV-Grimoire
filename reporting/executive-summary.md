---
title: "Executive Incident Summary"
author: thegr8val
use_case: "Translate a technical incident timeline into a non-technical executive brief"
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

You are a CISO writing an executive brief for senior leadership following a security incident. I will provide a technical incident timeline and findings. Translate this into a clear, non-technical executive summary.

Requirements:
- Write for an audience of C-suite executives and board members with no security background
- Lead with business impact — what was affected, what data or systems were involved
- Explain what happened in plain language, without jargon
- Describe what was done to contain and remediate, in outcome terms (not technical steps)
- State current status clearly: is the incident over, contained, or ongoing?
- List 3-5 specific next steps with ownership and timeframe
- Do NOT speculate on things not supported by evidence
- Tone: factual, calm, authoritative — not alarmist, not dismissive

Length: 400-600 words maximum. Executive time is valuable.

---

**Incident classification:** [e.g., Ransomware / Data breach / Business Email Compromise / Unauthorized access]

**Current status:** [Contained / Ongoing / Remediated / Under investigation]

**Technical timeline and findings:**

```
[PASTE TECHNICAL IR NOTES, TIMELINE, OR FINDINGS REPORT HERE]
```

**Audience:** [Board / C-suite / Legal / Regulator / All of the above]

**Sensitive information to omit:** [e.g., "Do not include specific vulnerability names", "Do not reference ongoing law enforcement contact"]

---

### Output format:

---

**SECURITY INCIDENT BRIEF**
**Classification:** [CONFIDENTIAL / INTERNAL USE]
**Date:** [date]
**Prepared by:** [role]
**Status:** [Contained / Ongoing / Remediated]

---

**What happened**

[Plain-language explanation — 2-3 paragraphs]

**Business impact**

[What was actually affected — systems, data, operations, customers]

**What we did**

[Response actions in outcome language]

**Current status**

[One paragraph: where things stand right now]

**Next steps**

| Action | Owner | Target date |
|--------|-------|-------------|
| [action] | [role/team] | [date] |

---

## Notes

- Strip technical jargon ruthlessly — "threat actor" is fine, "T1059.001 execution via encoded PowerShell" is not.
- If the incident involved customer data, legal and comms teams should review before distribution.
- Pair with `incident-postmortem.md` for the internal technical postmortem document.

---

## [ES] Notas

- Eliminar la jerga tecnica sin piedad — "actor de amenaza" esta bien, "ejecucion T1059.001 via PowerShell codificado" no lo esta.
- Si el incidente involucro datos de clientes, los equipos legal y de comunicaciones deben revisar antes de distribuir.
