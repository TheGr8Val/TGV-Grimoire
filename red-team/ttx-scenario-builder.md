---
title: "Tabletop Exercise Scenario Builder"
author: thegr8val
use_case: "Build a structured tabletop exercise scenario for a given threat actor and target organization profile"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - red-team
  - tabletop
  - threat-actor
  - blue-team
---

## Prompt

You are a security exercise designer. Build a tabletop exercise (TTX) scenario based on the organization profile and threat actor below. The scenario should be realistic, grounded in actual TTP patterns, and structured to test specific response capabilities.

The scenario must include:
1. **Narrative setup** — realistic backstory and initial conditions
2. **Inject sequence** — 5-8 timed injects that escalate the scenario
3. **Decision points** — at each inject, what decisions does each team need to make
4. **Discussion questions** — for each inject, 2-3 questions to drive team discussion
5. **Expected response actions** — what good looks like at each stage
6. **Learning objectives** — what the exercise is designed to surface

Keep the injects realistic and grounded in the threat actor's actual TTPs. Do not make the scenario cartoonishly obvious — build ambiguity where attackers actually create ambiguity.

---

**Authorized exercise scope:** [DESCRIBE THE AUTHORIZED SCOPE OF THIS EXERCISE]

**Organization profile:**

- **Sector:** [e.g., Healthcare, Finance, Energy]
- **Size:** [employees, locations]
- **Crown jewels:** [most critical data/systems]
- **Current security posture summary:** [e.g., mature SOC, no EDR, limited logging]

**Threat actor:** [NAME OR DESCRIBE THE ADVERSARY — e.g., "ransomware affiliate using LockBit 3.0 TTPs", "APT actor targeting energy sector"]

**Teams participating:** [e.g., SOC, IR, Legal, Executive, IT Ops, PR/Comms]

**Exercise duration:** [e.g., 4-hour tabletop]

**Primary capability to test:** [e.g., incident escalation, ransomware response, supply chain compromise detection]

---

## Example input

```
Authorized exercise scope: Internal tabletop, no live systems involved

Organization profile:
- Sector: Regional bank, 3,500 employees
- Crown jewels: Core banking system (FIS), SWIFT gateway, customer PII
- Security posture: Splunk SIEM, no EDR on legacy servers, MFA on VPN but not internal

Threat actor: FIN7-inspired financially motivated actor conducting spearphishing
  followed by hands-on-keyboard operations targeting banking credentials

Teams participating: SOC, IR, Legal, CISO, IT Ops
Exercise duration: 4 hours
Primary capability to test: Escalation procedures and crisis communication
```

---

## Notes

- The inject sequence should be distributed across the exercise duration with escalating severity.
- Include at least one inject that tests an organizational gap (communication breakdown, unclear ownership, missing runbook).
- Decision points should be genuinely ambiguous — the right answer should require discussion, not be obvious.
- This output works well as a starting template; customize inject details for your specific environment before running.

---

## [ES] Notas

- La secuencia de injects debe distribuirse a lo largo de la duracion del ejercicio con severidad escalante.
- Incluir al menos un inject que pruebe una brecha organizacional (fallo de comunicacion, responsabilidad poco clara).
- Los puntos de decision deben ser genuinamente ambiguos — la respuesta correcta debe requerir discusion.
