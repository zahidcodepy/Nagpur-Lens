# NagpurLens — User Personas

> **Authors:** Mohammad Ammar · Zahid Khan · Mohammad Ruwaifa
> **Document Status:** Foundational — derived from `VISION.md` Section 9 and `PROBLEM.md` Section 5. Every persona below must trace to at least one of the three questions in `three_questions.md`.
> **Version:** v1.2
> **Last Updated:** July 2026
> **Revision History:** v1.0 (July 2026) — initial draft. v1.1 (July 2026) — corrected a miscount in Section 0 ("five platform-adjacent personas" named only four); added an explicit Primary/Secondary rubric to Section 0. v1.2 (July 2026) — HAS and MII resolved as live v1.0 KPIs upstream in `VISION.md` v1.1; Home Buyer, Property Investor, and Government/Civic Officer KPI lists updated accordingly.

---

## 0. Purpose and Structure

`VISION.md` Section 9 and `PROBLEM.md` Section 5 each define five target users — Home Buyers, Property Investors, Builders and Developers, Government and Civic Bodies, and Researchers and Urban Planners — and state that every feature must be traceable to at least one of them. This document treats those five as the **core personas** and expands one of them (Urban Planner is separated from Researcher, given how differently the two groups consume the data) while adding four **platform-adjacent personas** — Student, Developer, API Consumer, and Future Enterprise Customer — that arise directly from the engineering pipeline and open-source posture described in `VISION.md` Sections 6, 7.3, and 11.

The platform-adjacent personas are not a scope expansion. They exist because `VISION.md` Section 7.3 requires the pipeline to be reproducible by "a developer who has never spoken to the NagpurLens team," and because Section 8 and Section 11 anticipate a civic SaaS API and enterprise licensing at Version 4. These personas describe people who already interact with the repository today (a student studying the schema, a developer running the pipeline) or will interact with it once later versions ship (an API consumer, an enterprise customer). No persona in this document justifies building anything outside the version boundaries defined in `PROBLEM.md` Section 7.

For each persona, this document covers: who they are, their current workflow, their pain points, how they make decisions, the questions they ask, their current alternatives, how NagpurLens changes their workflow, which datasets they consume, which KPIs matter to them, and which future version most benefits them.

**Primary vs. Secondary, defined.** Section 11's traceability table rates each persona against each question as Primary, Secondary, or not applicable. **Primary** means the question is the main driver of that persona's decision — the platform would not serve them at all without an answer to it. **Secondary** means the question provides useful supporting context to a decision that is primarily driven by a different question. This rubric is stated once, here, so the ratings in Section 11 are a reproducible classification rather than an unstated judgment call.

---

## 1. Home Buyer

**Who they are.** An individual or family evaluating a residential property purchase in Nagpur, typically in the ₹40–80 lakh range referenced in `VISION.md` Section 2. They are not real estate professionals; this is likely one of the largest financial decisions of their life, made a small number of times.

**Current workflow.** They shortlist localities based on budget and commute distance, visit a handful of properties with a broker, and rely on the broker's verbal description of the locality's schools, hospitals, and transit access.

**Pain points.** Brokers have a commission incentive to close the sale, not to disclose infrastructure gaps. There is no independent way to check a broker's claim about a specific locality before signing.

**Decision process.** Largely trust-based, anchored on broker reputation, family recommendations, and a small number of site visits — not on any structured comparison across localities.

**Questions they ask.** *Is this locality actually as well-served as the broker claims?* Does it have adequate healthcare access relative to how many people already live there?

**Current alternatives.** Broker opinions, informal word-of-mouth, and city-level statistics from Census or national portals that do not disaggregate to the locality in question.

**How NagpurLens changes their workflow.** They can look up a specific locality's Infrastructure Density Index and Population-Infrastructure Ratio before a site visit, converting a broker's verbal claim into a checkable, sourced figure.

