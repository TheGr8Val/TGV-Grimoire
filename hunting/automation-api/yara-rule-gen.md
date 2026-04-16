---
title: "YARA Rule Generation"
author: thegr8val
use_case: "Generate a valid YARA rule from malware strings, behavior description, or binary patterns"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - hunting
  - yara
  - malware
  - automation
  - api
---

## Prompt

Generate a valid YARA rule based on the input below. Output ONLY the YARA rule — no prose, no explanation, no markdown code fences.

Requirements:
- Rule name must be snake_case and descriptive
- Include a `meta` section with: `author`, `description`, `date`, `reference` (use "N/A" if none), `hash` (if a sample hash is provided)
- Use `strings` section with meaningful identifiers (`$mz_header`, `$mutex_name`, `$c2_url`, etc.)
- Use condition logic that balances detection coverage with false positive risk
- For PE files, include `uint16(0) == 0x5A4D` (MZ header check) in the condition where appropriate
- If the input suggests a specific malware family, name the rule accordingly

---

**Input type:** [STRINGS / BEHAVIOR DESCRIPTION / HEX PATTERNS / MIXED]

**Sample hash (if available):** [SHA256 or "N/A"]

**Input data:**

```
[PASTE MALWARE STRINGS, BEHAVIOR DESCRIPTION, OR HEX PATTERNS HERE]
```

**False positive context (optional):**

[Any legitimate software that might share these patterns]

---

## Example input

```
Input type: STRINGS + BEHAVIOR DESCRIPTION

Sample hash: 3395856ce81f2b7382dee72602f798b642f14140aafe0b5fa73f73030005e534d

Strings extracted from binary:
- "Mozilla/4.0 (compatible; MSIE 6.0)"  (hardcoded UA — unusual for modern malware)
- "/gate.php"
- "WindowsUpdate"   (mutex name)
- "update.exe"
- C2: "91.107.4.22"

Behavior: Creates mutex "WindowsUpdate", beacons to C2 via HTTP POST to /gate.php,
drops update.exe to AppData\Roaming, establishes Run key persistence.
Likely Emotet or Emotet-inspired loader.
```

---

## Example output

```yara
rule Emotet_Loader_Indicators {
    meta:
        author      = "thegr8val"
        description = "Detects Emotet-inspired loader based on hardcoded mutex, UA string, and C2 beacon path"
        date        = "2026-04-16"
        reference   = "N/A"
        hash        = "3395856ce81f2b7382dee72602f798b642f14140aafe0b5fa73f73030005e534d"

    strings:
        $mz_header   = { 4D 5A }
        $mutex       = "WindowsUpdate" ascii wide
        $ua_string   = "Mozilla/4.0 (compatible; MSIE 6.0)" ascii
        $gate_path   = "/gate.php" ascii
        $dropper_name = "update.exe" ascii nocase

    condition:
        uint16(0) == 0x5A4D and
        filesize < 2MB and
        $mz_header at 0 and
        $mutex and
        ($ua_string or $gate_path) and
        1 of ($dropper_name, $mutex)
}
```

---

## Notes

- Validate generated rules with `yara <rule.yar> <sample>` before deploying to production scanners.
- For hex pattern rules, provide the patterns as `{ XX XX XX ?? XX }` format and specify which offset they appear at if known.
- Be conservative with `condition` logic in wide-deployment scanners — a condition that requires 3+ distinct indicators reduces false positives significantly.
- Do not include IP addresses or domains as YARA strings unless the binary hardcodes them — this creates fragile rules that break when infrastructure rotates.

---

## [ES] Notas

- Validar las reglas generadas con `yara <rule.yar> <muestra>` antes de desplegar en scanners de produccion.
- Ser conservador con la logica de `condition` — requerir 3+ indicadores distintos reduce falsos positivos.
- No incluir IPs o dominios como strings YARA a menos que el binario los tenga hardcodeados.
