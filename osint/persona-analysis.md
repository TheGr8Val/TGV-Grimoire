---
title: "Social Media Persona Authenticity Analysis"
author: thegr8val
use_case: "Analyze a social media persona for indicators of sock puppet, bot, or coordinated inauthentic behavior"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - osint
  - threat-actor
  - fraud
  - social-engineering
---

## Prompt

You are an OSINT analyst specializing in influence operations and social media investigations. I will provide data about a social media persona. Analyze it for indicators of inauthenticity: sock puppets, bot accounts, hired personas, or coordinated inauthentic behavior (CIB).

Assess the following dimensions:
1. **Account creation and history patterns** — age vs. activity, gaps, sudden spikes
2. **Content patterns** — repetitive narratives, copy-paste across accounts, unnatural posting cadence
3. **Network patterns** — who they follow/are followed by, mutual amplification clusters
4. **Identity consistency** — profile photo analysis (AI-generated indicators), bio changes, username history
5. **Behavioral anomalies** — posting at unusual hours for stated timezone, language inconsistencies
6. **Amplification patterns** — whether the account is a source, amplifier, or both

For each indicator: note the evidence, assess significance, and flag confidence.

---

**Platform:** [Twitter/X / LinkedIn / Facebook / Instagram / Telegram / Other]

**Persona data:**

```
[PASTE: username, bio, account creation date, follower/following counts, post frequency,
sample posts (5-10), mutual connections if known, profile description, any other metadata]
```

**Context (optional):** [Why this persona is under investigation — e.g., "Appeared in spearphishing campaign", "Amplifying disinfo around [topic]", "Used in social engineering targeting our employees"]

---

### Output format:

#### Persona Assessment

**Authenticity assessment:** [Likely authentic / Suspicious / Likely inauthentic / Confirmed inauthentic]
**Primary concern:** [Bot / Sock puppet / Hired persona / Coordinated amplifier / Unknown]
**Confidence:** [High / Medium / Low]

---

#### Indicator summary

| Dimension | Finding | Significance | Confidence |
|-----------|---------|--------------|------------|
| [dimension] | [what was found] | [why it matters] | [H/M/L] |

---

#### Analyst notes

[Gaps in available data, alternative hypotheses, recommended additional investigation steps]

---

## Notes

- The model cannot access live social media data — paste the data you've collected manually or via API.
- Profile photo AI-generation analysis requires visual inspection tools (Hive Moderation, AI or Not, FotoForensics) — the model can interpret your findings but cannot analyze images in this prompt format.
- Treat output as investigative leads, not definitive attribution. Coordinate with platform trust & safety teams for confirmed CIB.

---

## [ES] Notas

- El modelo no puede acceder a datos de redes sociales en vivo — pegar los datos recopilados manualmente o via API.
- El analisis de generacion de fotos de perfil por IA requiere herramientas de inspeccion visual especializadas.
- Tratar el output como pistas de investigacion, no como atribucion definitiva.
