# hunting/

> Threat hunting prompts — IOC triage, actor profiling, log analysis, detection engineering

This module covers prompts used during the hunting lifecycle: from initial hypothesis formation to IOC enrichment, log triage, and detection rule generation.

---

## Categories

### [`llm-analysis/`](./llm-analysis/)

Prompts for direct LLM interaction. You feed the model data (logs, IOCs, malware samples, reports) and it returns structured analysis. Best used in chat interfaces or single-turn API calls with large context.

| File | Use case |
|------|----------|
| [threat-actor-profiling.md](./llm-analysis/threat-actor-profiling.md) | Build a structured profile of a threat actor from raw intel |
| [ioc-enrichment.md](./llm-analysis/ioc-enrichment.md) | Enrich a list of IOCs with context and classification |
| [malware-behavior-analysis.md](./llm-analysis/malware-behavior-analysis.md) | Analyze malware behavior from sandbox output or strings |
| [log-triage.md](./llm-analysis/log-triage.md) | Triage a block of logs for suspicious activity |
| [lateral-movement-timeline.md](./llm-analysis/lateral-movement-timeline.md) | Reconstruct attacker lateral movement path from auth and process events |
| [hypothesis-generation.md](./llm-analysis/hypothesis-generation.md) | Generate prioritized hunting hypotheses for a given sector and environment |
| [alert-fatigue-triage.md](./llm-analysis/alert-fatigue-triage.md) | Deduplicate and prioritize a large batch of SIEM alerts |
| [ransomware-pre-encryption-indicators.md](./llm-analysis/ransomware-pre-encryption-indicators.md) | Identify ransomware staging behaviors before encryption executes |

### [`automation-api/`](./automation-api/)

Prompts engineered for programmatic use. Output is structured (JSON, YAML, Sigma, KQL) for direct consumption by downstream tools. Minimal prose, maximum machine-readability.

| File | Use case |
|------|----------|
| [sigma-rule-gen.md](./automation-api/sigma-rule-gen.md) | Generate a Sigma detection rule from a behavior description |
| [ioc-extraction.md](./automation-api/ioc-extraction.md) | Extract and classify IOCs from unstructured text |
| [splunk-query-gen.md](./automation-api/splunk-query-gen.md) | Generate a Splunk SPL query from a hunting hypothesis |
| [yara-rule-gen.md](./automation-api/yara-rule-gen.md) | Generate a YARA rule from malware strings or behavior |
| [kql-query-gen.md](./automation-api/kql-query-gen.md) | Generate a KQL query for Microsoft Sentinel or Defender XDR |
| [mitre-mapping.md](./automation-api/mitre-mapping.md) | Map behavior descriptions to ATT&CK technique IDs — returns JSON |
| [ioc-to-detection-pipeline.md](./automation-api/ioc-to-detection-pipeline.md) | Generate both a Sigma rule and YARA rule from IOCs in one pass |

---

## [ES] Descripcion del modulo

Este modulo contiene prompts para el ciclo de vida del threat hunting:

- **`llm-analysis/`** — Para interaccion directa con el modelo. Alimentas datos (logs, IOCs, reportes) y obtienes analisis estructurado.
- **`automation-api/`** — Para uso programatico via API. Salida en JSON, YAML, Sigma o KQL lista para consumo por otras herramientas.

---

## Related modules (coming soon)

- `/malware-analysis` — Deep-dive static and dynamic analysis prompts
- `/red-team` — Adversary simulation and hypothesis generation
- `/reporting` — Executive and technical report generation
