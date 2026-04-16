---
title: "Lateral Movement Timeline Reconstruction"
author: thegr8val
use_case: "Reconstruct an attacker's lateral movement path from auth, process, and network events"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - hunting
  - lateral-movement
  - log-analysis
  - triage
  - blue-team
---

## Prompt

You are an incident responder reconstructing attacker lateral movement from log evidence. I will provide authentication, process creation, and/or network connection events across multiple hosts.

Your task:
1. Identify the likely initial foothold (first compromised host)
2. Reconstruct the movement path between hosts in chronological order
3. Flag the techniques used for each hop (MITRE ATT&CK)
4. Identify which accounts were used or compromised at each step
5. Highlight any gaps in the timeline where activity is inferred but not directly evidenced

Output a structured timeline followed by a movement graph in text form.

---

**Log sources provided:** [LIST SOURCES: e.g., Windows Security 4624/4648, Sysmon 3, VPN logs]

**Hosts in scope:** [LIST HOSTNAMES/IPs IF KNOWN]

**Time range:** [START — END UTC]

**Log data:**

```
[PASTE EVENTS HERE — include timestamp, host, event type, user, source IP, destination]
```

---

### Output format:

#### Timeline

| Time (UTC) | Source Host | Dest Host | Account | Method | MITRE | Confidence |
|------------|-------------|-----------|---------|--------|-------|------------|
| [timestamp] | [host] | [host] | [user] | [technique] | [Txxxx] | [High/Med/Low] |

---

#### Movement graph

```
[INITIAL_HOST] --[technique]--> [HOP_1] --[technique]--> [HOP_2]
                                    |
                                    +--[technique]--> [HOP_3]
```

---

#### Accounts compromised or abused

| Account | Type | Hosts accessed | Notes |
|---------|------|----------------|-------|
| [user] | [Domain/Local/Service] | [list] | [note] |

---

#### Timeline gaps

[List any hops that are inferred but not directly evidenced, and what log sources would confirm them.]

---

#### Analyst assessment

[2-3 sentences: overall movement pattern, attacker's apparent objective, recommended containment scope.]

---

## Example input

```
[Log sources: Windows Security EventLog]
[Hosts: WS-SALES01, WS-IT02, DC01]
[Time range: 2026-04-10 03:00 — 04:30 UTC]

03:12:44 WS-SALES01 EventID=4624 user=jsmith logon_type=10 src=10.0.1.44
03:14:02 WS-SALES01 EventID=4648 user=jsmith target_user=administrator target_host=WS-IT02
03:14:55 WS-IT02    EventID=4624 user=administrator logon_type=3 src=WS-SALES01
03:22:11 WS-IT02    EventID=4648 user=administrator target_user=svc_backup target_host=DC01
03:23:04 DC01       EventID=4624 user=svc_backup logon_type=3 src=WS-IT02
03:45:17 DC01       EventID=4624 user=svc_backup logon_type=3 src=WS-IT02
```

---

## Notes

- Works best when you include raw log lines rather than pre-summarized data — the model can reason about timing and technique from raw events.
- Logon type codes matter: include them if available (type 3 = network, type 10 = remote interactive, type 2 = interactive).
- If you have Sysmon network events (Event ID 3), include them — they often bridge gaps between auth events on different hosts.

---

## [ES] Notas

- Funciona mejor con lineas de log crudas en lugar de datos pre-resumidos.
- Los codigos de tipo de inicio de sesion son importantes: incluirlos si estan disponibles.
- Los eventos de red de Sysmon (Event ID 3) ayudan a conectar gaps entre eventos de autenticacion.
