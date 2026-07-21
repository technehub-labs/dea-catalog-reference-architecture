# Engagement Playbook

> How to run a DEA adoption programme using DERA.

---

## Before You Start

Confirm the following before initiating a DERA engagement:

- [ ] Executive sponsor identified (CTO or equivalent)
- [ ] Architecture team confirmed (minimum 2 architects)
- [ ] Engagement scope defined (which domains, which teams)
- [ ] TechNeHub Labs GitHub org access confirmed for all participants
- [ ] Metamodel version pinned (check `dea-metamodel/VERSION`)

---

## Kickoff Workshop (Week 1)

**Goal:** Agree the engagement scope, select the entity subset, and define the working agreement.

**Participants:** Chief Architect, Solutions Architects, key stakeholders from each in-scope domain.

**Agenda:**

1. **Framework introduction** (1h) — Present the four-layer DEA framework. Walk through the metamodel entity hierarchy. Show the `dea-cli` in action.

2. **Scope definition** (1h) — Identify which domains are in scope. Which L1 catalogs are relevant? Which entity types will the engagement focus on?

3. **Entity subset selection** (1h) — From the metamodel's 12 entity types, select the subset for this engagement. Not every engagement needs all 12. A Discovery engagement might focus on `Principle`, `ArchitecturePattern`, and `Standard`.

4. **Engagement style** (30m) — Choose Discovery, Blueprint, or Embedding based on scope and timeline.

5. **Working agreement** (30m) — Define PR cadence, review SLA, and communication channels.

**Output:** `DERA/v1-alpha/engagement-config.yaml` — the specific entity subset, engagement style, timeline, and participants for this engagement.

---

## Phase 1 Execution (Weeks 2–3)

### Activities

**1.1 — Metamodel CI setup**
- Fork or clone `dea-metamodel`
- Add the agreed entity subset to `metamodel.yaml` if custom entities are needed
- Configure GitHub Actions workflow (already in `dea-metamodel/.github/workflows/ci.yml`)
- Verify CI is green on first commit

**1.2 — Entity seeding**
- Seed the agreed entity subset with initial entries
- Follow the entity schema (see `dea-metamodel/schemas/entities/`)
- Run `dea validate` locally before pushing

**1.3 — Branching strategy**
- Define branch model: `main` (released), `draft/*` (work in progress)
- Configure branch protection rules
- Set up CODEOWNERS for the metamodel repo

**1.4 — Onboarding**
- Onboard all architects: clone, validate, submit a test PR
- Confirm all architects can run `dea-cli query` against the local catalog

### Milestone: Phase 1 Exit Review
Review at end of Week 3:
- CI pipeline is green
- Entity subset committed and validated
- All architects have submitted at least one PR
- Branch protection and CODEOWNERS active

---

## Phase 2 Execution (Weeks 4–6)

### Activities

**2.1 — Principles catalog seeding**
- Review `dea-catalog-principles` entries
- Select principles relevant to the engagement (typically 3–7)
- Link each principle to the engagement's strategic objectives

**2.2 — Standards catalog seeding**
- Review `dea-catalog-standards` entries
- Select applicable technology and architectural standards
- Map each standard to the patterns that implement it

**2.3 — Patterns catalog seeding**
- Review `dea-catalog-patterns` entries
- Select patterns for the solution architecture
- Document forces, context, and consequences for each selected pattern
- Link patterns to the principles that motivate them

**2.4 — Reference Models and other catalogs**
- Seed domain-specific reference models from `dea-catalog-reference-models`
- Seed metrics from `dea-catalog-metrics`
- Seed glossary terms from `dea-catalog-glossary`

**2.5 — Cross-catalog relationships**
- Declare all cross-catalog relationships in each entity's YAML frontmatter
- Pattern → Principle (motivated-by)
- Standard → Pattern (implemented-by)
- Component → Technology (uses)
- Metric → Capability (measures)

**2.6 — Validation**
- Run `dea validate` across all catalogs
- Resolve all validation errors before proceeding

