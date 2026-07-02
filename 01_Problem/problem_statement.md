# NagpurLens — Problem Statement

> **Authors:** Mohammad Ammar  · Zahid Khan · Mohammad Ruwaifa
> **Document Status:** Foundational — derived from `VISION.md`. Every claim here is traceable to that document. Nothing here contradicts it.
> **Version:** v1.0
> **Last Updated:** July 2026

---

> *This document defines the problem. Not the solution. The solution lives in the schema, the data standards, and the system design documents — all of which trace back here.*

---

## 1. Background — The City Without a Data Layer

Nagpur is the geographic center of India. It is a Smart City Mission beneficiary. It has an operational metro rail network and an active Nagpur Municipal Corporation managing civic infrastructure across dozens of localities. Between 2001 and 2011, Nagpur's urban population grew significantly, with peripheral localities absorbing large portions of that growth.

None of this growth has been matched by a corresponding public data intelligence layer.

Walk into any real estate office in Dharampeth, Hingna, or Hudkeshwar. You will receive broker opinions. You will receive commission-driven advice. You will receive informal estimates based on recent transactions a broker happened to witness. What you will not receive is structured, verified, locality-level data.

Citizens in Nagpur — home buyers, investors, builders, urban planners — make major decisions without reliable information. **This is the problem NagpurLens exists to solve.**

---

## 2. The Three Core Problems

NagpurLens is built to answer three specific questions. These are not academic exercises. They are the actual questions real people in Nagpur cannot currently answer with data.

---

### Problem 1 — Where does infrastructure lag despite having population?

Infrastructure investment in Nagpur is not uniformly distributed. Established localities — Dharampeth, Civil Lines, Sitabuldi — receive consistent civic investment. Peripheral and rapidly growing localities — Hingna, Hudkeshwar, Wathoda — often absorb large population without proportionate infrastructure development.

The problem is not that this imbalance exists. Every city has imbalances. **The problem is that no verified, structured dataset exists to quantify it at the locality level.**

Without this data:
- A family cannot know whether the locality they are buying into has adequate healthcare access relative to its population
- The NMC cannot prioritize infrastructure investment using population-to-infra ratios
- A researcher cannot study Nagpur's civic equity with locality-level precision
- An investor cannot identify which underserved localities are positioned for infrastructure catch-up

**What is missing:** A verified, locality-level dataset mapping infrastructure supply against population demand — producing a quantified Infrastructure Gap Score for every locality in Nagpur.

**Version 1 addresses this problem.**

---

### Problem 2 — Which localities demonstrate measurable urban growth?

Urban growth in Nagpur is visible on the ground — new construction, new metro stations, new markets — but invisible in any integrated data system. Growth signals exist across multiple disconnected sources: NMC project announcements, metro expansion maps, Census data, property listing volumes. No platform integrates these signals into a single, queryable growth indicator at the locality level.

Without this data:
- An investor cannot identify which localities are 3–5 years ahead of price appreciation
- A builder cannot identify where demand is forming before supply catches up
- A homebuyer cannot distinguish between a locality that looks affordable because it is growing versus one that looks affordable because it is declining

**What is missing:** A Growth Signal Index that combines construction activity, metro proximity, infrastructure investment trends, and population movement into a single ranked output per locality.

**Version 2 addresses this problem.**

---

### Problem 3 — Which localities demonstrate stronger long-term investment potential based on documented indicators?

Property investment decisions in Nagpur are made on incomplete, subjective, and commercially biased information. Brokers have commission incentives. National real estate portals — MagicBricks, 99acres — operate at city level and rarely provide locality-level intelligence for Tier-2 markets. No public tool exists that combines infrastructure health, growth trajectory, and demographic signals into an objective, auditable investment score for Nagpur localities.

Without this data:
- An investor allocating ₹50 lakhs has no data-driven basis for choosing between two localities
- A builder deciding where to develop next has no quantified signal for where demand is underserved
- A researcher studying real estate market efficiency in Tier-2 cities has no verified dataset to work with

