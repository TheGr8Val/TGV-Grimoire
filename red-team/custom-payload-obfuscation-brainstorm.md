---
title: "Payload Obfuscation Brainstorm (Authorized Engagements)"
author: thegr8val
use_case: "Brainstorm obfuscation and evasion approaches for a given payload type in an authorized red team engagement"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - red-team
  - evasion
  - automation
---

## Prompt

You are a red team operator consulting on payload delivery for an authorized engagement. Based on the engagement scope and target environment below, brainstorm obfuscation and evasion approaches for the described payload. Focus on techniques that are realistic, documented, and appropriate for the stated authorization level.

For each approach:
1. Describe the technique
2. Note which defensive controls it is designed to bypass
3. Flag the OPSEC risk (does it create noisy artifacts or unusual behavior that hunts can catch?)
4. Cite the MITRE ATT&CK technique
5. Note detection difficulty: **Easy / Medium / Hard to detect with current defenses**

Do not generate working exploit code or fully functional malware. Focus on technique selection and approach reasoning.

---

**REQUIRED — Engagement authorization:**

- **Engagement type:** [Red team / Purple team / CTF / Internal research lab]
- **Authorization scope:** [What is authorized — e.g., "Full-scope red team, authorized by CISO, no production DB exfil"]
- **Rules of engagement summary:** [Key constraints]

---

**Target environment:**

- **OS:** [Windows 10/11 / Server 2019/2022 / Linux / macOS]
- **EDR deployed:** [CrowdStrike / SentinelOne / Defender / None / Unknown]
- **AV:** [Windows Defender / Symantec / etc.]
- **Logging:** [Sysmon / Windows Event Logs / EDR telemetry / Unknown]
- **AppLocker/WDAC:** [Enabled / Disabled / Unknown]

**Payload type:** [e.g., staged shellcode loader / PowerShell C2 stager / DLL sideload / macro dropper]

**Delivery vector:** [e.g., spearphishing attachment / USB drop / web drive-by / assumed breach]

---

## Notes

- This prompt requires explicit authorization context. Fill in the engagement fields accurately — vague or absent authorization details will result in generic output.
- Output is technique brainstorming and approach selection, not functional code generation.
- Use the OPSEC risk ratings to choose techniques that match your engagement's noise tolerance — purple team exercises benefit from noisy techniques (generates detection data); covert red teams do not.
- All techniques described are publicly documented in ATT&CK, academic research, or vendor advisories.

---

## [ES] Notas

- Este prompt requiere contexto de autorizacion explicito. Completar los campos de engagement con precision.
- El output es brainstorming de tecnicas y seleccion de enfoque, no generacion de codigo funcional.
- Usar las calificaciones de riesgo OPSEC para elegir tecnicas que coincidan con la tolerancia al ruido del engagement.
