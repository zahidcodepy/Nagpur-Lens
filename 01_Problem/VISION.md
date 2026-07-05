# NagpurLens — Vision

> **Authors:** Mohammad Ammar · Zahid Khan  · Mohammad Ruwaifa

> **Document Status:** Foundational — every other document in this repository must remain consistent with this one. If a future decision cannot be justified by this document, it is scope creep until this document itself is deliberately revised.
> **Version:** v1.0

> **Last Updated:** July 2026

---

> *"Nagpur's real estate market runs on rumors. NagpurLens runs on data."*

---

## 1. What NagpurLens Is

NagpurLens is an open-source **Urban Intelligence Platform** built specifically for Nagpur — designed to transform fragmented, scattered civic data into verified, structured, and actionable intelligence.

It is not a dashboard. It is not a portfolio project. It is a complete data engineering system — from raw research and source documentation, through validation and relational database design, through analytics and KPI computation, to a public product that real people can use to make real decisions.

The dashboard is one output. **The validated urban data platform is the foundation. Decision-support applications built on top of it are the product**

---

## 2. Why Nagpur

Nagpur is not a background detail. It is the reason this platform exists.

Nagpur sits at the geographic center of India. It is a Smart City Mission beneficiary. It has an operational metro rail network. It is headquarters to the Nagpur Municipal Corporation — one of Maharashtra's largest civic bodies. It is experiencing genuine and rapid infrastructure investment across its peripheral localities.

And yet — no public data intelligence tool exists for this market. No verified, structured, locality-level dataset. No analytical platform that answers the questions every home buyer, investor, builder, and urban planner in Nagpur actually has.

People making ₹40–80 lakh decisions in Nagpur's real estate market rely on broker opinions and word-of-mouth. NagpurLens exists to replace that with data.

Nagpur was deliberately chosen not because it is easy, but because it represents the broader challenge faced by many Tier-2 Indian cities: fragmented public data, limited locality-level intelligence, and a lack of integrated analytical platforms. By solving this problem for Nagpur first, NagpurLens establishes an engineering framework that can later be adapted to other cities.

---

## 3. The Three Questions We Answer

NagpurLens is not a general analytics platform. It is purpose-built to answer three specific questions about Nagpur — in order of version, and in order of importance:

### Question 1 — Where does infrastructure lag despite having population?
Densely populated localities with failing infrastructure represent both a civic failure and a market inefficiency. Identifying and quantifying this gap — with verified data, not estimates — is the foundation of everything NagpurLens builds.

**Version 1 answers this question.**

### Question 2 — Which localities demonstrate measurable urban growth?
Growth is measurable. New construction signals, metro proximity, infrastructure investment patterns, and population density trends all point toward which localities are gaining momentum — and which are stagnating. NagpurLens surfaces these signals.

**Version 2 answers this question.**

### Question 3 — Which localities demonstrate stronger long-term investment potential based on documented indicators?
Combining infrastructure health, growth trajectory, accessibility scores, and demographic signals into a single auditable Investment Attractiveness Score. One number, fully explained, every weight documented, every formula public.

**Version 3 answers this question.**

---

## 4. The Data We Are Building

NagpurLens is built on documented, verified, and legally reusable data collected from public, official, open-data, and field-verified sources. Every record is traceable to its source and verification history.

### Core Dataset (Version 1)
- **Localities table:** 50+ Nagpur localities with GPS coordinates (6 decimal places), NMC zone classification, area, and Census 2011 population. Each locality is intended to be verified against multiple independent geographic references (such as OpenStreetMap, Google Maps, and official mapping resources where available), with the verification methodology documented in the project.
- **Infrastructure table:** 150+ infrastructure records across 9 categories — hospitals, schools, colleges, metro stations, bus stops, markets, police stations, fire stations, and parks. Every published record includes documented geographic coordinates, source attribution, collection date (where available), and verification status.
- **Locality ID standard:** XXX format, alphabetically assigned, consistent across every table and every document in this repository.
- **Haversine validation:** Every infrastructure record's locality assignment verified using haversine nearest-centroid algorithm. Zero orphan records.

