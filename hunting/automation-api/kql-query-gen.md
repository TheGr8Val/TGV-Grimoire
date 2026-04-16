---
title: "KQL Query Generation (Microsoft Sentinel / Defender)"
author: thegr8val
use_case: "Generate a KQL query from a hunting hypothesis for Microsoft Sentinel or Defender XDR"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - hunting
  - kql
  - automation
  - api
  - log-analysis
  - blue-team
---

## Prompt

Generate a KQL query based on the hunting hypothesis below. Output ONLY the KQL query — no prose, no explanation, no markdown code fences.

Requirements:
- Use the correct table names for the specified platform (Sentinel or Defender XDR)
- Apply the time range using `| where TimeGenerated > ago(Xd)` or the specified window
- Use `summarize`, `project`, or `extend` to produce actionable, readable output — not raw event dumps
- Add `| order by TimeGenerated desc` unless aggregation makes ordering irrelevant
- Where applicable, use `| join` or `| union` to correlate across tables
- Use `// comment` lines to annotate non-obvious logic steps

---

**Platform:** [Microsoft Sentinel | Defender XDR | Both]

**Primary table(s):** [e.g., SecurityEvent, DeviceProcessEvents, SigninLogs, OfficeActivity, CommonSecurityLog]

**Time range:** [e.g., last 14 days | 2026-04-01 to 2026-04-15]

**Hypothesis:**

[DESCRIBE WHAT YOU ARE HUNTING FOR IN PLAIN LANGUAGE]

**Known good to exclude (optional):**

[Accounts, hosts, or patterns to filter out]

---

## Example input

```
Platform: Microsoft Sentinel
Primary table: SecurityEvent, SigninLogs
Time range: last 30 days

Hypothesis:
Hunt for accounts that had a successful login from a new country/region they've never
logged in from before, within 24 hours of a password reset event. This could indicate
account takeover after credential stuffing.

Known good to exclude:
ServiceAccount_* accounts — these use automation from fixed IPs and generate false positives.
```

---

## Example output

```kql
// Step 1: Get all password reset events in the window
let PasswordResets = SecurityEvent
| where TimeGenerated > ago(30d)
| where EventID == 4723 or EventID == 4724
| project ResetTime = TimeGenerated, ResetAccount = tolower(TargetUserName);

// Step 2: Get sign-in locations per account (historical baseline — 90 days)
let HistoricalCountries = SigninLogs
| where TimeGenerated > ago(90d)
| where ResultType == 0
| summarize KnownCountries = make_set(Location) by UserPrincipalName = tolower(UserPrincipalName);

// Step 3: Get post-reset logins and check for new countries
SigninLogs
| where TimeGenerated > ago(30d)
| where ResultType == 0
| where UserPrincipalName !startswith "serviceaccount_"
| extend UPN = tolower(UserPrincipalName)
| join kind=inner PasswordResets on $left.UPN == $right.ResetAccount
| where TimeGenerated between (ResetTime .. (ResetTime + 1d))
| join kind=leftouter HistoricalCountries on $left.UPN == $right.UserPrincipalName
| where not(Location in (KnownCountries))
| project TimeGenerated, UPN, Location, IPAddress, AppDisplayName, ResetTime
| order by TimeGenerated desc
```

---

## Notes

- Sentinel and Defender XDR use different table schemas. Specify the platform — common mixups: `DeviceProcessEvents` (Defender) vs `SecurityEvent` (Sentinel).
- For complex joins on large tables, add `| take 10000` during testing to avoid query timeouts.
- KQL `join` is expensive — filter both sides as much as possible before joining.
- The `ago()` function accepts `d` (days), `h` (hours), `m` (minutes).

---

## [ES] Notas

- Sentinel y Defender XDR usan esquemas de tablas diferentes. Especificar la plataforma.
- Para joins complejos en tablas grandes, agregar `| take 10000` durante pruebas para evitar timeouts.
- El `join` de KQL es costoso — filtrar ambos lados lo mas posible antes de unir.