**What is missing:** An Investment Attractiveness Score — The weighting methodology is versioned and may evolve based on validation, expert review, and empirical evaluation. Every revision will be documented.

**Version 3 addresses this problem.**

---

## 3. Why Existing Information Cannot Solve This

Data about Nagpur exists. The problem is not absence of data — it is the condition of data that exists.

### Fragmentation
Infrastructure data lives across NMC portals, Google Maps, Census India, MSRTC route maps, and Nagpur Metro's published station lists. No single source integrates them. A person trying to answer "how many hospitals serve Hingna relative to its population?" must manually cross-reference four or more sources, with no guarantee of consistency.

### No Locality-Level Granularity
National datasets — Census 2011, RBI housing reports, national real estate indices — operate at city or district level. Nagpur as a whole may appear adequately served by healthcare infrastructure. Nagpur broken into 57 localities reveals that this infrastructure is concentrated in 8–10 localities, leaving the rest severely underserved. **City-level data hides the problem that locality-level data reveals.**

### Unverified Provenance
Data that does exist for Nagpur localities is often undated, unsourced, and unverified. GPS coordinates are approximate. Infrastructure counts are estimates. Population figures are extrapolated without methodology. A platform built on this data produces outputs that look precise but are not reliable.

### No Relational Structure
Even when data exists, it is not connected. Infrastructure records are not linked to localities. Localities are not linked to population. Population is not linked to infrastructure density. Disconnected data cannot answer relational questions — and the three questions NagpurLens answers are all relational by nature.

### No Validation Pipeline
No existing Nagpur data source publishes a validation report, a unit test suite, or a join integrity check. There is no way to know whether the data is correct — only to assume it is.
Even when datasets are publicly available, they rarely expose their assumptions, validation process, or quality metrics, making independent verification difficult.

---

## 4. The Shift NagpurLens Makes

Most data tools answer descriptive questions. NagpurLens answers decision-support questions.

| Descriptive question | NagpurLens decision-support question |
|---|---|
| How many hospitals are in Nagpur? | Which localities have fewer than 1 hospital per 10,000 residents? |
| What is Nagpur's population? | Which localities are population-dense but infrastructure-thin? |
| Where is the metro? | Which localities fall within the metro influence zone? |
| What are property prices in Nagpur? | Which localities are undervalued relative to their infrastructure score? |

This shift — from isolated statistics to integrated, relational, decision-support intelligence — is the core contribution of NagpurLens.

---

## 5. Target Users

Five users have a direct, specific stake in NagpurLens answering these three questions. Every feature, every KPI, and every table in this system exists because it serves at least one of them.

**Home Buyers**
Making a ₹40–80 lakh decision in Nagpur's real estate market without reliable locality-level data. They need to know: *Is this locality actually as well-served as the broker claims?*

**Property Investors**
Allocating capital across Nagpur localities without a quantified growth or infrastructure signal. They need to know: *Which localities are positioned for appreciation before the market prices it in?*

**Builders and Developers**
Choosing where to develop next without verified data on where population density outpaces infrastructure supply. They need to know: *Where is demand forming before supply catches up?*

**Government and Civic Bodies — NMC, Smart City Nagpur Limited**
Prioritizing infrastructure investment across 57+ localities with constrained budgets and no integrated locality-level dataset. They need to know: *Where are citizens most underserved relative to population?*

**Researchers and Urban Planners**
Needing a validated, source-documented, reproducible dataset for academic or policy work. They need: *A research-grade urban dataset for Nagpur that I can audit, cite, and build upon.*

---

## 6. Why This Problem Has Not Been Solved

Three reasons explain why this problem exists in 2026 for a city of Nagpur's size and importance:

