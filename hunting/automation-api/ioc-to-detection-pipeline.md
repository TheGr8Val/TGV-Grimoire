---
title: "IOC to Detection Pipeline — Sigma + YARA in One Pass"
author: thegr8val
use_case: "Given a set of IOCs and behavior context, generate both a Sigma rule and a YARA rule in one prompt"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - hunting
  - sigma
  - yara
  - automation
  - api
  - ioc
---

## Prompt

I will provide a set of IOCs and behavioral context for a malware sample or threat actor campaign. Generate two detection artifacts:

1. A **Sigma rule** for log-based detection (SIEM/EDR telemetry)
2. A **YARA rule** for file/memory-based detection

Output ONLY the two rules separated by the delimiter `---YARA---`. No prose, no explanation, no markdown code fences.

Format:
```
<sigma rule YAML here>
---YARA---
<yara rule here>
```

Requirements for the Sigma rule:
- Valid Sigma YAML per official specification
- `status: experimental`
- Appropriate `logsource` for the behaviors described
- At least one `falsepositives` entry
- MITRE ATT&CK `tags`

Requirements for the YARA rule:
- Valid YARA syntax
- `meta` section with author, description, date, hash (if provided)
- Meaningful string identifiers
- Condition that checks `uint16(0) == 0x5A4D` if PE-based
- Balance detection coverage vs false positive risk

---

**Sample hash (if available):** [SHA256 or "N/A"]

**Campaign/malware name (if known):** [Name or "Unknown"]

**IOCs:**

```
[PASTE IOC LIST — domains, IPs, file hashes, mutex names, registry keys, file paths, strings]
```

**Behavioral context:**

```
[DESCRIBE WHAT THE MALWARE DOES — delivery, execution, persistence, C2, exfiltration]
```

---

## Example input

```
Sample hash: 3395856ce81f2b7382dee72602f798b642f14140aafe0b5fa73f73030005e534d
Campaign: Emotet-inspired loader, Q1 2026

IOCs:
- Mutex: WindowsUpdate
- C2: 91.107.4.22:8080, update-service[.]com
- C2 URI: /gate.php
- Dropper path: C:\Users\<user>\AppData\Roaming\update.exe
- Hardcoded UA: Mozilla/4.0 (compatible; MSIE 6.0)
- Registry persistence: HKCU\Software\Microsoft\Windows\CurrentVersion\Run\SvcUpdate

Behavioral context:
Malicious Word document spawns PowerShell which downloads and executes the dropper.
Dropper creates mutex WindowsUpdate, establishes Run key persistence, and beacons
to C2 via HTTP POST to /gate.php using an outdated IE6 user-agent string.
```

---

## Notes

- Parse the output by splitting on `---YARA---` to get the two artifacts separately.
- Validate both rules before deployment: `sigma check` for the Sigma rule, `yara <rule> <sample>` for YARA.
- When behavioral context and IOCs conflict (e.g., IOC is a domain but the Sigma rule covers process behavior), the model will generate complementary rules — the Sigma rule covers process/log evidence and the YARA rule covers the binary.

---

## [ES] Notas

- Parsear el output dividiendo por `---YARA---` para obtener los dos artefactos por separado.
- Validar ambas reglas antes del despliegue: `sigma check` para Sigma, `yara <rule> <muestra>` para YARA.
- Si el contexto de comportamiento y los IOCs son complementarios, el modelo generara reglas que cubren ambos vectores de deteccion.
