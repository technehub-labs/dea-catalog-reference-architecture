# DERA v1-alpha — Digital Enterprise Reference Architecture

> Status: **Alpha** — Draft for review and early adoption
>
> **Terminology note (2026-08-16):** catalog names follow OpenDEAM v0.4.0 (ADR-0004) — Principle → **Tenet** (`dea-catalog-tenets`), Standard → **Guardrail** (`dea-catalog-guardrails`), Glossary/Taxonomy → **Concept** (`dea-catalog-concepts`), Reference Model → **Blueprint** (`dea-catalog-blueprints`). Some prose below still uses the pre-ADR-0004 vocabulary; repo links are current. Entity counts reference the live root model (`dea-architecture-framework`, OpenDEAM v0.5.0 — 53 first-level entities).

---

## Purpose

DERA v1-alpha provides the canonical delivery blueprint for adopting the TechNeHub Labs Digital Enterprise Architecture framework in an enterprise context. It answers the question: *where do I start, and how do the pieces fit together?*

It is a **reference model**, not a methodology. It does not prescribe how you run your sprints — it describes the logical structure of a DEA adoption programme and the relationships between the framework's constituent parts.

---

## Core Concept: The Four Phases

A DEA adoption programme progresses through four sequential phases. Each phase has a clear focus, a defined set of activities, and measurable deliverables.

```
Phase 1 ──► Phase 2 ──► Phase 3 ──► Phase 4
Foundation  Catalog    Tooling    Governance
            Seeding    Enablement Activation
```

### Phase 1 — Foundation
**Focus:** Establish the metamodel as the single source of truth.

The metamodel is the most foundational investment. Every catalog entry, every relationship, every generated artifact flows from the metamodel's entity definitions. Getting the metamodel right — and getting the CI pipeline that validates it working — is the precondition for everything else.

**Key activities:**
- Agree the entity subset in scope for the engagement
- Configure `dea-metamodel` CI: JSON Schema validation, TTL consistency checks
- Seed the SQLite runtime for local tooling
- Define branching strategy and CODEOWNERS by layer
- Assign metamodel steward role

**Exit criteria:**
- `dea-metamodel` CI pipeline is green
- All scoped entity types have at least one seed entry
- At least two contributors have onboarded and can submit a PR

---

### Phase 2 — Catalog Seeding
**Focus:** Populate the reference catalogs with the engagement scope.

With the metamodel in place, the catalogs become the primary deliverable. Each catalog is seeded with entries that are relevant to the engagement domain. Entries are typed against the metamodel and linked to each other through typed relationships.

**Key activities:**
- Seed `dea-catalog-tenets` — select principles that govern the engagement (e.g., API-first, Zero Trust)
- Seed `dea-catalog-guardrails` — enumerate the technology and architectural standards that apply
- Seed `dea-catalog-patterns` — select patterns that are relevant to the solution architecture
- Seed `dea-catalog-blueprints` — document the reference architecture for the domain
- Seed `dea-catalog-metrics` — define how success will be measured
- Seed `dea-catalog-concepts` — agree on terminology for the engagement
- Establish cross-catalog relationships (Pattern → Principle, Standard → Pattern)
- Run `dea-cli validate` across all entries and resolve all errors

**Exit criteria:**
- All scoped catalogs have at least one seed entry per entity type
- All cross-catalog relationships are declared and valid
- `dea validate` passes for all entries

---

### Phase 3 — Tooling Enablement
**Focus:** Enable practitioners to work effectively with the seeded catalogs.

The tooling layer turns the catalogs from reference documents into active work instruments. Architects query the catalogs to find applicable patterns. Solutions architects generate component specs from catalog entries. CTOs generate viewpoint dashboards for steering.

**Key activities:**
- Install `dea-cli` and configure catalog paths for the engagement
- Deploy `dea-web-viewer` for non-technical stakeholders to browse the catalog
- Configure viewpoint templates for each practitioner role
- Integrate `dea-cli` into the architecture review workflow
- Train architects on `dea query`, `dea viewpoint`, and `dea generate`

**Exit criteria:**
- At least one viewpoint generated for each practitioner role
- Architecture artifact generation pipeline running (ADR, component spec)
- Web viewer accessible to all stakeholder roles

---

### Phase 4 — Governance Activation
**Focus:** Put the operational governance model in place.

Governance ensures the framework is maintained and evolves correctly after the initial adoption programme. This phase activates the L3 governance artifacts: branch protection, CODEOWNERS, contributing guidelines, SBOM, and the release cadence.

