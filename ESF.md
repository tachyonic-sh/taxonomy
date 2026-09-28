# How This Repository Implements the Evolutionary Security Framework

This repository is the **Phases 1-3 reference implementation** of the [Evolutionary Security Framework (ESF)](https://github.com/tachyonic-sh/esf) — an open maturity model for progressively hardening agentic AI security systems.

## What is the ESF?

The ESF defines ten phases that describe how security knowledge matures — from naming threats to mathematically proving defenses:

```
Name → Relate → Guess → Measure → Model → Explain → Formalize → Constrain → Prove → Evolve
```

This repository implements the first three phases. The ESF specification, maturity rubric, and full framework live in [tachyonic-sh/esf](https://github.com/tachyonic-sh/esf).

## Phase Mapping

| ESF Phase | This Repo | What It Does |
|---|---|---|
| **Phase 1: Name** (Taxonomy) | `taxonomy/` | Classifies 168 AI/LLM attack vectors across 16 categories with stable IDs, severity ratings, and framework mappings |
| **Phase 2: Relate** (Ontology) | `taxonomy/owasp_mapping.yaml`, `taxonomy/atlas_mapping.yaml` | Maps relationships between attacks and industry frameworks. Attack chain analysis and trust boundary modeling are growth areas (see below) |
| **Phase 3: Guess** (Heuristics) | `remediation/` | Provides defensive heuristics — detection strategies and response guidance per OWASP category, with code examples |

## What's Open vs. Proprietary

This repository shares the **epistemology** — what attacks exist, how they relate, and strategies for defending against them. It does not include:

- Attack payloads (the specific prompts/content that execute attacks)
- Detection logic (how to identify if an attack succeeded)
- Model-specific success rates
- Confidence scoring methodology

These remain proprietary because they power [Tachyonic's](https://tachyonic.co) security runtimes. The open taxonomy tells you *what* to defend against. The proprietary layer tells you *how* to test and detect.

## Growth Areas

As the ESF matures, this repository will expand:

- **Phase 2 depth**: Machine-readable attack chains, trust boundary definitions, and entity relationship types (planned in `ontology/`)
- **Phase 3 depth**: Detection strategies per attack chain and response playbooks (planned in `heuristics/`)

## Learn More

- [ESF Living Specification](https://github.com/tachyonic-sh/esf/blob/main/spec/ESF-v0.1.0.md) — the full framework
- [Quick Start Assessment](https://github.com/tachyonic-sh/esf/blob/main/guides/quick-start.md) — assess your system in 30 minutes
- [OWASP LLM Top 10 ↔ ESF Mapping](https://github.com/tachyonic-sh/esf/blob/main/mappings/owasp-llm-top10.yaml)
- [OWASP Agentic Top 10 ↔ ESF Mapping](https://github.com/tachyonic-sh/esf/blob/main/mappings/owasp-agentic-top10.yaml)
