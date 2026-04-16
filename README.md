# TGV-Grimoire

<p align="center">
  <img src="./assets/grimoire-cover.png" alt="TGV-Grimoire" width="220" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/prompts-26-blue?style=flat-square" />
  <img src="https://img.shields.io/badge/modules-6-blueviolet?style=flat-square" />
  <img src="https://img.shields.io/badge/language-EN%20%2F%20ES-teal?style=flat-square" />
  <img src="https://img.shields.io/badge/license-MIT-green?style=flat-square" />
  <a href="https://buymeacoffee.com/thegr8val">
    <img src="https://img.shields.io/badge/Buy%20Me%20A%20Coffee-support-yellow?style=flat-square"/>
  </a>
</p>

<p align="center">
  <em>A bilingual cybersecurity prompt library by <a href="https://github.com/TheGr8Val">TheGr8Val</a></em>
</p>

---

## About

**TGV-Grimoire** is a curated collection of LLM prompts engineered for cybersecurity practitioners — analysts, threat hunters, detection engineers, and red teamers who want to leverage AI models in their daily workflows without reinventing the wheel every time.

Every prompt is:
- 🧪 **Battle-tested** in real or lab environments
- 🗂️ **Documented with metadata** — author, use case, model tested, language, tags
- 🔁 **Ready to use** — fill in the `[PLACEHOLDERS]` and send to your model of choice
- 🌐 **Bilingual** — English primary, Spanish sections labeled `[ES]`

Two types of prompts in every module:
- 💬 **`llm-analysis/`** — For direct LLM chat interaction. Feed data, get structured analysis.
- ⚙️ **`automation-api/`** — For programmatic API use. Output is JSON, YAML, Sigma, KQL, SPL — no prose.

---

## 🗂️ Modules

| Module | Prompts | Description |
|--------|:-------:|-------------|
| 🎯 [`/hunting`](./hunting/) | **11** | Threat hunting — IOC triage, actor profiling, log analysis, Sigma / YARA / KQL / SPL generation |
| 🦠 [`/malware-analysis`](./malware-analysis/) | **3** | String deobfuscation, C2 protocol fingerprinting, packer identification |
| 🗡️ [`/red-team`](./red-team/) | **3** | Tabletop exercise builder, detection gap analysis, payload obfuscation brainstorm |
| 🔍 [`/osint`](./osint/) | **3** | Passive recon checklists, persona authenticity analysis, lookalike domain generation |
| 📋 [`/reporting`](./reporting/) | **3** | Executive incident summaries, pentest findings → remediation tickets, incident postmortems |
| 🛡️ [`/blue-team`](./blue-team/) | **3** | Detection rule review, analyst response playbooks, crown jewels mapping |

---

## 🚀 Usage

```bash
git clone https://github.com/TheGr8Val/TGV-Grimoire.git
cd TGV-Grimoire/hunting/llm-analysis
```

Open any prompt file, substitute the `[PLACEHOLDER]` values with your data, and send it to your model of choice (Claude, GPT-4o, Gemini, etc.).

---

## 🧬 Prompt metadata format

Every prompt starts with a YAML header:

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

## 🤝 Contributing

Contributions are welcome. See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines, metadata format, and the tag taxonomy.

## 🔒 Security

Found a prompt that could cause harm or a sensitive file accidentally committed? See [SECURITY.md](./SECURITY.md) — please report privately, not via public issues.

---

## 🌐 [ES] Descripcion

**TGV-Grimoire** es una coleccion bilingue de prompts de ciberseguridad para analistas, hunters e ingenieros que quieren aprovechar modelos de IA en sus flujos de trabajo.

Cada prompt incluye metadatos (autor, caso de uso, modelo probado, idioma, etiquetas) y esta listo para usarse en entornos reales.

Los placeholders se indican con `[MAYUSCULAS_EN_CORCHETES]`. Las notas en espanol aparecen en secciones marcadas `[ES]`.

---

## ☕ Support / Apoya el Proyecto

If this helps you work smarter in your security workflows, consider buying me a coffee.

[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-support-yellow)](https://buymeacoffee.com/thegr8val)

---

## 📄 License

[MIT](./LICENSE) — TheGr8Val, 2026
