---
title: "IOC Extraction from Unstructured Text"
author: thegr8val
use_case: "Extract and classify IOCs from threat reports, emails, or unstructured text — returns structured JSON"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - hunting
  - ioc
  - extraction
  - automation
  - api
---

## Prompt

Extract all indicators of compromise (IOCs) from the text below. Return ONLY valid JSON — no prose, no explanation, no markdown.

Rules:
- Defang all IPs, domains, and URLs in the output (replace `.` with `[.]` and `http` with `hxxp`)
- Classify each IOC by type: `ip`, `domain`, `url`, `md5`, `sha1`, `sha256`, `email`, `registry_key`, `file_path`, `mutex`, `other`
- If context about the IOC's purpose is available in the text, include it in the `context` field; otherwise use `null`
- Deduplicate — include each unique value only once
- If no IOCs are found, return `{"iocs": []}`

---

**Text:**

```
[PASTE THREAT REPORT, EMAIL BODY, BLOG POST, OR OTHER UNSTRUCTURED TEXT HERE]
```

---

**Output schema:**

```json
{
  "iocs": [
    {
      "type": "<ip|domain|url|md5|sha1|sha256|email|registry_key|file_path|mutex|other>",
      "value": "<defanged value>",
      "context": "<purpose or association, or null>"
    }
  ]
}
```

---

## Example input

```
The actor leveraged update-service[.]com for command and control, with traffic going to
185.220.101.45 over port 443. The dropper has SHA256 hash
3395856ce81f2b7382dee72602f798b642f14140aafe0b5fa73f73030005e534d
and was downloaded from hxxps://cdn.delivery-net[.]ru/update.bin.
Persistence was established via HKCU\Software\Microsoft\Windows\CurrentVersion\Run\SvcUpdate.
Contact email observed: recon@threat-actor[.]io
```

---

## Example output

```json
{
  "iocs": [
    {
      "type": "domain",
      "value": "update-service[.]com",
      "context": "Command and control"
    },
    {
      "type": "ip",
      "value": "185[.]220[.]101[.]45",
      "context": "C2 server, port 443"
    },
    {
      "type": "sha256",
      "value": "3395856ce81f2b7382dee72602f798b642f14140aafe0b5fa73f73030005e534d",
      "context": "Dropper hash"
    },
    {
      "type": "url",
      "value": "hxxps://cdn[.]delivery-net[.]ru/update.bin",
      "context": "Dropper download URL"
    },
    {
      "type": "registry_key",
      "value": "HKCU\\Software\\Microsoft\\Windows\\CurrentVersion\\Run\\SvcUpdate",
      "context": "Persistence mechanism"
    },
    {
      "type": "email",
      "value": "recon@threat-actor[.]io",
      "context": "Actor contact email"
    }
  ]
}
```

---

## Notes

- Designed for API use. Pipe the JSON output directly into MISP, OpenCTI, or a custom enrichment pipeline.
- The model respects already-defanged IOCs in the input and will preserve or normalize defanging in the output.
- For very long reports (10,000+ words), split into sections and merge the JSON arrays programmatically.
- Test the output schema with a JSON validator before trusting it in automated pipelines.

---

## [ES] Notas

- Disenado para uso via API. El output JSON se puede pasar directamente a MISP, OpenCTI, o un pipeline de enriquecimiento propio.
- El modelo respeta IOCs ya defensivizados en el input y normaliza el defensivizado en el output.
- Para reportes muy largos (10,000+ palabras), dividir en secciones y fusionar los arrays JSON programaticamente.