### Five Derived KPIs
1. **Infrastructure Density Index (IDI):** Total infra count per km² — measures coverage.
2. **Healthcare Accessibility Score (HAS):** Weighted count of hospitals and clinics — measures health infrastructure.
3. **Metro Influence Index (MII):** Inverse distance to nearest operational metro station — measures connectivity.
4. **Growth Signal Index (GSI):** Composite of new construction signals and infrastructure investment — measures momentum.
5. **Investment Attractiveness Score (IAS):** The weighting methodology is versioned and may evolve based on validation, expert review, and empirical evaluation. Every revision will be
 documented.

All KPI methodologies are version-controlled and reproducible.
---

## 5. What Makes NagpurLens Different

Most student data projects follow the same path: find a Kaggle dataset, build a dashboard, call it a portfolio project. NagpurLens is built on an entirely different philosophy.

| Typical data project | NagpurLens |
|---|---|
| Kaggle dataset, provenance unknown | Self-collected, every source named and dated |
| No validation | Full validation report + passing automated tests |
| Dashboard only | Complete pipeline: research → DB → analytics → API → product |
| Black-box scores | Every KPI formula public and auditable |
| No methodology | Full methodology document, every decision explained |
| Scope undefined | Version-locked scope, explicit in/out boundaries |
| No CI | GitHub Actions run validation tests on every push |
| Generic README | README leads with a real, numbered finding from real data |

The real product is not the Streamlit dashboard. The real product is the validated, documented, reproducible data platform that anyone — a researcher, a developer, a government body — can audit, reproduce, and build upon.

---

## 6. The Engineering Pipeline

NagpurLens is built in strict sequence. No stage is skipped. No stage is rushed because a later stage looks exciting.

```
Research
   ↓
Data Acquisition
   ↓
Source Documentation
   ↓
Validation & Unit Testing
   ↓
Peer Review
   ↓
Normalization & Database Design (MySQL)
   ↓
KPI Computation (Python / Pandas)
   ↓
Analytical Queries (SQL)
   ↓
REST API (FastAPI)
   ↓
Dashboard (Streamlit)
   ↓
Public Website
   ↓
Scalable Platform
```

Beautiful dashboards cannot compensate for poor data quality. Correct data first. Reliable database second. Meaningful analytics third. Visualization last.

---

## 7. Guiding Principles

### 7.1 Trust Before Analytics
Every dataset must be verified, traceable, reproducible, and documented. An insight built on unverified data is not an insight — it is a guess with a chart on top.

### 7.2 Engineering Before Visualization
The priority order is fixed: correct data → reliable schema → meaningful analytics → visualization. This order is never reversed.

### 7.3 Open and Reproducible
Every stage of the pipeline is transparent. A developer who has never spoken to the NagpurLens team should be able to reproduce the complete database, all KPI scores, and all analytical outputs using only this repository. No hidden steps. No undocumented assumptions.

### 7.4 Limitations Are Stated, Not Hidden
Census 2011 population data is 15 years old. Infrastructure data is manually collected and may miss recently opened facilities. These limitations are front-and-center in every report — not buried in footnotes, not omitted to make the project look cleaner than it is. Honesty about limitations is what makes the rest of the data trustworthy.

### 7.5 Real Problems Over Demo Projects
NagpurLens exists to answer questions that real people in Nagpur actually have — not to demonstrate isolated technical skills. Every feature, every KPI, every table exists because it answers something a home buyer, investor, builder, or government body genuinely needs to know.

### 7.6 Depth Before Breadth
No version is pursued at the expense of the one before it. Version 1 must be fully correct, validated, and documented before Version 2 begins. A second city cannot be added on top of a shaky foundation.

### 7.7 Evidence Before Claims
Every public claim made by NagpurLens must be traceable to documented evidence, reproducible methodology, or explicitly stated assumptions.
---

## 8. Versioned Roadmap

