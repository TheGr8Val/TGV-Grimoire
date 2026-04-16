# TGV-Grimoire

<p align="center">
  <img src="./assets/grimoire-cover.png" alt="TGV-Grimoire" width="220" />
</p>

> A bilingual cybersecurity prompt library by [TheGr8Val](https://github.com/thegr8val)

**TGV-Grimoire** is a curated collection of LLM prompts engineered for cybersecurity practitioners — analysts, hunters, and engineers who want to leverage AI models in their workflows without reinventing the wheel every time.

Every prompt is battle-tested, documented with metadata, and designed to be immediately useful in real environments.

---

## Modules

| Module | Prompts | Description | Status |
|--------|---------|-------------|--------|
| [`/hunting`](./hunting/) | 11 | Threat hunting — IOC triage, actor profiling, log analysis, Sigma/YARA/KQL/SPL generation | Active |
| [`/malware-analysis`](./malware-analysis/) | 3 | String deobfuscation, C2 fingerprinting, packer identification | Active |
| [`/red-team`](./red-team/) | 3 | Tabletop exercises, detection gap analysis, payload obfuscation brainstorm | Active |
| [`/osint`](./osint/) | 3 | Passive recon checklists, persona analysis, lookalike domain generation | Active |
| [`/reporting`](./reporting/) | 3 | Executive summaries, remediation tickets, incident postmortems | Active |
| [`/blue-team`](./blue-team/) | 3 | Detection rule review, analyst playbooks, crown jewels mapping | Active |

---

## How prompts are organized

Each module contains two categories:

- **`llm-analysis/`** — Prompts designed for direct LLM interaction (ChatGPT, Claude, Gemini, etc.). Feed these data, ask questions, get structured analysis.
- **`automation-api/`** — Prompts engineered for programmatic use via API. Optimized for consistent, parseable output (JSON, YAML, Sigma, etc.).

---

## Prompt metadata format

Every prompt file starts with a YAML metadata header:

```yaml
---
title: "Prompt title"
author: thegr8val
use_case: "Short description of the use case"
model_tested:
  - claude-sonnet-4-6
  - gpt-4o
language: EN/ES
tags:
  - hunting
  - ioc
  - automation
---
```

---

## Usage

Clone the repo and use prompts directly:

```bash
git clone https://github.com/thegr8val/TGV-Grimoire.git
cd TGV-Grimoire/hunting/llm-analysis
```

Copy a prompt, substitute the `[PLACEHOLDER]` values with your data, and send it to your model of choice.

---

## Contributing

Contributions are welcome. See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

---

## [ES] Descripcion

**TGV-Grimoire** es una coleccion bilingue de prompts de ciberseguridad para analistas, hunters e ingenieros que quieren aprovechar modelos de IA en sus flujos de trabajo.

Cada prompt incluye metadatos (autor, caso de uso, modelo probado, idioma, etiquetas) y esta listo para usarse en entornos reales.

Los placeholders se indican con `[MAYUSCULAS_EN_CORCHETES]`.

---

## License

[MIT](./LICENSE) — TheGr8Val, 2026
