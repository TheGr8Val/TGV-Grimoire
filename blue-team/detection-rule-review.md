---
title: "Detection Rule Review"
author: thegr8val
use_case: "Review an existing Sigma, KQL, or SPL detection rule for logic gaps, false positive risk, and coverage quality"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - blue-team
  - detection-engineering
  - sigma
  - kql
  - splunk
---

## Prompt

You are a senior detection engineer conducting a peer review of a detection rule. I will provide the rule and its intent. Review it for:

1. **Logic correctness** — does the rule do what it claims to detect?
2. **False positive risk** — what legitimate activity could trigger this? How often?
3. **Coverage gaps** — what variations of the attack would this miss?
4. **Performance** — any inefficient patterns that would cause SIEM performance issues?
5. **Field accuracy** — are the field names correct for the stated log source?
6. **Condition logic** — is the condition tight enough, or too broad/narrow?
7. **Sigma compliance** (if Sigma) — does it follow the spec?

Provide a specific, improved version of the rule if significant issues are found. Do not rewrite it for style alone — only change what has a real quality or correctness impact.

---

**Rule type:** [Sigma / KQL / Splunk SPL / ESQL / Other]

**Intended detection:** [One sentence — what this rule is meant to catch]

**Log source / platform:** [e.g., Sysmon process_creation / Windows Security Event / Microsoft Sentinel SigninLogs]

**Rule:**

```
[PASTE THE RULE HERE]
```

**Environment context (optional):** [Anything that affects expected false positive rate — e.g., "Dev team runs PowerShell scripts frequently", "All workstations have CrowdStrike EDR"]

---

### Output format:

#### Review Summary

**Overall quality:** [Pass / Needs minor revision / Needs major revision]

---

#### Issues found

| # | Category | Severity | Description |
|---|----------|----------|-------------|
| 1 | [Logic / FP Risk / Coverage / Performance / Field / Compliance] | [Critical/High/Medium/Low] | [description] |

---

#### Detailed findings

**Issue 1 — [title]**
[Detailed explanation and recommended fix]

---

#### Improved rule (if applicable)

```
[IMPROVED RULE HERE]
```

---

#### False positive scenarios

| Scenario | Likelihood | Mitigation |
|----------|------------|------------|
| [specific FP scenario] | [High/Med/Low] | [how to reduce — filter, allowlist, additional condition] |

---

## Notes

- For Sigma rules, the model checks against the official Sigma specification and common SIEM backend requirements.
- For KQL, note whether you're targeting Sentinel vs Defender XDR — table schemas differ.
- The model will not invent field names to fix issues — if a field is wrong, it will tell you what the correct field should be and where to verify.

---

## [ES] Notas

- Para reglas Sigma, el modelo verifica contra la especificacion oficial y los requisitos comunes de backend SIEM.
- Para KQL, indicar si el objetivo es Sentinel o Defender XDR — los esquemas de tablas difieren.
