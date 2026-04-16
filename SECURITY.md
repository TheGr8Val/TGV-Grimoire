# Security Policy

## Scope

This repository contains **prompt templates** — no backend, no API keys, no authentication layer, no user data. The attack surface is intentionally minimal.

That said, there are meaningful security concerns for a project like this:

| In scope | Out of scope |
|----------|-------------|
| Prompts that could cause harm if used as-is (e.g., unintentional prompt injection patterns) | Vulnerabilities in LLM providers (Claude, OpenAI, etc.) |
| Prompts in `/red-team` that lack proper authorization guardrails | General AI safety concerns unrelated to this repo |
| Markdown files that could render maliciously in certain environments | Third-party tools referenced in prompt notes |
| Sensitive data accidentally committed (tokens, keys, PII) | Issues with your own LLM API setup |

---

## Reporting a Vulnerability

**Do not open a public GitHub issue for security concerns.**

Report privately via one of the following:

- **GitHub Security Advisories** — [Report a vulnerability](https://github.com/TheGr8Val/TGV-Grimoire/security/advisories/new) *(preferred)*
- **Email** — Contact [@TheGr8Val](https://github.com/TheGr8Val) directly through GitHub

### What to include

- A clear description of the concern
- The file(s) affected
- A concrete example of how it could cause harm
- Your suggested fix (optional but appreciated)

---

## Response commitment

| Timeline | Action |
|----------|--------|
| Within **48 hours** | Acknowledgment of your report |
| Within **7 days** | Initial assessment and triage |
| Within **30 days** | Resolution or public disclosure timeline agreed upon |

---

## Ethical use

TGV-Grimoire is built for **defensive security, authorized testing, and education**.

Prompts in this library — especially in `/red-team` and `/osint` — are designed for practitioners operating within legal and ethical boundaries. If you find a prompt that could be easily weaponized without authorization context, or that lacks sufficient ethical guardrails, please report it. We will add appropriate warnings or restructure the prompt.

Misuse of prompts from this library for unauthorized access, harassment, or illegal activity is solely the responsibility of the user and is explicitly against the project's intent.

---

## [ES] Politica de Seguridad

No abras un issue publico para reportar problemas de seguridad. Usa GitHub Security Advisories o contacta directamente a [@TheGr8Val](https://github.com/TheGr8Val).

Los prompts de este repositorio estan disenados para uso defensivo, pruebas autorizadas y educacion. El mal uso es responsabilidad exclusiva del usuario.
