# NagpurLens — The Three Questions

> **Authors:** Mohammad Ammar · Zahid Khan · Mohammad Ruwaifa
> **Document Status:** Foundational — derived from `VISION.md` and `PROBLEM.md`. Every KPI, table, and dashboard view in this repository must trace back to one of the three questions defined here.
> **Version:** v1.2
> **Last Updated:** July 2026
> **Revision History:** v1.0 (July 2026) — initial draft. v1.1 (July 2026) — added an "Open Items" section flagging two unresolved conflicts between `VISION.md` and `PROBLEM.md`; added an explicit fallback commitment to Section 2.5 for the Growth Signal Index's population-movement input. v1.2 (July 2026) — both open items resolved upstream in `VISION.md` v1.1 and `PROBLEM.md` v1.1 (KPI set reconciled to six version-tagged KPIs; roadmap's pre-1.0 price-data conflict removed); Open Items section removed, and HAS/MII folded into Version 1's KPI outputs throughout.

---

## 0. Purpose of This Document

`VISION.md` states that NagpurLens exists to answer three specific questions, in a fixed order of version and importance. `PROBLEM.md` restates them as the three core problems the platform is built to solve. Neither document explains, at engineering depth, *why* these three questions were chosen over any of the dozens of other questions one could ask about Nagpur's urban data.

This document is that explanation. It exists so that no future contributor has to guess why Version 1 stops at infrastructure and does not touch price data, or why growth modeling is deferred to Version 2 instead of being folded into Version 1 for convenience. Every KPI defined in `kpi_definitions.md`, every table in `schema.sql`, and every dashboard panel in the Streamlit product must be traceable to one of the three sections below. If a proposed feature cannot be mapped to a question here, it does not belong in the current version — it belongs in a future one, or it does not belong in NagpurLens at all.

The three questions are ordered by dependency, not by difficulty. Each question requires the data foundation and validated outputs of the question before it. This is why the roadmap in `VISION.md` Section 8 is sequential and why Section 7.6 ("Depth Before Breadth") forbids starting a later question before the earlier one is fully validated.

---

## 1. Question 1 — Where does infrastructure lag despite having population?

### 1.1 Background

Nagpur's Municipal Corporation manages civic infrastructure across more than fifty distinct localities that differ enormously in age, planning history, and investment priority. Localities such as Dharampeth, Civil Lines, and Sitabuldi were developed decades ago under earlier municipal planning cycles and have accumulated dense infrastructure — hospitals, schools, markets, and transit access — over that time. Peripheral localities such as Hingna, Hudkeshwar, and Wathoda have absorbed a large share of Nagpur's population growth since 2001 without a matching build-out of civic infrastructure.

This is not a Nagpur-specific anomaly. It is the standard pattern in Tier-2 Indian cities, where population growth at the urban periphery consistently outpaces the civic planning cycle. What is specific to Nagpur — and to nearly every city of its size — is that this imbalance has never been quantified at the locality level with a dataset anyone can inspect, audit, or reproduce.

### 1.2 Why It Matters

An imbalance that is known informally ("everyone knows Hudkeshwar is underserved") but not quantified cannot be acted on systematically. A civic body cannot allocate a limited infrastructure budget based on informal consensus. A family cannot weigh a broker's claim about a locality against a documented figure. A researcher cannot cite "everyone knows" in a paper on civic equity.

Quantification converts an anecdotal imbalance into an actionable one. A locality with a computed Population-Infrastructure Ratio in the bottom decile is a defensible target for civic investment. A locality with a documented Infrastructure Density Index below the city median is a defensible red flag for a home buyer. Without the number, both parties are guessing. With the number, both parties are working from the same evidence.

### 1.3 Who Benefits

- **Home buyers** evaluating a ₹40–80 lakh purchase gain a way to check a broker's claim about a locality's infrastructure against a verified, dated figure rather than accepting it on trust.
- **The Nagpur Municipal Corporation and Smart City Nagpur Limited** gain a locality-ranked view of where infrastructure investment is most urgently needed relative to population, rather than relying on ward-level political pressure alone.
- **Builders and developers** gain a way to identify localities where population density already justifies new infrastructure-adjacent development, ahead of formal civic announcements.
- **Researchers and urban planners** gain a citable, source-documented dataset for studying civic equity in a Tier-2 Indian city — a category of city that is systematically under-studied relative to Tier-1 metros.

