---
title: "MITRE ATT&CK Technique Mapping"
author: thegr8val
use_case: "Map plain-language behavior descriptions to ATT&CK technique IDs — returns structured JSON"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - hunting
  - automation
  - api
  - threat-actor
  - malware
---

## Prompt

Map the behaviors described below to MITRE ATT&CK techniques. Return ONLY valid JSON — no prose, no explanation, no markdown.

Rules:
- Use the current ATT&CK Enterprise matrix (v14+)
- Include sub-techniques where applicable (e.g., T1059.001 not just T1059)
- For each technique, assign a confidence: `"high"` (behavior directly maps), `"medium"` (likely but could fit multiple techniques), `"low"` (inferred or partial evidence)
- If a behavior maps to multiple techniques, include all of them
- Do not fabricate technique IDs — if you are unsure, use `"confidence": "low"` and note the uncertainty in `"notes"`

---

**Behaviors to map:**

```
[DESCRIBE EACH BEHAVIOR ON A SEPARATE LINE OR AS A NUMBERED LIST]
```

---

**Output schema:**

```json
{
  "mappings": [
    {
      "behavior": "<original behavior description>",
      "techniques": [
        {
          "technique_id": "Txxxx.xxx",
          "technique_name": "<full name>",
          "tactic": "<tactic name>",
          "confidence": "<high|medium|low>",
          "notes": "<optional: reasoning or caveats>"
        }
      ]
    }
  ]
}
```

---

## Example input

```
1. PowerShell spawned by winword.exe executing a base64-encoded command
2. LSASS memory read by a non-system process
3. Scheduled task created pointing to a file in C:\Users\Public\
4. DNS queries to a domain registered 3 days ago with high entropy subdomain labels
5. Volume shadow copies deleted via vssadmin
```

---

## Example output

```json
{
  "mappings": [
    {
      "behavior": "PowerShell spawned by winword.exe executing a base64-encoded command",
      "techniques": [
        {
          "technique_id": "T1566.001",
          "technique_name": "Phishing: Spearphishing Attachment",
          "tactic": "Initial Access",
          "confidence": "medium",
          "notes": "Word as parent implies document-based delivery; confidence medium as initial access vector is inferred"
        },
        {
          "technique_id": "T1059.001",
          "technique_name": "Command and Scripting Interpreter: PowerShell",
          "tactic": "Execution",
          "confidence": "high",
          "notes": null
        },
        {
          "technique_id": "T1027",
          "technique_name": "Obfuscated Files or Information",
          "tactic": "Defense Evasion",
          "confidence": "high",
          "notes": "Base64 encoding of command line is a direct indicator"
        }
      ]
    }
  ]
}
```

---

## Notes

- Designed for API pipelines: parse the JSON and push directly into MISP, OpenCTI, or a Navigator layer generator.
- Pair with `ioc-extraction.md` to enrich extracted IOCs with technique context before ingesting into a threat intel platform.
- For generating ATT&CK Navigator layer files from this output, pass the JSON to a second prompt or a post-processing script.

---

## [ES] Notas

- Disenado para pipelines de API: parsear el JSON y enviarlo directamente a MISP, OpenCTI, o un generador de capas de Navigator.
- Combinar con `ioc-extraction.md` para enriquecer IOCs extraidos con contexto de tecnicas antes de ingestar en una plataforma de inteligencia.
