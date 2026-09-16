---
title: "DGGS as a Spatial Harness for AI Agents at the 2026 ISPRS Congress"
layout: news
date: 2026-07-09
redirect_from:
  - /DGGS-Spatial-Harness-for-AI-ISPRS-Congress/

---
![Presenting at the 2026 ISPRS Congress Forum session in Toronto](/assets/img/20260709/isprs-forum.jpg)

**At the XXV ISPRS Congress in Toronto, I gave a Forum talk on how Discrete Global Grid Systems can act as a spatial harness for AI agents. The core argument is simple: an AI agent is a language model plus a harness, and DGGS is the harness that gives spatial work the structure, scale, and traceability that language alone cannot provide.** [View the slides](/assets/pdf/slides/2026-07-ISPRS-Forum.pdf)

Large language models are strong at interaction, planning, and explanation. They are far less reliable when spatial relationships must be inferred from raw coordinates, map images, or free text. My talk walked through two projects that put DGGS underneath the model, so the agent explains behavior instead of inventing geography.

## The Session

The talk was part of Forum 9A, *Exploring the Role of DGGS and AI in Addressing Challenges of National Mapping and Remote Sensing Agencies*, held on 9 July 2026. The session brought together work on DGGS foundations, DGGS-based analytics, and the OGC and ISO standardization effort, followed by a panel discussion among the presenters.

## Project 1: DGGS-Q, Traceable Natural-Language Querying

The first project, **DGGS-Q**, is a DGGS-grounded multi-agent system that turns natural-language spatial questions into traceable query workflows over harmonized methane emission inventories.

The motivation is data fragmentation. Spatial data arrive in inconsistent coordinate reference systems, formats, resolutions, and semantics, and that inconsistency slows human decisions and causes AI models to hallucinate. DGGS addresses this by unifying four dimensions:

- **Spatial**: an equal-area global grid unifies coordinate systems.
- **Temporal**: consistent time-indexed snapshots support change analysis.
- **Scale**: a hierarchical, multi-resolution structure supports aggregation and zooming.
- **Semantic**: a common feature schema aligns attributes across sources.

The work has two parts. First, we harmonized 15 emission inventories onto the rHEALPix DGGS using DGGAL, standardizing sectoral semantics to the IPCC 2006 scheme and reporting units to Mg a⁻¹, and applying a scaling factor to conserve total emissions after conversion. The result is stored in a DGGS-indexed relational backend and is publicly available.

Second, a multi-agent system turns questions into DGGS-aware queries. A reasoner generates a step-by-step execution plan and replans on failure, while a coordinator routes work to specialized agents: an intent parser extracts the task and variables, a geo-resolver maps location text to DGGS cell identifiers, a data-query agent writes and runs SQL using DGGS prefix matching, and a validator checks the answer against the retrieved data. Because every answer cites specific DGGS cells, datasets, and SQL, the whole workflow is auditable rather than a black box.

## Project 2: GridMind, Reasoning Grounded in DGGS Topology

The second project, **GridMind**, is ongoing. It asks whether DGGS can serve not just as a query index but as a substrate for spatial reasoning itself.

Spatial reasoning derives new facts from relations such as adjacency, containment, hierarchy, and proximity. These feel intuitive to people, but language models infer them unreliably. GridMind removes that guesswork by indexing space with rHEALPix cells and deriving the relations directly from cell identifiers: parent and child cells give hierarchy, neighboring cells give adjacency, and features are linked to their containing cell. The model explains what happens; it does not invent the spatial relationships.

The system treats both cells and features as agents, demonstrated in an oil and gas asset management scenario:

- **Grid-cell agents** represent spatial units at multiple resolutions and summarize local and regional conditions.
- **Feature agents** represent domain entities such as facilities, leaks, sensors, and repairs, each bound to its containing cell.

Communication follows the grid topology through three channels. **Vertical** links between parent and child cells support cross-resolution reasoning, so fine cells roll up to regional summaries and coarse cells drill down to local detail. **Lateral** links between neighboring cells support propagation and pattern detection, such as tracking a leak that may spread. **Inward** links let a facility or sensor report its status to the cell that contains it. The system is event-driven, so agents stay dormant until a leak event, a sensor reading, a neighbor message, or a user question reaches them.

## The Take-Home Message

I closed with the framing that ran through both projects: DGGS is a spatial harness for AI agents.

- **Data**: DGGS standardizes fragmented spatial datasets across space, scale, time, and semantics.
- **Querying**: DGGS-Q makes natural-language geospatial queries traceable, explainable, and auditable.
- **Reasoning**: GridMind uses DGGS topology to ground adjacency, hierarchy, and containment.

The language model provides interaction, planning, and explanation. DGGS provides the spatial structure that makes the whole system reliable.

## Panel Discussion

I also served as one of the panelists in the session's discussion. The conversation focused on turning DGGS from a research idea into operational practice, organized around questions including:

- The biggest challenges in deploying DGGS for real-world applications such as disaster management.
- Performance bottlenecks, particularly quantization, and how to mitigate them through staging databases and cell-native geometry generation.
- Where processing, queries, and filtering should happen: on the client, on the server, or in an orchestrating mediation service.
- How to incorporate real-time and dynamic disaster data.
- Which use cases are well suited to DGGS, and which are clearly ill suited.
- How supporting tools and approaches can be better promoted given the potential of DGGS.

These questions map closely onto the two systems I presented, especially the trade-offs around where computation lives and how to keep large-scale queries fast without losing traceability.

---

***DGGS gives AI agents a stable place to stand. I am continuing to build out GridMind so that grounded spatial reasoning becomes a practical substrate, not just a demo.***