### 1.4 Current Limitations

No public dataset currently answers this question for Nagpur at the locality level. National datasets (Census, RBI housing reports) operate at city or district granularity and therefore hide exactly the imbalance this question is trying to reveal — a pattern documented in `PROBLEM.md` Section 3 under "No Locality-Level Granularity." Locality-level data that does exist is fragmented across NMC portals, mapping services, and Census tables, with no single source integrating them, no consistent locality identifier across sources, and no documented verification process. GPS coordinates in informal sources are frequently approximate rather than surveyed, and infrastructure counts are frequently informal estimates rather than dated, sourced records.

Within NagpurLens itself, Version 1's own limitation must be stated plainly, consistent with the Vision's principle that limitations are stated, not hidden (Section 7.4): Census 2011 is the most recent uniformly available locality-level population dataset, and it is more than a decade old at the time of writing. The Infrastructure Density Index and Population-Infrastructure Ratio computed in Version 1 are therefore accurate relative to a 2011 population baseline, not a 2026 one. This is disclosed in every output, not hidden in a footnote.

### 1.5 Required Datasets

- **Localities table:** 50+ Nagpur localities, each with GPS coordinates verified against independent geographic references, NMC zone classification, area, and Census 2011 population, as specified in `VISION.md` Section 4.
- **Infrastructure table:** 150+ records across nine categories — hospitals, schools, colleges, metro stations, bus stops, markets, police stations, fire stations, and parks — each with documented coordinates, a named and dated source, and a verification status.
- **Locality-infrastructure linkage:** every infrastructure record correctly assigned to exactly one locality via the haversine nearest-centroid validation method defined in `VISION.md` Section 4, with zero orphan records.

### 1.6 Expected Outputs

- `localities_final.csv` and `infra_final.csv` — the validated source tables.
- `schema.sql` and `seed_data.sql` — the relational database implementing the locality-infrastructure relationship with enforced foreign key constraints.
- `kpi_outputs.csv` — Infrastructure Density Index (IDI), Population-Infrastructure Ratio (PIR), Healthcare Accessibility Score (HAS), and Metro Influence Index (MII) computed and ranked for every locality, per the versioned KPI list in `VISION.md` Section 4. HAS and MII require no data beyond the Version 1 infrastructure table and are therefore delivered alongside IDI and PIR rather than deferred.
- `validation_report.md` — documenting GPS bounds tests, join integrity checks, null checks, and the haversine correction log, all passing.
- A Streamlit dashboard view ranking localities by infrastructure gap, and a FastAPI `/gap-analysis` endpoint exposing the same computation programmatically.

### 1.7 Version Responsible

**Version 1** answers this question in full, per `VISION.md` Section 3 and `PROBLEM.md` Section 7. It is explicitly scoped to Problem 1 only; property price data, growth modeling, and the Investment Attractiveness Score are out of scope for Version 1 regardless of how straightforward they might appear to add alongside the infrastructure work.

### 1.8 Future Evolution

The Infrastructure Density Index and Population-Infrastructure Ratio computed in Version 1 become direct inputs to the Growth Signal Index in Version 2 and to the Investment Attractiveness Score in Version 3. Their correctness in Version 1 is therefore not just a Version 1 concern — an error in the population-infrastructure baseline propagates into every later score. This is the concrete reason `VISION.md` Section 7.6 insists that no version begin before the one before it is fully validated. As Census data ages further, later versions may need to incorporate updated population estimates from NMC ward records or a future Census cycle; any such change will be versioned and documented rather than silently substituted.

---

## 2. Question 2 — Which localities demonstrate measurable urban growth?

### 2.1 Background

Urban growth in Nagpur is visible on the ground long before it appears in any published dataset. A new metro station, a cluster of new construction permits, a market that has recently opened — these are all signals that a locality is gaining momentum. They exist today across several disconnected sources: NMC project announcements, the Nagpur Metro's own expansion plans, Census population trends, and property listing volumes. No platform currently integrates these signals into a single, locality-level, queryable indicator.

