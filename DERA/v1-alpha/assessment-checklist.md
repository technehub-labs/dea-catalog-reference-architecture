# DEA Maturity Assessment Checklist

> Self-assessment template for scoring an organisation's current state against the DEA framework.

---

## Purpose

Use this checklist to score the organisation's current architecture maturity before a DERA engagement. The assessment produces a baseline score and identifies priority areas for improvement. Re-run the assessment at the end of each phase to track progress.

---

## Scoring Guide

For each item, score:
- **0** — Not started / no awareness
- **1** — Partially addressed / informal practice
- **2** — Formally defined / documented
- **3** — Fully implemented / consistently practiced

Maximum score: **99** (3 × 33 items)

---

## Section 1: Metamodel & Definitions (12 items, max 36)

| # | Assessment Item | Score (0–3) |
|---|----------------|-------------|
| 1.1 | We have a shared, versioned vocabulary for architecture entities (principles, patterns, standards, components). | |
| 1.2 | Architecture entity definitions are written down and accessible to all architects. | |
| 1.3 | New entities require a formal proposal and review process. | |
| 1.4 | Relationships between entities are declared and traceable. | |
| 1.5 | Entity definitions are expressed in a machine-readable format (JSON, YAML, RDF). | |
| 1.6 | We maintain a glossary of shared architectural terms. | |
| 1.7 | We have a taxonomy for grouping entities (by domain, layer, concern). | |
| 1.8 | Entity ownership is assigned — someone is responsible for each entity type. | |
| 1.9 | We validate architecture entities against a schema before publishing. | |
| 1.10 | We use a canonical metamodel that all other definitions reference. | |
| 1.11 | We version our entity definitions and track changes over time. | |
| 1.12 | Our metamodel is tooling-accessible (CLI, API, or database query). | |

**Section 1 Score: ___ / 36**

---

## Section 2: Patterns & Standards (9 items, max 27)

| # | Assessment Item | Score (0–3) |
|---|----------------|-------------|
| 2.1 | We maintain a documented library of approved architecture patterns. | |
| 2.2 | Pattern selection is documented with forces, context, and consequences. | |
| 2.3 | Each pattern is linked to the business or technical problem it solves. | |
| 2.4 | We have a formal process for adding a new pattern to the library. | |
| 2.5 | We maintain a documented library of technical and architectural standards. | |
| 2.6 | Standards are linked to the patterns or components that implement them. | |
| 2.7 | We track which standards are mandatory vs. advisory. | |
| 2.8 | Pattern and standard adoption is reviewed in architecture governance. | |
| 2.9 | We measure pattern usage and flag deviations from approved patterns. | |

**Section 2 Score: ___ / 27**

---

## Section 3: Tooling & Automation (6 items, max 18)

| # | Assessment Item | Score (0–3) |
|---|----------------|-------------|
| 3.1 | Architects can query the architecture catalog programmatically. | |
| 3.2 | Architecture viewpoints can be generated for different stakeholder roles. | |
| 3.3 | Architecture decisions are documented as ADRs. | |
| 3.4 | Catalog entries are validated automatically (CI/CD). | |
| 3.5 | We have a web-based viewer for browsing the architecture catalog. | |
| 3.6 | Architecture artifacts (ADRs, component specs) are generated from the catalog. | |

**Section 3 Score: ___ / 18**

---

## Section 4: Governance & Process (6 items, max 18)

| # | Assessment Item | Score (0–3) |
|---|----------------|-------------|
| 4.1 | We have a documented contributing process for proposing new architecture entities. | |
| 4.2 | All architecture repos enforce branch protection and code review. | |
| 4.3 | Architecture decisions require sign-off from a designated authority. | |
| 4.4 | We publish a regular (quarterly) architecture health report. | |
| 4.5 | We maintain a public-facing architecture roadmap. | |
| 4.6 | We have an SBOM for all major tooling packages. | |

**Section 4 Score: ___ / 18**

---

## Total Score: ___ / 99

---

## Maturity Band

| Score | Band | Description |
|-------|------|-------------|
| 0–25 | **Ad Hoc** | Architecture practices are informal and person-dependent. No shared framework. |
| 26–50 | **Defined** | Core entities and patterns are documented but not consistently enforced. |
| 51–75 | **Managed** | Architecture framework is formal, tooling-enabled, and governance is active. |
| 76–99 | **Optimising** | Framework is self-sustaining, metrics-driven, and continuously improving. |

---

## Target Score by Engagement Style

| Engagement Style | Recommended Target | Priority Focus Areas |
|------------------|--------------------|---------------------|
| Discovery | 26–40 (Defined) | Sections 1, 2 |
| Blueprint | 51–65 (Managed) | Sections 1, 2, 3 |
| Embedding | 66–80 (Managed → Optimising) | Sections 3, 4 |

---

## Priority Improvement Plan

Based on the assessment, list the top 3 gaps to address:

1. **Gap 1:** _______________________________________________________________
   Target: _______________________________________________________________
   Phase: _______________________________________________________________

2. **Gap 2:** _______________________________________________________________
   Target: _______________________________________________________________
   Phase: _______________________________________________________________

3. **Gap 3:** _______________________________________________________________
   Target: _______________________________________________________________
   Phase: _______________________________________________________________

---

*Assessment date: _____________ Assessed by: _____________ Next review: _____________*
