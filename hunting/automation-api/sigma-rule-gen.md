---
title: "Sigma Rule Generation"
author: thegr8val
use_case: "Generate a valid Sigma detection rule from a behavior description or log evidence"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - hunting
  - sigma
  - automation
  - api
  - blue-team
---

## Prompt

Generate a valid Sigma detection rule based on the behavior described below. Follow the official Sigma specification strictly. Output ONLY the YAML — no prose, no explanation, no markdown code fences.

Requirements:
- Use correct Sigma field names for the specified log source
- Set `status` to `experimental`
- Set `level` based on the severity of the behavior (low/medium/high/critical)
- Include at least one `falsepositives` entry
- Use `condition` logic that minimizes false positives where possible
- Add relevant `tags` from the MITRE ATT&CK framework (attack.tXXXX format)

---

**Log source:** [SPECIFY: windows/sysmon | windows/security | zeek/dns | proxy | linux/auditd | etc.]

**Behavior to detect:**

[DESCRIBE THE BEHAVIOR IN PLAIN LANGUAGE — what process, what action, what indicators]

**Known false positive context (optional):**

[ANY LEGITIMATE USE CASES THAT COULD TRIGGER THIS RULE]

---

## Example input

```
Log source: windows/sysmon

Behavior to detect:
PowerShell spawning from Microsoft Word (winword.exe). Child process is powershell.exe
or pwsh.exe. This is a common malicious macro execution pattern.

Known false positives:
Some internal automation scripts use Word macros to launch PowerShell legitimately
in the IT department.
```

---

## Example output

```yaml
title: PowerShell Spawned by Microsoft Word
id: a7f3b2c1-4e5d-4f6a-8b9c-0d1e2f3a4b5c
status: experimental
description: Detects PowerShell being spawned as a child process of Microsoft Word, a common indicator of malicious macro execution.
references:
  - https://attack.mitre.org/techniques/T1566/001/
author: thegr8val
date: 2026-04-16
tags:
  - attack.execution
  - attack.t1059.001
  - attack.initial_access
  - attack.t1566.001
logsource:
  category: process_creation
  product: windows
detection:
  selection:
    ParentImage|endswith: '\WINWORD.EXE'
    Image|endswith:
      - '\powershell.exe'
      - '\pwsh.exe'
  condition: selection
falsepositives:
  - Legitimate IT automation using Word macros to invoke PowerShell (allowlist by ParentCommandLine or user)
level: high
```

---

## Notes

- Always validate generated rules with `sigma check` before deploying to production.
- The model occasionally uses non-standard field names. Cross-reference against the Sigma taxonomy for your target SIEM.
- For complex conditions (aggregations, timeframes), provide explicit examples of matching and non-matching log lines.

---

## [ES] Notas

- Siempre valida las reglas generadas con `sigma check` antes de desplegar en produccion.
- El modelo ocasionalmente usa nombres de campo no estandar. Verificar contra la taxonomia Sigma para el SIEM objetivo.
- Para condiciones complejas (agregaciones, ventanas de tiempo), proporciona ejemplos explicitos de logs que deben y no deben coincidir.