**Datasets consumed.** Localities table, infrastructure table.

**KPIs that matter.** Infrastructure Density Index (IDI), Population-Infrastructure Ratio (PIR), Healthcare Accessibility Score (HAS) — all live at v1.0, directly answering this persona's healthcare-access question.

**Future versions that benefit them.** Version 3 (Investment Attractiveness Score) helps them assess whether a locality is also a sound long-term hold, not just adequately served today.

---

## 2. Property Investor

**Who they are.** An individual or small-scale investor allocating capital across Nagpur localities with the goal of price appreciation, as described in `PROBLEM.md` Section 5.

**Current workflow.** They track listing prices informally across a small number of localities they already know, often relying on a network of brokers for tips on "up and coming" areas.

**Pain points.** By the time growth in a locality is visible in listing prices, much of the appreciation has already occurred. There is no integrated, locality-level growth signal to act on earlier.

**Decision process.** Pattern recognition from informal signals (broker tips, visible construction) combined with risk tolerance for a given capital amount.

**Questions they ask.** *Which localities are three to five years ahead of price appreciation?* Which underserved localities are positioned for infrastructure catch-up?

**Current alternatives.** National real estate portals such as MagicBricks and 99acres, which per `PROBLEM.md` Section 3 operate at city level and rarely disaggregate to locality granularity for Tier-2 markets.

**How NagpurLens changes their workflow.** They gain a documented Growth Signal Index and, eventually, an Investment Attractiveness Score, allowing comparison across localities on a common, auditable basis instead of informal tips.

**Datasets consumed.** Localities and infrastructure tables (v1); construction activity and metro proximity data (v2); demographic and price data (v3).

**KPIs that matter.** Growth Signal Index (GSI), Investment Attractiveness Score (IAS) drive this persona's core decision from v2.0/v3.0 onward. Metro Influence Index (MII), live from v1.0, is available earlier as a supporting connectivity signal.

**Future versions that benefit them.** Version 2 and Version 3 directly; Version 1's infrastructure baseline is a necessary input but not, on its own, sufficient for this persona's decision.

---

## 3. Builder / Developer (Real Estate)

**Who they are.** A construction firm or individual developer deciding where to build the next residential or mixed-use project in Nagpur.

**Current workflow.** Site selection based on land availability and cost, informal awareness of nearby population density, and anecdotal sense of unmet housing demand.

**Pain points.** No quantified way to confirm that a candidate site sits in a locality where population density already outpaces available infrastructure — the exact condition that signals unmet demand.

**Decision process.** Land cost and availability weighted against a qualitative read of local demand, often confirmed only after the fact by how quickly units sell.

**Questions they ask.** *Where is demand forming before supply catches up?* Which localities are population-dense but infrastructure-thin?

**Current alternatives.** Site visits, informal broker networks, and land-cost data with no infrastructure-gap overlay.

**How NagpurLens changes their workflow.** The Infrastructure Density Index and Population-Infrastructure Ratio give a quantified, locality-ranked view of where population already exceeds infrastructure supply — a direct, data-driven site-selection signal.

**Datasets consumed.** Localities and infrastructure tables.

**KPIs that matter.** Population-Infrastructure Ratio (PIR), Infrastructure Density Index (IDI), Growth Signal Index (GSI) once available.

**Future versions that benefit them.** Version 1 already serves this persona directly; Version 2 sharpens the signal with growth trajectory.

---

## 4. Urban Planner

**Who they are.** A professional — academic, consultant, or civic-adjacent planner — studying Nagpur's spatial development patterns, distinct from an NMC employee in that they are not responsible for budget allocation but for analysis and policy recommendation.

**Current workflow.** Assembling locality-level pictures manually from Census tables, NMC planning documents, and site visits, often for a specific study or report.

**Pain points.** As `PROBLEM.md` Section 3 documents, no relational structure connects population, infrastructure, and geography at the locality level, forcing manual cross-referencing across four or more sources for even a single analytical question.

