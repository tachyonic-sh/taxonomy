# Tachyonic Taxonomy

**An open taxonomy of 168 AI/LLM attack vectors with versioned, source-pinned framework relations.**

[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![ESF Phases 1-3](https://img.shields.io/badge/ESF-Phases_1--3-green.svg)](https://github.com/tachyonic-sh/esf)

---

## What is this?

A structured, machine-readable catalog of documented techniques for attacking AI systems. Each attack has an ID, name, category, description, severity rating, and reviewed relations to applicable public frameworks, including OWASP LLM, Agentic, and MCP taxonomies and MITRE ATLAS.

This is the **what** — what attacks exist and how to defend against them. It does not include payloads, detection logic, or model-specific data.

This repository implements **Phases 1-3** of the [Evolutionary Security Framework (ESF)](https://github.com/tachyonic-sh/esf) — the open maturity model for progressively hardening AI security systems. See [ESF.md](ESF.md) for details.

## Why?

Most AI security discussions focus on a handful of well-known attacks. In reality, there are over 160 distinct techniques across 16 categories. A system that blocks a naive instruction override might still fall to an encoding bypass, a multi-turn escalation, or an indirect injection through retrieved content.

This taxonomy gives you:

* **A checklist** — do your defenses cover all 16 categories?
* **A common language** — reference specific attack IDs (e.g., PI-007, JB-015) in security discussions
* **Framework traceability** — versioned OWASP and MITRE ATLAS control references for security assessment and audit evidence; a mapping is not a compliance or certification result
* **Remediation guidance** — defensive strategies per category with code examples
* **ESF Phase 1-3 foundation** — the naming, relating, and initial heuristics that all downstream hardening depends on

## Attack Categories

Identifiers below are from the **OWASP GenAI LLM Top 10 2026** (v1.0, released
2026-08-04). That release renumbered eight of the ten risks without adding or
removing any, so a 2025 identifier is still a valid 2026 identifier meaning a
different risk. Where a category's identifier moved, the 2025 value is shown so
an older report can be reconciled.

| Category | ID Prefix | Count | OWASP LLM Top 10 2026 |
| --- | --- | --- | --- |
| Prompt Injection | PI | 20 | LLM01 |
| System Prompt Leakage | SPL | 12 | LLM08 Hidden Context Exposure (was LLM07) |
| Jailbreaks | JB | 22 | LLM01 |
| Vision/Multimodal | VI | 12 | LLM01 |
| Excessive Agency / Tool Abuse | EA | 20 | LLM03 (was LLM06) |
| Multi-Turn Manipulation | MT | 10 | LLM01 |
| Sensitive Information Disclosure | SID | 10 | LLM02 |
| Supply Chain | SC | 12 | LLM04 (was LLM03) |
| Vector/Embedding Attacks | VE | 10 | LLM09 (was LLM08) |
| Improper Output Handling | IOH | 8 | LLM10 (was LLM05) |
| Unbounded Consumption | UC | 2 | LLM06 (was LLM10) |
| Misinformation | MIS | 6 | LLM07 (was LLM09) |
| Memory/Context Poisoning | CTX | 6 | ASI06 |
| Unexpected Code Execution | UCE | 6 | ASI05 |
| Inter-Agent Communication | IAC | 6 | ASI07 |
| Human Trust Exploitation | HTE | 6 | ASI09 |
| **Total** |  | **168** |  |

## Repository Structure

```
taxonomy/                            ← repo root (tachyonic-sh/taxonomy)
├── taxonomy/                        ← ESF Phase 1: Name
│   ├── attack_catalog.yaml          # Generated: 168 attacks plus generic, versioned framework_refs
│   ├── owasp_mapping.yaml           # Attack → OWASP LLM Top 10 mapping
│   └── atlas_mapping.yaml           # Attack → MITRE ATLAS mapping
├── schema/
│   └── attack_schema.yaml           # Generated public schema (do not edit directly)
├── remediation/                     ← ESF Phase 3: Guess
│   ├── by_owasp.yaml               # Defensive guidance per OWASP category
│   └── code_examples/
│       ├── input_validation.py      # Input sanitization patterns
│       └── output_sanitization.py   # Output filtering patterns
├── research/
│   └── papers.yaml                  # Academic references index
├── examples/
│   └── sample_attacks.yaml          # Basic public examples
├── ESF.md                           # How this repo implements ESF Phases 1-3
├── README.md
├── LICENSE                          # Apache 2.0
└── CONTRIBUTING.md
```

## Quick Start

### Browse the taxonomy

```yaml
# taxonomy/attack_catalog.yaml
- id: PI-001
  name: Direct Instruction Override
  category: prompt_injection
  description: >
    Attacker provides input that directly instructs the model to ignore
    its system prompt and follow new instructions instead.
  severity: critical
  owasp: LLM01
  framework_refs:
    - framework_id: owasp_llm
      framework_version: 2026-v1.0
      control_id: LLM01
      control_name: Prompt Injection
      control_name_origin: upstream
      relation: classifies
      strength: direct
```

### Use in your security assessments

1. Clone the repo
2. Review `taxonomy/attack_catalog.yaml` for the full attack surface
3. Check `remediation/by_owasp.yaml` for defensive guidance
4. Use `schema/attack_schema.yaml` to prepare a
   [data proposal](https://github.com/tachyonic-sh/taxonomy/issues/new); maintainers
   ingest accepted proposals into the canonical corpus and regenerate the catalog

### Resolve framework relations

```yaml
# taxonomy/owasp_mapping.yaml — keys are <id>_<name>, so a key written against
# an older release fails to resolve rather than resolving to the wrong risk.
LLM01_prompt_injection:
  name: "Prompt Injection"
  total: 71
  attacks: [PI-001, ..., PI-020, JB-001, ..., MT-010, VI-001, ..., VI-012]
```

`framework_refs` in `taxonomy/attack_catalog.yaml` is the generic interface.
Each reference carries its framework version, control identifier and name,
relation type, strength, and source pin when available. The legacy `owasp` and
`atlas` fields remain during a compatibility window.

### Assess your maturity

Use the [ESF Quick Start](https://github.com/tachyonic-sh/esf/blob/main/guides/quick-start.md) to score your system against the ten-phase maturity model. This taxonomy provides the foundation for Phases 1-3.

## Evolutionary Security Framework (ESF)

This repository is the **Phases 1-3 reference implementation** of the [ESF](https://github.com/tachyonic-sh/esf).

The ESF defines how security knowledge matures through ten phases — from naming threats (Phase 1, this repo) to mathematically proving defenses (Phase 9). OWASP tells you *what* the risks are. The ESF tells you *how to progressively harden* against them.

| ESF Phase | This Repo | What It Does |
|---|---|---|
| Phase 1: **Name** | `taxonomy/` | Classifies 168 attacks with stable IDs and framework mappings |
| Phase 2: **Relate** | `taxonomy/attack_catalog.yaml`, `taxonomy/*_mapping.yaml` | Publishes reviewed, versioned relations to approved framework controls |
| Phase 3: **Guess** | `remediation/` | Defensive heuristics and code examples |

See [ESF.md](ESF.md) for the full mapping and growth roadmap.

## What's NOT included

This taxonomy deliberately excludes:

* **Attack payloads** — the specific prompts/content that execute attacks
* **Detection logic** — how to identify if an attack succeeded
* **Model-specific success rates** — which attacks work against which models
* **Confidence scoring** — how to rate vulnerability severity programmatically

These are the difference between knowing attacks exist and being able to systematically test for them.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines. We welcome:

* New attack technique descriptions
* Source-pinned framework relation proposals with license and claim boundaries
* Remediation guidance improvements
* Research paper references

The catalog and public schema are generated artifacts. Propose data changes
through the canonical ingest route in CONTRIBUTING rather than editing those
files directly.

## Professional Assessment

Want to test your AI system against all 168 attack vectors? [Tachyonic](https://tachyonicai.com) offers 48-hour red team assessments with full reporting, resistance scoring, and ESF maturity assessment.

[Book a scoping call →](https://cal.com/tachyonicai/ai-security-scoping)

## License

Apache 2.0 — see [LICENSE](LICENSE).

## Citation

```
@misc{tachyonic-taxonomy,
  title={Tachyonic Taxonomy: AI/LLM Attack Vectors},
  author={Tachyonic},
  year={2026},
  url={https://github.com/tachyonic-sh/taxonomy}
}
```
