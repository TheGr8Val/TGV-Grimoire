# Contributing to TGV-Grimoire

Thanks for helping grow the Grimoire. Contributions from practitioners in the field make this more useful for everyone.

---

## What belongs here

- Prompts you've actually used in real or lab environments
- Prompts that produce reliable, structured output
- Prompts that solve a concrete problem (not demos or toys)

Do NOT submit:
- Prompts designed to bypass LLM safety measures
- Prompts that rely on jailbreaks or unethical techniques
- Proprietary data or client-specific context

---

## File naming convention

Use lowercase, hyphen-separated names that describe the use case:

```
threat-actor-profiling.md
sigma-rule-gen.md
log-triage-splunk.md
```

---

## Required metadata header

Every prompt file must start with this YAML block:

```yaml
---
title: "Human-readable title"
author: your_handle
use_case: "One sentence describing what this prompt does"
model_tested:
  - model-name-version
language: EN          # EN, ES, or EN/ES for bilingual
tags:
  - tag1
  - tag2
---
```

**`model_tested`** — list every model you've confirmed works well. If untested on a model, don't list it.

**`tags`** — use existing tags when possible (see below). Add new ones only if nothing fits.

### Existing tags

`hunting` `ioc` `threat-actor` `malware` `log-analysis` `sigma` `yara` `splunk` `kql` `automation` `api` `enrichment` `triage` `reporting` `red-team` `blue-team` `osint`

---

## Prompt body format

Structure your prompt file like this:

```markdown
## Prompt

[The actual prompt text. Use [PLACEHOLDER] for values the user must supply.]

---

## Example input

[A sanitized or fictional example of what you'd pass to the model.]

---

## Example output

[A sample of what a good response looks like — trimmed if long.]

---

## Notes

[Optional: caveats, model quirks, tips for best results.]

---

## [ES] Notas

[Optional Spanish notes or translation of the Notes section.]
```

---

## Submitting

1. Fork the repo
2. Add your file to the correct module/category folder
3. Open a PR with a short description of what the prompt does and where you've used it
4. A maintainer will review for quality and ethics before merging

---

## [ES] Contribuir

Sigue el formato de metadatos y estructura del cuerpo descritos arriba. Los PRs deben incluir al menos un ejemplo de entrada y salida. Las notas en espanol son bienvenidas en la seccion `[ES] Notas`.

---

## Code of conduct

Be professional. This is a tool for defenders and researchers. Maintain that standard in every contribution and discussion.