**Decision process.** Structured, methodology-driven analysis, typically for a defined research or consulting deliverable with its own citation and rigor requirements.

**Questions they ask.** *Is there a research-grade, locality-level urban dataset for Nagpur I can build on?* Where does the city's growth pattern deviate from its infrastructure investment pattern?

**Current alternatives.** Manual data assembly from NMC, Census, and mapping sources, with no validation methodology to lean on.

**How NagpurLens changes their workflow.** A single validated, source-documented relational dataset replaces the manual cross-referencing step, with a published validation report they can cite directly.

**Datasets consumed.** Localities table, infrastructure table, validation report, source registry.

**KPIs that matter.** Infrastructure Density Index (IDI), Population-Infrastructure Ratio (PIR); Growth Signal Index (GSI) from Version 2 onward.

**Future versions that benefit them.** All versions incrementally; Version 2's growth modeling is particularly relevant to planning-oriented spatial analysis.

---

## 5. Government / Civic Officer

**Who they are.** A staff member or decision-maker at the Nagpur Municipal Corporation or Smart City Nagpur Limited responsible for prioritizing infrastructure investment across the city's localities, as named in `VISION.md` Section 9.

**Current workflow.** Budget allocation informed by ward-level political input, historical precedent, and ad hoc citizen complaints, without a consistent locality-level infrastructure-versus-population baseline.

**Pain points.** No integrated dataset to prioritize investment strictly by documented need across all 57+ localities; allocation risk is skewed toward localities with more political visibility rather than more measurable need.

**Decision process.** Budget-cycle driven, balancing political input against whatever quantitative data is available — which today is limited to city-level or ward-level aggregates.

**Questions they ask.** *Where are citizens most underserved relative to population density?*

**Current alternatives.** Ward-level complaint records, informal staff knowledge of specific localities, and city-level Census aggregates that hide the imbalance, per `PROBLEM.md` Section 3.

**How NagpurLens changes their workflow.** A ranked, locality-level Infrastructure Density Index and Population-Infrastructure Ratio give a defensible, publicly auditable basis for prioritization decisions, independent of political visibility.

**Datasets consumed.** Localities table, infrastructure table, validation report.

**KPIs that matter.** Population-Infrastructure Ratio (PIR), Infrastructure Density Index (IDI), Healthcare Accessibility Score (HAS) — all live at v1.0, directly supporting this persona's prioritization decision.

**Future versions that benefit them.** Version 4's civic API and government collaboration model, described in `VISION.md` Section 8, is built specifically for this persona to consume the platform's outputs at institutional scale rather than through the public dashboard alone.

---

## 6. Researcher

**Who they are.** An academic or independent researcher studying urban economics, civic equity, or real estate market efficiency in Tier-2 Indian cities, distinct from the Urban Planner in that their output is typically a paper or dataset contribution rather than a policy recommendation.

**Current workflow.** Searching for a citable, methodologically sound dataset for Nagpur and, in its absence, either excluding Nagpur from comparative studies or assembling a partial dataset manually with limited documentation of its own provenance.

**Pain points.** As `PROBLEM.md` Section 3 notes, even where Nagpur data exists, it rarely exposes its own assumptions, validation process, or quality metrics, making independent verification difficult — a direct obstacle to academic use.

**Decision process.** Governed by academic rigor standards: a dataset must be citable, its methodology auditable, and its limitations disclosed before it can be used in published work.

**Questions they ask.** *Is there a research-grade urban dataset for Nagpur I can build on?*

**Current alternatives.** City-level Census and RBI datasets, or manually assembled and undocumented locality data of unknown reliability.

**How NagpurLens changes their workflow.** A published validation report, source registry, and methodology document give them exactly the provenance and reproducibility trail required for academic citation.

**Datasets consumed.** All tables, plus the validation report and methodology document specifically.

