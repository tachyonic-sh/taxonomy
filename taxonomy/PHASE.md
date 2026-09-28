# ESF Phase 1: Name (Taxonomy)

> **Core Question:** *What exists in this domain?*

This directory implements Phase 1 of the [Evolutionary Security Framework](https://github.com/tachyonic-sh/esf).

## Contents

| File | Role |
|---|---|
| `attack_catalog.yaml` | 168 attack vectors — IDs, names, categories, descriptions, severity, and generic versioned framework relations |
| `owasp_mapping.yaml` | Attack → OWASP LLM Top 10 relationships (also feeds Phase 2) |
| `atlas_mapping.yaml` | Attack → MITRE ATLAS relationships (also feeds Phase 2) |

## ESF Maturity: Score 3-4

- Machine-readable YAML format
- Exhaustive within scope (168 attacks across 16 categories)
- Faceted classification (category, severity, and manifest-approved framework relations)
- Stable identifiers (PI-001, JB-015, etc.)
- Extensible schema (`schema/attack_schema.yaml`)

## What Would Reach Score 4

- Automated gap detection when new attack techniques emerge
- Version tracking on taxonomy changes with changelog
- Dynamic updates driven by Phase 10 (Evolve) feedback loops
