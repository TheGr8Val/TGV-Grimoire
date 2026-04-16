---
title: "Splunk SPL Query Generation"
author: thegr8val
use_case: "Generate a Splunk SPL query from a natural language hunting hypothesis"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - hunting
  - splunk
  - automation
  - api
  - log-analysis
---

## Prompt

Generate a Splunk SPL query based on the hunting hypothesis below. Output ONLY the SPL query — no prose, no explanation, no markdown code fences.

Requirements:
- Use the index and sourcetype specified
- Include a time range filter using `earliest` and `latest` if provided
- Add a `| table` or `| stats` command at the end to produce actionable output
- Use `rex` or `eval` for field extraction only if the field is not natively parsed
- Prefer `stats count` over raw event listings for high-volume sources
- Comment lines with ```` ``` ```` prefix if you need to annotate logic steps (Splunk ignores these)

---

**Index:** [SPECIFY OR USE `index=*`]

**Sourcetype:** [SPECIFY: WinEventLog:Security | XmlWinEventLog:Microsoft-Windows-Sysmon/Operational | stream:http | pan:traffic | etc.]

**Time range:** [e.g., last 7 days | 2026-04-01 to 2026-04-15 | leave blank for no filter]

**Hypothesis:**

[DESCRIBE WHAT YOU ARE HUNTING FOR IN PLAIN LANGUAGE]

**Known good to exclude (optional):**

[ACCOUNTS, HOSTS, OR PATTERNS TO FILTER OUT]

---

## Example input

```
Index: index=windows
Sourcetype: XmlWinEventLog:Microsoft-Windows-Sysmon/Operational
Time range: last 7 days

Hypothesis:
Hunt for PowerShell processes spawned by Office applications (Word, Excel, Outlook).
This could indicate malicious macro execution. I want to see the parent process,
child process, command line, and the host where it occurred.

Known good to exclude:
Hosts matching "IT-AUTO-*" run legitimate automation.
```

---

## Example output

```
index=windows sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational"
earliest=-7d
EventCode=1
ParentImage IN ("*\\WINWORD.EXE", "*\\EXCEL.EXE", "*\\OUTLOOK.EXE", "*\\POWERPNT.EXE")
Image IN ("*\\powershell.exe", "*\\pwsh.exe", "*\\cmd.exe")
NOT host="IT-AUTO-*"
| table _time, host, user, ParentImage, Image, CommandLine, ParentCommandLine
| sort -_time
```

---

## Notes

- Always test generated queries against a small time window first before running across large indexes.
- If your environment uses CIM-compliant data models, ask the model to rewrite the query using `datamodel` instead of raw sourcetype searches for better portability.
- For KQL (Microsoft Sentinel) or ESQL (Elastic), swap this prompt's instructions accordingly — the hypothesis format is the same.

---

## [ES] Notas

- Siempre prueba las consultas generadas contra una ventana de tiempo pequena antes de ejecutar en indices grandes.
- Si tu entorno usa modelos de datos compatibles con CIM, pide al modelo reescribir la consulta usando `datamodel` para mejor portabilidad.
- Para KQL (Microsoft Sentinel) o ESQL (Elastic), ajusta las instrucciones del prompt — el formato de hipotesis es el mismo.