| Version | Focus | Headline Question Answered |
|---|---|---|
| **v0.1** | Data foundation — localities + infra tables, schema, validation | Data exists and is trustworthy |
| **v0.2** | Analytics engine — KPI computation, ranked outputs | Which localities score highest/lowest |
| **v0.3** | Public product — Streamlit dashboard, FastAPI, website | Anyone can explore the data |
| **v0.4** | Real estate data layer — price trends, transaction signals | Where is money moving |
| **v1.0** | Full Version 1 — Infrastructure Intelligence Platform for Nagpur | Where does infra lag vs population |
| **v2.0** | Growth Intelligence — growth signal modeling | Which localities are growing |
| **v3.0** | Investment Intelligence — Investment Attractiveness Score | Where should you invest |
| **v4.0** | Platform — civic SaaS API, government collaboration, data licensing | Scalable beyond Nagpur |

---

## 9. Target Users

NagpurLens is built for five specific users. Every feature must be traceable to at least one of them.

**Home Buyers** — Making a ₹40–80 lakh decision in Nagpur's real estate market. They need verified infrastructure data for specific localities before they sign. NagpurLens answers: *"Is this locality actually as well-served as the broker claims?"*

**Property Investors** — Allocating capital across Nagpur localities. They need growth signals and infrastructure scores to identify appreciation potential before the market prices it in. NagpurLens answers: *"Which localities are 3–5 years ahead of price appreciation?"*

**Builders and Developers** — Identifying where population is dense but infrastructure is thin. That gap is where the next residential project belongs. NagpurLens answers: *"Where is demand forming before supply catches up?"*

**Government and Civic Bodies (NMC, Smart City Nagpur Limited)** — Prioritizing infrastructure investment across 57+ localities with limited budgets. NagpurLens answers: *"Where are citizens most underserved relative to population density?"*

**Researchers and Urban Planners** — Needing a validated, source-documented, reproducible dataset for academic and policy work. NagpurLens answers: *"Is there a research-grade urban dataset for Nagpur I can build on?"*

---

## 10. Success Metrics

NagpurLens Version 1 succeeds when:

- 50+ localities are in the database with Coordinates validated to the precision appropriate for the data source, with verification methodology documented.
- 150+ infrastructure records with zero orphan locality_id mismatches
- All unit tests pass on every push (GitHub Actions CI)
- Validation report documents every null check, GPS bounds test, and join integrity check
- Every data point has a named, dated, public source in the source registry
- A developer with no prior context can reproduce the full database from this repo alone
- The Streamlit dashboard is live and publicly accessible
- The README leads with a real, numbered finding from the actual data

---

## 11. Beyond Nagpur

The methodology, schema design, validation framework, and KPI architecture built for NagpurLens are designed to be city-agnostic from the start. The locality_id standard, source registry format, data dictionary structure, and unit test suite all generalize.

Version 2.0 expands to additional Maharashtra cities — Nashik, Aurangabad, Amravati — using the same pipeline. Version 4.0 The long-term vision includes exploring licensing, partnerships, and civic deployments if the platform demonstrates sustained value.

Nagpur is the proof of concept. The platform is the long-term vision.

---

## 12. The Team

**Mohammad Ammar** — Data Engineering, Analytics, Architecture, Project Lead
Building NagpurLens as a flagship open-source project from ACET Nagpur, pursuing a parallel track in data analytics and data science alongside his ENTC degree.

**Zahid Khan** — Website, Documentation, Community
Public-facing presence, GitHub documentation standards, and the NagpurLens website.

**Mohammad Ruwaifa** — Research, Data Collection, Verification
Primary research, locality list construction, infrastructure data collection, and source verification.

---

## 13. The Standard This Document Sets

Every file in this repository — `PROBLEM.md`, `data_dictionary.md`, `source_registry.md`, `kpi_definitions.md`, `validation_report.md`, and every file built after — must remain traceable to this document.

If a future decision cannot be justified by Sections 3, 6, 7, or 8 of this document, it is scope creep — not progress — until this document itself is deliberately and explicitly revised.

This document is the root. Everything else is a branch.