**Tier-2 market neglect.** National real estate and civic data platforms invest in Tier-1 cities. Mumbai, Pune, Bengaluru, Hyderabad receive attention because the market size justifies it. Nagpur — despite being a Smart City Mission beneficiary with a metro network and significant NMC investment — is below the threshold where commercial platforms allocate resources.

**Data collection requires ground-level work.** Building a verified locality dataset for Nagpur requires manually collecting GPS coordinates, cross-verifying infrastructure records source by source, and applying haversine validation to ensure every infrastructure record is correctly mapped to its locality. This is not work that can be scraped or automated from existing sources — it requires deliberate, documented, human-verified effort.

**No one has treated it as an engineering problem.** The gap between "data exists somewhere" and "data is structured, validated, and queryable" is an engineering gap, not a data gap. Closing it requires schema design, normalization, validation pipelines, and documentation standards — not just data collection. This work has not been done for Nagpur because it has not been framed as an engineering problem worth solving.

NagpurLens frames it as exactly that.

---

## 7. Version 1 Scope

This document describes the full three-problem space NagpurLens is built to address. Version 1 addresses **Problem 1 only** — Infrastructure Gap Analysis.

### In Scope — Version 1
- 50+ Nagpur localities with verified GPS coordinates and NMC zone classification
- 150+ infrastructure records across 9 categories with named, dated sources
- MySQL relational database with enforced foreign key constraints
- Infrastructure Density Index and Population-Infrastructure Ratio computed for every locality
- Full validation report — GPS bounds, join integrity, null checks, haversine correction log
- Automated unit tests via GitHub Actions CI
- Streamlit dashboard — locality map, infrastructure gap ranking, locality profile
- FastAPI REST endpoints for localities and infrastructure data
- Public website
- Complete methodology documentation

### Out of Scope — Version 1
- Property price data
- Growth signal modeling
- Investment Attractiveness Score
- Machine learning models
- Multi-city expansion
- Real-time data

Scope is fixed. Features not listed above are not Version 1 features regardless of how useful they appear. They belong to the roadmap.

---

## 8. Expected Outputs

Version 1 produces the following verifiable, concrete outputs:

| Output | Description |
|---|---|
| `localities_final.csv` | 50+ verified Nagpur localities with GPS, zone, area, population |
| `infra_final.csv` | 150+ infrastructure records with GPS, type, source, verification status |
| `schema.sql` | MySQL schema with enforced FK constraints |
| `seed_data.sql` | Full database seed from validated CSVs |
| `validation_report.md` | GPS bounds test, join integrity, null check, source audit — all PASS |
| `kpi_outputs.csv` | IDI and PIR computed for every locality, ranked |
| Streamlit dashboard | Live at streamlit.io — map, gap ranking, locality profiles |
| FastAPI | Live REST API — `/localities`, `/infra`, `/gap-analysis` endpoints |
| Public website | NagpurLens landing page on GitHub Pages |
| `methodology.md` | Every decision explained, every assumption stated |

---

## 9. Boundary of This Document

This document defines the problem. Not the solution.

The solution — schema design, data standards, KPI formulas, system architecture, validation methodology — lives in separate documents, all of which trace back here:

- `data_dictionary.md` — defines what data is collected and why
- `source_registry.md` — documents where every data point came from
- `kpi_definitions.md` — defines how each KPI is computed
- `validation_report.md` — proves the data is correct
- `methodology.md` — explains every analytical decision

If a future design decision cannot be traced back to one of the three problems in Section 2, it does not belong in Version 1.

---

## 10. Closing Statement

Nagpur deserves better than broker opinions and fragmented civic portals. Its residents deserve verified data when making major financial decisions. Its government deserves a tool that identifies where infrastructure investment is most needed. Its researchers deserve a reproducible, source-documented dataset they can actually cite.

NagpurLens is being built to fill that gap — with engineering discipline, full transparency, and data that earns trust by being auditable, not just by looking polished.

The problem is real. The data gap is real. The platform is being built.

