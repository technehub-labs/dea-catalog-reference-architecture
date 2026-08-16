# Digital Enterprise Reference Architecture

> **Canonical reference model assembling the full TechNeHub Labs DEA framework into a practical enterprise delivery blueprint.**

[![Layer: L1](https://img.shields.io/badge/Layer-L1%20—%20Reference%20Catalogs-8b5cf6?style=flat-square)](https://github.com/technehub-labs/dea-metamodel)
[![Status: Alpha](https://img.shields.io/badge/Status-Alpha-FF6B35?style=flat-square)](./)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue?style=flat-square)](LICENSE)

---

## Overview

The Digital Enterprise Reference Architecture (DERA) is the synthesising L1 catalog that assembles all other DEA framework catalogs into a coherent, deliverable end-to-end blueprint. Where individual catalogs define *what* the framework contains (patterns, tenets, guardrails), DERA defines *how the pieces fit together* — which layers reference which, in what order, for what kind of engagement.

> Naming follows OpenDEAM v0.4.0 (ADR-0004): Principle → **Tenet**, Standard → **Guardrail**, Glossary Term + Taxonomy Node → **Concept**, Reference Model → **Blueprint**.

DERA is the reference model that enterprise architects, solution architects, and technology leaders use to plan a DEA adoption programme: scoping the engagement, sequencing the deliverables, assigning ownership by layer, and measuring progress.

---

## Framework Position

```
L0 — Metamodel
  ↕  Defines entities and relationships used by all L1 catalogs
L1 — Reference Catalogs
  ├── Tenets           (dea-catalog-tenets)
  ├── Guardrails       (dea-catalog-guardrails)
  ├── Patterns         (dea-catalog-patterns)
  ├── Blueprints       (dea-catalog-blueprints)
  ├── Metrics          (dea-catalog-metrics)
  ├── Concepts         (dea-catalog-concepts)
  ├── Ontologies       (dea-catalog-ontologies)
  └── Reference Architecture ← DERA (this repo) — the assembling blueprint
L2 — Tooling           (dea-cli, dea-scripts, dea-code-gen, dea-web-viewer)
L3 — Governance        (branch strategy, SBOM, Apache 2.0 licensing, contributing)
```

---

## Structure

```
dea-catalog-reference-architecture/
├── README.md
├── DERA/
│   ├── v1-alpha/
│   │   ├── model.md              ← The canonical DERA v1-alpha reference model
│   │   ├── engagement-playbook.md ← How to run a DEA adoption programme
│   │   └── assessment-checklist.md ← Maturity self-assessment template
│   └── index.yaml                ← Version-indexed entry point
├── stakeholders/
│   └── viewpoint.yaml            ← DERA stakeholder viewpoints
└── relationships/
    └── catalog-links.yaml        ← Typed relationships to other L1 catalogs
```

---

## The Reference Model

DERA v1-alpha defines the following canonical **delivery phases** and their constituent layer responsibilities:

### Phase 1 — Foundation (L0 + L0 tooling)
Establish the metamodel as the single source of truth for all entity definitions.

**Activities:**
- Agree on entity subset for the engagement scope
- Configure CI validation pipeline (JSON Schema + TTL consistency checks)
- Seed the metamodel SQLite runtime for local tooling use
- Establish branching strategy and CODEOWNERS per layer

**Deliverables:**
- Configured `dea-metamodel` CI pipeline
- Initial entity subset committed and validated
- Team onboarding: how to contribute to catalogs

---

### Phase 2 — Catalog Seeding (L1)
Populate the reference catalogs for the engagement scope.

**Activities:**
- Seed Tenets (from `dea-catalog-tenets`)
- Seed Guardrails (from `dea-catalog-guardrails`)
- Seed Architecture Patterns (from `dea-catalog-patterns`)
- Seed Blueprints (from `dea-catalog-blueprints`)
- Seed Metrics (from `dea-catalog-metrics`)
- Seed Concepts (from `dea-catalog-concepts`)

**Deliverables:**
- All scoped catalogs seeded with initial entries
- Cross-catalog relationships established (Tenet → Guardrail `informs`, Blueprint → Pattern `composed of`, etc.)
- `dea-cli validate` passing for all entries

---

### Phase 3 — Tooling Enablement (L2)
Enable practitioners to work with the seeded catalogs.

**Activities:**
- Install and configure `dea-cli`
- Set up `dea-web-viewer` for stakeholder browsing
- Configure viewpoint templates for each practitioner role
- Train architects on `dea query` and `dea viewpoint`

**Deliverables:**
- `dea-cli` configured for the engagement environment
- Stakeholder viewpoints generated and shared
- Architecture artifact generation pipeline running

---

### Phase 4 — Governance Activation (L3)
Put the operational governance model in place.

**Activities:**
- Activate GitHub Discussions for Q&A
- Enforce branch protection on all active repos
- Configure CODEOWNERS per layer
- Publish SBOM for all tooling packages
- Establish release cadence and catalog versioning policy

**Deliverables:**
- All repos at L1/L2 have branch protection enabled
- CODEOWNERS active per layer
- `CONTRIBUTING.md` published and linked from all READMEs
- SBOM published for `dea-cli`, `dea-scripts`, `dea-web-viewer`

---

## Engagement Styles

DERA supports three engagement styles, distinguished by scope and depth:

| Style | Scope | Phases | Duration |
|-------|-------|--------|----------|
| **Discovery** | Single domain, 3–5 patterns, 1 standard | 1 → 2 | 2–4 weeks |
| **Blueprint** | Full enterprise, all catalogs, L2 tooling | 1 → 4 | 8–12 weeks |
| **Embedding** | Ongoing programme, integrated with agile delivery | Continuous (1 → 4 cycling) | Ongoing |

---

## Relationships to Other Catalogs

DERA references and composes all other L1 catalogs. Key relationships:

| Relationship | Target Catalog | Description |
|-------------|---------------|-------------|
| `references` | `dea-catalog-tenets` | DERA phases are driven by architecture tenets |
| `applies` | `dea-catalog-patterns` | Each phase applies specific patterns from the catalog |
| `conforms-to` | `dea-catalog-guardrails` | DERA delivery conforms to enforced guardrails |
| `measured-by` | `dea-catalog-metrics` | Phase completion measured by catalog metrics |
| `defines` | `dea-catalog-concepts` | DERA phases link to the canonical concept graph |
| `formalises` | `dea-catalog-ontologies` | DERA's entity model formalised in OWL/RDF |

---

## How to Use This Catalog

1. **Read the reference model** — `DERA/v1-alpha/model.md` defines the full delivery blueprint
2. **Run the assessment** — `DERA/v1-alpha/assessment-checklist.md` to score current maturity
3. **Choose your engagement style** — Discovery, Blueprint, or Embedding
4. **Follow the phases in order** — each phase builds on the previous
5. **Use the CLI** — `dea-cli viewpoint -s <role>` to generate a DERA viewpoint for your role

---

## Contributing to DERA

DERA is maintained as part of the TechNeHub Labs framework. To propose changes:

1. Open an issue in this repo describing the proposed change
2. Align with the Chief Architect or Solutions Architect stakeholder viewpoint
3. Ensure the change is consistent with the metamodel (`dea-metamodel`)
4. Submit a PR with the updated model section and relationships

---

## License

Apache 2.0 — see [LICENSE](./LICENSE).