This question depends on Question 1 being answered first. A growth signal is only meaningful relative to a documented baseline — a locality cannot be said to be "catching up" on infrastructure unless its infrastructure gap was already quantified. This is why Version 2, not Version 1, addresses this question.

### 2.2 Why It Matters

Growth that is visible informally but not measured cannot be acted on ahead of the market pricing it in. By the time a locality's growth is obvious to everyone — reflected in listing prices, broker commentary, and word of mouth — much of the appreciation opportunity has already passed. A Growth Signal Index computed from documented construction activity, metro proximity, and infrastructure investment trends gives an investor, builder, or researcher a way to identify momentum earlier and on an auditable basis, rather than relying on the same broker commentary that `PROBLEM.md` Section 1 identifies as the core problem NagpurLens exists to replace.

### 2.3 Who Benefits

- **Property investors** gain a way to identify localities that are three to five years ahead of price appreciation, based on documented signals rather than broker intuition.
- **Builders and developers** gain a way to identify where housing demand is forming before supply catches up, informing where the next development belongs.
- **Home buyers** gain a way to distinguish a locality that appears affordable because it is growing from one that appears affordable because it is declining — a distinction that is invisible from price alone.
- **Government and civic bodies** gain a secondary lens on where infrastructure investment is likely to face rising demand pressure, complementing the Question 1 gap analysis with a forward-looking view.

### 2.4 Current Limitations

Growth signals for Nagpur are not currently integrated anywhere. Construction activity data is not published at the locality level in a structured form. Metro expansion plans are published but not linked to locality identifiers usable in a relational database. Property listing volumes, where available, come from commercial portals that operate at the city level and, per `PROBLEM.md` Section 3, rarely disaggregate to locality granularity for Tier-2 markets. Building a Growth Signal Index therefore requires assembling and normalizing several disconnected, differently structured sources — a nontrivial engineering task, not a data-availability problem alone.

### 2.5 Required Datasets

- Everything produced in Version 1: the validated locality and infrastructure tables, and the computed IDI and PIR baselines.
- A construction-activity signal, sourced from NMC building permit records or equivalent documented public sources.
- Metro proximity data, extending the existing infrastructure table's metro station records into a distance-based influence measure.
- Population movement trends, to the extent a documented, locality-level source becomes available beyond the 2011 Census baseline.

**Fallback commitment:** if a documented population-movement source is not available by the point Version 1 is validated and Version 2 begins, the Growth Signal Index still ships at v2.0 computed from whichever of its inputs — construction activity, metro proximity, infrastructure investment trends — are validated at that time. Any input not yet available is explicitly listed as deferred in `kpi_definitions.md`, with the GSI formula versioned accordingly, rather than the release being blocked indefinitely on a data source outside the team's control. This keeps Section 7.6's "Depth Before Breadth" principle from becoming an open-ended excuse to never ship Version 2.

### 2.6 Expected Outputs

- A Growth Signal Index (GSI) computed and ranked per locality, combining construction activity, metro proximity, and infrastructure investment trends as defined in `VISION.md` Section 4, with any deferred input documented per Section 2.5 above.
- An expanded validation report covering the new data sources and their join integrity against the existing locality table.
- Dashboard and API extensions exposing GSI rankings alongside the existing infrastructure gap ranking, so a user can view both the current state (Question 1) and the trajectory (Question 2) for any locality.

### 2.7 Version Responsible

**Version 2** answers this question, per `VISION.md` Section 3 and the roadmap in Section 8 (v2.0 — "Growth Intelligence").

### 2.8 Future Evolution

The Growth Signal Index becomes a direct input to the Investment Attractiveness Score in Version 3, alongside the Version 1 infrastructure metrics. As with Question 1's outputs, any weighting or methodology decision made in the GSI calculation must be documented and versioned, since it will be inherited by every later score built on top of it.

---

## 3. Question 3 — Which localities demonstrate stronger long-term investment potential based on documented indicators?

### 3.1 Background

Property investment decisions in Nagpur are currently made on incomplete and commercially biased information, as documented in `PROBLEM.md` Section 2, Problem 3. National real estate portals operate at the city level and rarely provide locality-level intelligence for Tier-2 markets. No public tool combines infrastructure health, growth trajectory, and demographic signals into a single, objective, auditable score for Nagpur localities.