**Key activities:**
- Enable GitHub Discussions for Q&A and idea proposals
- Enforce branch protection on all active repos (require PR + 1 reviewer + CI)
- Configure CODEOWNERS per layer (L0/L1/L2 ownership)
- Publish SBOM for all L2 tooling packages using `syft`
- Write and publish `CONTRIBUTING.md` with the engagement-specific workflow
- Define catalog versioning policy (semver + metamodel version pinning)
- Establish release cadence for catalogs and tooling

**Exit criteria:**
- Branch protection active on all active repos
- CODEOWNERS configured for all layers
- SBOM published for `dea-cli`, `dea-scripts`, `dea-web-viewer`
- `CONTRIBUTING.md` linked from all repo READMEs
- GitHub Discussions active with at least one category configured

---

## Engagement Styles

DERA supports three engagement styles. The right style depends on the scope of the adoption and the maturity of the organisation's existing architecture practice.

### Discovery
**Scope:** Single domain or team. 3–5 architecture patterns. 1–2 standards.
**Duration:** 2–4 weeks.
**Phases:** 1 → 2 (foundation + catalog seeding only).

Best for organisations that are evaluating the framework or building a small pilot. No L2 tooling or L3 governance activation in this style — those come in a follow-on Blueprint engagement.

### Blueprint
**Scope:** Full enterprise. All catalogs. L2 tooling fully operational.
**Duration:** 8–12 weeks.
**Phases:** 1 → 4 (all four phases).

Best for organisations that are committed to adopting the framework enterprise-wide. Full catalog seeding, tooling deployment, and governance activation. Produces a self-sustaining architecture practice.

### Embedding
**Scope:** Ongoing programme integrated with agile delivery.
**Duration:** Continuous.
**Phases:** 1 → 4 cycling continuously as the programme evolves.

Best for organisations running an architecture transformation programme that is embedded in sprint-based delivery. Each sprint cycle revisits phases as needed — new patterns are added, new tooling is deployed, governance is refined.

---

## Catalog Relationships

DERA is the assembling reference model. Its value is in defining how the other catalogs relate to each other and to the delivery programme.

```
dea-catalog-reference-architecture
    │ references         dea-catalog-tenets
    │ applies            dea-catalog-patterns
    │ conforms-to        dea-catalog-guardrails
    │ references         dea-catalog-blueprints
    │ measured-by        dea-catalog-metrics
    │ uses               dea-catalog-concepts
    │ formalised-by      dea-catalog-ontologies
    │ expressed-in        dea-metamodel (L0)
    │ operationalised-by dea-cli, dea-scripts (L2)
    └─ governed-by       L3 Governance
```

---

## Versioning

DERA follows semantic versioning. Changes to the reference model are versioned independently of the individual catalogs.

- **MAJOR:** Structural change to phase order, new phase added, engagement style change
- **MINOR:** New activity added to a phase, new catalog relationship declared
- **PATCH:** Typo corrections, clarifications, alignment with metamodel updates

DERA catalogs declare their metamodel dependency via `metamodel_version` in `index.yaml`, following the Catalog Versioning Guide (see [dea-metamodel/GOV-R-002](https://github.com/technehub-labs/dea-metamodel/issues/32)).

---

## DERA Entity

DERA itself is a `ReferenceModel` entity in the metamodel:

```yaml
id: dea:reference-dera
type: ReferenceModel
name: Digital Enterprise Reference Architecture
abbreviation: DERA
version: "1.0.0-alpha"
status: active
description: >
  Canonical delivery blueprint for adopting the TechNeHub Labs DEA framework.
  Defines four sequential phases: Foundation, Catalog Seeding, Tooling Enablement,
  and Governance Activation. Supports three engagement styles: Discovery, Blueprint,
  and Embedding.
relationships:
  - source_id: dea:reference-dera
    target_id: dea:principle-api-first
    relationship_type: references
  - source_id: dea:reference-dera
    target_id: dea:pattern-cqrs
    relationship_type: applies
engagement_styles:
  - Discovery
  - Blueprint
  - Embedding
phases:
  - id: phase-1
    name: Foundation
    layers: [L0]
    exit_criteria: [CI green, entity subset agreed, team onboarded]
  - id: phase-2
    name: Catalog Seeding
    layers: [L1]
    exit_criteria: [catalogs seeded, relationships declared, validate passes]
  - id: phase-3
    name: Tooling Enablement
    layers: [L2]
    exit_criteria: [viewpoints generated, artifact pipeline running, training complete]
  - id: phase-4
    name: Governance Activation
    layers: [L3]
    exit_criteria: [branch protection active, CODEOWNERS set, SBOM published]
tags:
  - reference-architecture
  - delivery-blueprint
  - engagement-model
```