**KPIs that matter.** All six KPIs defined in `VISION.md` Section 4, each live from the version that introduces it, with particular attention to the documented formula and any versioned revisions to it.

**Future versions that benefit them.** Version 2 and Version 3 extend the dataset's relevance to growth and investment research; Version 4's multi-city expansion, per `VISION.md` Section 11, enables comparative Tier-2 city research that is not possible with Nagpur data alone.

---

## 7. Student

**Who they are.** An undergraduate or postgraduate student — potentially in engineering, data science, or urban studies — encountering NagpurLens as a learning resource or as a foundation for a coursework or capstone project.

**Current workflow.** Searching for a real-world, non-trivial dataset and pipeline to learn from or build on top of, typically finding either toy datasets with no real-world stakes or real datasets with no documentation of how they were built.

**Pain points.** Most publicly available "real" datasets provide no visibility into the collection and validation process, so a student can practice analysis but not learn the engineering discipline (schema design, validation, CI) that produced trustworthy data in the first place.

**Decision process.** Driven by learning value and how well a project maps to a course requirement or personal skill-building goal, not by commercial or research stakes.

**Questions they ask.** *How was this data actually collected and validated? Can I reproduce this pipeline myself?*

**Current alternatives.** Kaggle datasets with unknown provenance — the exact anti-pattern `VISION.md` Section 5 contrasts NagpurLens against.

**How NagpurLens changes their workflow.** The full pipeline — research, source documentation, validation, schema design, KPI computation — is visible and reproducible end to end, giving a student a real example of engineering discipline rather than just a dataset to plot.

**Datasets consumed.** All tables; the pipeline documentation itself (`methodology.md`, `validation_report.md`) is as relevant to this persona as the data.

**KPIs that matter.** Whichever KPIs are relevant to the student's specific coursework; the formulas and their documentation matter more than any single number.

**Future versions that benefit them.** All versions equally; this persona's interest is in engineering process, which is present from Version 1 onward.

---

## 8. Developer (Open Source Contributor)

**Who they are.** A software engineer, distinct from the Student persona in that they intend to contribute code, extend the pipeline, or adapt it for another use case, consistent with the reproducibility standard in `VISION.md` Section 7.3.

**Current workflow.** Evaluating an open-source repository's documentation and CI setup before deciding whether to invest time contributing, and expecting to be able to build and test the project without contacting the maintainers.

**Pain points.** Open-source urban data projects frequently have undocumented setup steps, inconsistent schemas, or no automated tests — making contribution costly and error-prone.

**Decision process.** Evaluates build reproducibility, test coverage, and documentation clarity before committing time to a contribution.

**Questions they ask.** *Can I reproduce the full database and KPI outputs from this repository alone, with no undocumented steps?*

**Current alternatives.** Other open-source civic or real-estate data projects, most of which, per `VISION.md` Section 5, lack full validation, CI, or a documented methodology.

**How NagpurLens changes their workflow.** A CI-tested, schema-documented, source-attributed pipeline lets them verify correctness before contributing and extend the schema or KPI logic with confidence that existing tests will catch regressions.

**Datasets consumed.** All tables, plus `schema.sql`, `validation_report.md`, and the test suite itself.

**KPIs that matter.** Less the KPI values themselves than the correctness and testability of the code that computes them.

**Future versions that benefit them.** Version 4's multi-city, platform-oriented architecture, per `VISION.md` Section 11, is the version where this persona's contributions have the highest structural leverage, since a city-agnostic schema change benefits every future city onboarded.

---

## 9. API Consumer

**Who they are.** A third-party developer or organization building an external application, analysis, or integration on top of NagpurLens's data via its REST API, rather than through the dashboard.

**Current workflow.** Currently non-existent for Nagpur-specific data, since no locality-level API exists for this market; an API consumer today would have to scrape or manually assemble data from the same fragmented sources described in `PROBLEM.md` Section 3.

