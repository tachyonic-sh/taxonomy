# Contributing to Tachyonic Taxonomy

We welcome contributions that expand and improve this taxonomy.

## What we accept

- **New attack descriptions** — documented techniques not yet in the catalog
- **Framework relations** — source-pinned control relations with a rationale,
  relation type, strength, and license review
- **Remediation improvements** — better defensive guidance or code examples
- **Research references** — academic papers, blog posts, CVEs
- **Corrections** — factual errors, broken links, typos

## What we don't accept

- **Attack payloads** — actual exploit content (prompts, images, etc.)
- **Detection logic** — indicators of successful exploitation
- **Model-specific data** — success rates against specific models
- **Automated tools** — scripts that execute attacks

This is a taxonomy, not an exploit database.

## Generated files and canonical ingest

`taxonomy/attack_catalog.yaml` and `schema/attack_schema.yaml` are generated
release artifacts. Public release generation owns each whole file, so direct
edits will be replaced on the next sync.

For a new attack, correction, or framework relation, open a
[data proposal issue](https://github.com/tachyonic-sh/taxonomy/issues/new) and
include:

- the proposed normalized YAML record, following `schema/attack_schema.yaml`
- primary or authoritative source references
- the suggested severity and framework relation rationale
- the upstream version or immutable source pin and any known license terms

Maintainers review accepted proposals, ingest them into the canonical Tachyonic
corpus, and regenerate the public artifacts. Pull requests remain appropriate
for hand-authored documentation, remediation guidance, examples, and research
references that are not generated files.

## How to contribute hand-authored content

1. Fork the repository
2. Create a focused branch
3. Avoid files whose header says `GENERATED FILE — DO NOT EDIT DIRECTLY`
4. Submit a pull request describing the change and its sources

## Attack definition format

Use this shape in a data proposal; maintainers validate it against the generated
schema before canonical ingest:

```yaml
- id: XX-NNN          # Category prefix + 3-digit number
  name: Technique Name
  category: category_id
  description: >
    What the attack does, how it works conceptually,
    and why it's a risk. No actual payloads.
  severity: critical|high|medium|low
  owasp: LLM01-LLM10
  atlas: AML.T0000     # MITRE ATLAS technique ID (if applicable)
  framework_refs:
    - framework_id: framework_slug
      framework_version: exact-version
      control_id: CONTROL-ID
      control_name: Published or clearly attributed display name
      control_name_origin: upstream|tachyonic
      relation: classifies|tests
      strength: direct|partial|inherited|contextual
  references:
    - url: https://...
      title: Source reference
```

Framework references must resolve to a pinned source in the private canonical
corpus and be permitted by that source manifest's public export policy. A
mapping means only that a reviewed relation exists; it must not be described as
a passed test, compliance determination, certification, or independent
assurance.

## Severity ratings

- **critical** — trivial to execute, high impact, broadly applicable
- **high** — reliable execution, significant impact
- **medium** — requires specific conditions, moderate impact
- **low** — difficult to execute or limited impact

## Code of conduct

Be professional. This project exists to improve AI security. Contributions should be educational and defensive in nature.