This question is the synthesis point of the platform. It depends entirely on Questions 1 and 2 being answered and validated first, since the Investment Attractiveness Score is explicitly defined in `VISION.md` Section 4 as a composite of infrastructure health (IDI, PIR), accessibility (HAS), connectivity (MII), and growth trajectory (GSI) — all of which are outputs of the earlier two questions.

### 3.2 Why It Matters

A single composite score is only trustworthy if every component feeding into it is independently documented, verified, and auditable — which is precisely why this question cannot be attempted before Questions 1 and 2 are complete. An investment score built on unverified components would be, in the language of `VISION.md` Section 7.1, "a guess with a chart on top." The Investment Attractiveness Score is designed to be the opposite: a number where every input, every weight, and every formula revision is public and traceable.

### 3.3 Who Benefits

- **Property investors** allocating capital gain a documented, auditable basis for comparing localities, rather than the subjective and commercially biased information described in `PROBLEM.md` Section 2.
- **Builders and developers** gain a quantified signal for where underserved demand exists, supporting site-selection decisions.
- **Researchers** studying real estate market efficiency in Tier-2 Indian cities gain a verified dataset and a transparent scoring methodology to test, critique, or build upon.
- **Government and civic bodies** gain a way to see how their own infrastructure investment decisions (Question 1) and observed growth patterns (Question 2) combine into a market-facing signal, closing the loop between civic planning and private investment behavior.

### 3.4 Current Limitations

Because this question depends on the outputs of Questions 1 and 2, it inherits every limitation documented in those sections — most notably the Census 2011 population baseline and the absence, at present, of a structured construction-activity data source. In addition, the specific weighting methodology for the Investment Attractiveness Score is, per `VISION.md` Section 4, not fixed at the outset: it is expected to evolve based on validation, expert review, and empirical evaluation. Every revision to the weighting will be documented rather than applied silently, so that historical scores remain interpretable against the methodology version that produced them.

The accessibility component of the Investment Attractiveness Score is the Healthcare Accessibility Score (HAS), and the connectivity component is the Metro Influence Index (MII) — both delivered in Version 1 per `VISION.md` Section 4, so both are already validated, auditable inputs by the time Version 3 begins to synthesize them.

### 3.5 Required Datasets

- The complete Version 1 infrastructure and locality dataset.
- The complete Version 2 Growth Signal Index dataset.
- Demographic growth signals beyond the static 2011 population figure, to the extent documented sources become available.
- Property price and transaction data, explicitly out of scope for Version 1 per `PROBLEM.md` Section 7, but required as an input once this question is addressed.

### 3.6 Expected Outputs

- An Investment Attractiveness Score (IAS) computed, ranked, and published per locality, with the full weighting formula documented in `kpi_definitions.md`.
- A methodology document explaining every weighting decision and its evidentiary basis.
- Dashboard and API exposure of the IAS alongside its component scores, so a user can inspect not just the final number but how it was derived.

### 3.7 Version Responsible

**Version 3** answers this question, per `VISION.md` Section 3 and the roadmap in Section 8 (v3.0 — "Investment Intelligence").

### 3.8 Future Evolution

Once Version 3 is validated, Version 4 shifts focus from answering a new question to scaling the existing answers — civic API access, government collaboration, and data licensing, as described in `VISION.md` Section 8 (v4.0) and Section 11. The three questions themselves do not change in Version 4; what changes is who can access the answers and at what scale. Section 11 also establishes that the methodology built to answer these three questions for Nagpur is intended to generalize to other Maharashtra cities, meaning any future refinement to how a question is answered must remain city-agnostic rather than Nagpur-specific.

---

## 4. Summary

| Question | Core Output | Version | Depends On |
|---|---|---|---|
| Where does infrastructure lag despite population? | Infrastructure Density Index, Population-Infrastructure Ratio, Healthcare Accessibility Score, Metro Influence Index | v1.0 | Validated locality + infrastructure tables |
| Which localities demonstrate measurable growth? | Growth Signal Index | v2.0 | Version 1 outputs |
| Which localities have stronger long-term investment potential? | Investment Attractiveness Score | v3.0 | Version 1 and Version 2 outputs |

Every table, KPI, dashboard panel, and API endpoint in this repository exists to answer one of the three rows above. If it does not, it does not belong in the current scope.