### Milestone: Phase 2 Exit Review
Review at end of Week 6:
- All scoped catalogs seeded with entries
- Cross-catalog relationships declared
- `dea validate` passes for all entries
- Catalog versioning policy agreed

---

## Phase 3 Execution (Weeks 7–9)

### Activities

**3.1 — CLI deployment**
- Install `dea-cli` for all architects
- Configure catalog paths in `~/.dea/config.yaml`
- Verify `dea query` returns results from all in-scope catalogs

**3.2 — Viewpoint generation**
- Generate viewpoints for each stakeholder role: CTO, Chief Architect, Solutions Architect, Business Architect, Developer
- Save viewpoints as GitHub wiki pages or shared documents
- Set a recurring monthly viewpoint refresh

**3.3 — Artifact generation pipeline**
- Integrate `dea generate` into the architecture review workflow
- Generate ADRs for all significant architectural decisions
- Generate component specs for each major solution component

**3.4 — Web viewer deployment** (Blueprint style only)
- Deploy `dea-web-viewer` to a shared URL accessible to all stakeholders
- Configure catalog sources to point to the engagement's GitHub repos
- Publish the URL to all participants

**3.5 — Training**
- Run a 2-hour `dea-cli` workshop for architects
- Cover: `dea query`, `dea viewpoint`, `dea validate`, `dea generate`
- Document common workflows in the engagement wiki

### Milestone: Phase 3 Exit Review
Review at end of Week 9:
- All stakeholder viewpoints generated and shared
- Architecture artifact pipeline running
- Web viewer deployed (Blueprint) or CLI accessible to all architects (Discovery)
- Training complete

---

## Phase 4 Execution (Weeks 10–12)

### Activities

**4.1 — Branch protection audit**
- Verify branch protection on all active repos
- Confirm: require PR, 1 reviewer approval, CI passing

**4.2 — CODEOWNERS deployment**
- Confirm CODEOWNERS per layer is active on all repos
- Assign L0: @chief-architect, L1: @solutions-architects, L2: @tooling-team

**4.3 — SBOM publication**
- Generate SBOM for each L2 tooling package using `syft`
- Publish to the repo's Releases page
- Configure GitHub Actions to regenerate SBOM on every release

**4.4 — Contributing guide**
- Write engagement-specific `CONTRIBUTING.md`
- Include: how to propose a new entity, how to add a relationship, validation requirements
- Link from all repo READMEs

**4.5 — GitHub Discussions**
- Enable GitHub Discussions on the org
- Create categories: Q&A, Ideas & Proposals, General, Announcements
- Seed with at least one pinned announcement: the engagement kickoff summary

**4.6 — Release cadence**
- Define: monthly catalog updates, quarterly metamodel reviews
- Assign release manager role
- Publish release notes using Keep a Changelog format

### Milestone: Phase 4 Exit Review
Review at end of Week 12:
- All governance artifacts active
- SBOM published for all L2 packages
- Contributing guide linked from all READMEs
- GitHub Discussions active
- Framework is self-sustaining

---

## Ongoing: Embedding Cycle

For Embedding-style engagements, the DERA cycle repeats:

```
Every Sprint Cycle:
  1. Review catalog gaps → add new entries (Phase 2)
  2. Review tooling needs → deploy new capabilities (Phase 3)
  3. Review governance → refine policies (Phase 4)
  4. Re-generate viewpoints → refresh stakeholder views
  5. Quarterly: metamodel review → propose new entities (Phase 1)
```

---

## Roles and Responsibilities

| Role | Responsibility | Phase Focus |
|------|---------------|-------------|
| Chief Architect | Metamodel stewardship, cross-domain coherence | Phase 1, Phase 4 |
| Solutions Architect | Catalog seeding, pattern selection, relationships | Phase 2 |
| Platform Engineer | Tooling deployment, CI/CD, web viewer | Phase 3 |
| Engagement Manager | Sprint planning, stakeholder communication | All phases |
| Release Manager | Catalog versioning, release cadence | Phase 4 |
