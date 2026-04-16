---
title: "Pentest Findings to Remediation Tickets"
author: thegr8val
use_case: "Convert pentest or assessment findings into prioritized remediation tickets with acceptance criteria"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - reporting
  - red-team
  - blue-team
  - automation
---

## Prompt

You are a security engineer converting pentest findings into actionable remediation tickets for an engineering team. I will provide raw finding descriptions from a security assessment. For each finding, produce a structured ticket that an engineer can pick up and execute without needing to read the full pentest report.

Each ticket must include:
1. **Title** — clear, actionable, under 70 characters
2. **Severity** — Critical / High / Medium / Low (inherit from finding, adjust if needed)
3. **CVSS score** (if applicable) or risk rating rationale
4. **Plain-language description** — what the vulnerability is, in terms an engineer understands
5. **Business impact** — what an attacker could do if this is exploited
6. **Remediation steps** — specific, ordered, actionable steps (not "patch the system")
7. **Acceptance criteria** — how the engineer knows they're done (verifiable, testable)
8. **Validation test** — how security will verify the fix
9. **References** — CVE, CWE, OWASP, or vendor advisory if applicable

Output one ticket block per finding.

---

**Assessment type:** [External pentest / Internal pentest / Web app / Cloud / Red team]

**Target environment:** [Brief description — OS, tech stack, cloud provider if relevant]

**Findings:**

```
[PASTE RAW FINDINGS HERE — one finding per section or numbered list]
```

---

### Output format (per finding):

---

**[SEVERITY] — [TICKET TITLE]**

**Severity:** [Critical / High / Medium / Low]
**Risk rating:** [CVSS score or rationale]

**Description**
[Plain-language explanation of the vulnerability]

**Business impact**
[What an attacker gains from this]

**Remediation steps**
1. [Specific step]
2. [Next step]

**Acceptance criteria**
- [ ] [Verifiable condition 1]
- [ ] [Verifiable condition 2]

**Validation test**
[How the security team will retest — specific test case]

**References**
- [CVE/CWE/OWASP/Advisory]

---

## Notes

- Generic remediation steps ("upgrade to latest version") are not useful. Push the model to be specific about what version, what config change, what code pattern.
- Acceptance criteria should be binary — either done or not done. Avoid subjective criteria ("improve security of X").
- This output is designed for direct import into Jira, Linear, or GitHub Issues — ticket titles and acceptance criteria are written with that in mind.

---

## [ES] Notas

- Los pasos de remediacion genericos ("actualizar a la ultima version") no son utiles. Especificar que version, que cambio de configuracion, que patron de codigo.
- Los criterios de aceptacion deben ser binarios — o completado o no completado.
- Este output esta disenado para importacion directa en Jira, Linear, o GitHub Issues.