**Pain points.** No programmatic, structured access point to Nagpur locality-level infrastructure or investment data exists anywhere else.

**Decision process.** Evaluates API stability, documentation completeness, and data freshness before building a dependency on it.

**Questions they ask.** *Is there a stable, documented API for Nagpur locality data I can build against?*

**Current alternatives.** None specific to Nagpur; would otherwise need to build a custom scraping and validation pipeline from scratch.

**How NagpurLens changes their workflow.** The FastAPI endpoints defined in `PROBLEM.md` Section 8 (`/localities`, `/infra`, `/gap-analysis`) give them a documented, versioned data source to build against without replicating the underlying collection and validation work themselves.

**Datasets consumed.** All data exposed via the public API surface.

**KPIs that matter.** Whichever KPIs are exposed via the API at a given version; correctness and versioning of the API response schema matter more to this persona than any single KPI value.

**Future versions that benefit them.** Version 4's civic SaaS API, per `VISION.md` Section 8, is built specifically for this persona at institutional scale, though the Version 1 FastAPI endpoints already serve smaller-scale consumers.

---

## 10. Future Enterprise Customer

**Who they are.** A prospective institutional customer — a civic technology vendor, a real estate analytics firm, or a government contractor — evaluating NagpurLens for licensed data access or a collaboration, corresponding to the long-term possibility described in `VISION.md` Section 8 (v4.0) and Section 11.

**Current workflow.** Not yet applicable, since this persona's engagement model does not exist prior to Version 4; today, such an organization would have no NagpurLens-specific workflow at all.

**Pain points.** Institutional buyers require data provenance, validation guarantees, and a licensing structure before they can adopt an external dataset into their own product — none of which a project can offer credibly before Version 1 through Version 3 have established a validated track record.

**Decision process.** Procurement-driven: requires documented data quality, a clear licensing model, and evidence of the platform's reliability over multiple release cycles before committing.

**Questions they ask.** *Does this platform have a licensing model, and can its data quality be independently verified before we commit to it?*

**Current alternatives.** Building an equivalent Nagpur (or Tier-2 city) dataset in-house, or foregoing locality-level Tier-2 data entirely.

**How NagpurLens changes their workflow.** By the time this persona engages, the platform's public validation reports, methodology documentation, and multi-version track record (Sections 1–8 of this document) serve as the due-diligence trail an institutional buyer requires — something this persona could not obtain by any other channel for this market.

**Datasets consumed.** Full dataset, under whatever licensing terms are defined at v4.0.

**KPIs that matter.** All KPIs, evaluated for reliability across versions rather than any single figure.

**Future versions that benefit them.** Version 4 exclusively — this persona does not exist as an active user prior to it, per the explicit "long-term vision" framing of licensing and civic deployment in `VISION.md` Section 11.

---

## 11. Persona-to-Question Traceability

Ratings below follow the Primary/Secondary rubric defined in Section 0.

| Persona | Question 1 (Infrastructure Gap) | Question 2 (Growth) | Question 3 (Investment) |
|---|---|---|---|
| Home Buyer | Primary | — | Secondary |
| Property Investor | Secondary | Primary | Primary |
| Builder / Developer | Primary | Secondary | — |
| Urban Planner | Primary | Secondary | — |
| Government / Civic Officer | Primary | Secondary | — |
| Researcher | Primary | Primary | Primary |
| Student | Primary (pipeline-focused) | — | — |
| Developer | Primary (schema-focused) | — | — |
| API Consumer | Primary | Secondary (v2+) | Secondary (v3+) |
| Future Enterprise Customer | — | — | Primary (v4) |

Every persona in this document maps to at least one question in `three_questions.md`. A future feature proposed for a persona that cannot be placed in this table should be treated as scope creep until it can be justified against `VISION.md`, consistent with the governance standard set in Section 13 of that document.
