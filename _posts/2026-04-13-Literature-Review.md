---
title: "Geospatial Reasoning, LLMs, and Multi-Agent Systems: A Brief Literature Review"
layout: post
---

**Scope.** This review covers ~25 papers published between 2023 and 2026 at the intersection of geospatial reasoning, large language models, and multi-agent systems. The focus is on GIS-domain journals (IJGIS, IJDE, JAG, TGIS, Annals of GIS, Big Earth Data, GeoInformatica), machine learning venues (ICLR, ICML, NeurIPS, ACM SIGSPATIAL), and relevant preprints. The goal is to map what the community is actively pursuing, and — more importantly — to identify gaps that deserve attention.

---

## 1. What Is Hot

### 1.1 Autonomous GIS Agents

The dominant research theme since 2023 is building LLM-powered agents that perform GIS tasks from natural language input. Li and Ning (2023) set the agenda with five autonomy goals (self-generating, self-organizing, self-verifying, self-executing, self-growing), and the Penn State group subsequently delivered two implementations: GIS Copilot (Akinboyewa et al. 2025), a QGIS plugin with RAG over 390 tools, and LLM-Find (Ning et al. 2025), a data retrieval agent with handbook-driven knowledge injection. A community vision paper by 16 GIScience scholars (Li et al. 2025) formalized five autonomy levels and surveyed 24 existing agents, finding that most achieve only Level 2 (workflow generation).

Other single-agent frameworks include GeoGPT (Zhang et al. 2024), which orchestrates 18 GIS tools through a ReAct loop; GeoCogent (Hou et al. 2025), which integrates RAG over 8,729 functions with CRS inference and spatial extent parsing modules; and Spatial-Agent (Bao et al. 2026), which formalizes geo-analytical QA as concept transformation using GeoFlow Graphs grounded in Kuhn's core spatial concepts.

**Shared pattern.** All systems place a single LLM at the center: the LLM plans, decomposes, selects tools, generates code, and self-corrects. Spatial data is passive input to the reasoning process.

### 1.2 Multi-Agent Geospatial Frameworks

A second wave (2025-2026) decomposes geospatial workflows across multiple LLM agents with specialized roles:

- **GeoColab** (Wu et al. 2025): product manager, algorithm engineer, and programmer collaborating on code generation, improving 7.6--26.1% over single-agent baselines.
- **GeoLLM-Squad** (Lee et al. 2025): orchestrator + five domain sub-agents (agriculture, climate, urban, forestry, vision) distributing 521 tools, achieving 60.29% correctness — 17% above single-agent systems.
- **GeoJSON Agents** (Luo et al. 2026): planner-worker architecture comparing function calling (85.7%) against code generation (97.1%) on a 70-task GeoJSON benchmark.
- **GeoAgentic-RAG** (Liang et al. 2026): four-agent hierarchy extending RAG with spatial-semantic retrieval and inter-agent message passing.
- **GeoQA Portal** (Feng et al. 2025): analyzer-explainer-visualizer pipeline with semantic search for non-expert access to geospatial data, achieving 90--96% accuracy.

**Shared pattern.** Agents are differentiated by functional role (planner, coder, retriever, visualizer), not by spatial position. Communication follows task dependencies in a fixed pipeline. Coordination is orchestrated top-down.

### 1.3 Domain-Specific LLM Fine-Tuning for GIS

A parallel thread fine-tunes smaller models for GIS tool mastery. GeoTool-GPT (Wei et al. 2024) fine-tunes LLaMA-2-7B on curated instruction datasets, approaching GPT-4 accuracy (66% vs. 75.3%) at a fraction of the size. GTChain (Zhang et al. 2025) trains a 7B model in a simulated environment with self-instruct-generated data, beating GPT-4 by 32.5% on tool-use chains. These results suggest that domain-specialized compact models can substitute for large general-purpose LLMs on narrowly defined GIS tasks.

### 1.4 Spatial Reasoning Benchmarks

Four benchmarks collectively quantify LLM spatial reasoning ability — and its limits:

| Benchmark | Venue | Scope | Key finding |
|---|---|---|---|
| GeoLLM (Manvi et al. 2024) | ICLR 2024 | Geospatial prediction from coordinates | LLMs cannot interpret raw coordinates; enriched OSM prompts improve predictions 3.3x |
| MapEval (Dihan et al. 2025) | ICML 2025 | 700 map questions, 180 cities, 30 FMs | No model exceeds 67%; all lag 20%+ behind humans |
| Spatial cognition (Yang et al. 2025) | IJGIS 2025 | 105 questions, landmark/route/survey | GPT-4-turbo <25%; Hybrid Mind (LLM + GIS algorithms) reaches 70.5% |
| GeoAnalystBench (Zhang, Gao et al. 2025) | TGIS 2025 | 50 Python-based geoprocessing tasks | Spatial reasoning is hardest category for all models |

The convergent finding is that LLMs are unreliable spatial reasoners across models, tasks, and modalities. The failures are not closing with scale: GPT-4 improves tool selection and syntax over GPT-3.5, but spatial reasoning accuracy plateaus.

### 1.5 DGGS Meets Multi-Agent Systems

Two recent systems connect Discrete Global Grid Systems with multi-agent architectures. Wu et al. (2025) integrate an H3 DGGS pipeline with a multi-agent framework where a coordinator decomposes queries and task agents operate at adaptively selected resolutions. Li and Liang (2026, under review) use rHEALPix DGGS to index methane emission inventories and query them through seven LLM agents, achieving 96.3% success — with spatial joins reduced to prefix operations on hierarchical cell identifiers.

### 1.6 Decentralized Environmental Monitoring

On the non-LLM side, Alarcon Granadeno et al. (2025) demonstrate cooperative multi-agent reinforcement learning for airborne plume tracing, where a UAV swarm localizes emission sources through decentralized policies in partially observable environments. Ding et al. (2024) propose SeqComm, a multi-level communication scheme where agents negotiate decision priority dynamically. Both achieve decentralized coordination but operate in flat continuous space with no geographic hierarchy.

---

## 2. Research Gaps

### 2.1 Agents Reason *About* Space but Never *Through* Space

Every multi-agent GeoAI system differentiates agents by functional role: one agent plans, another retrieves data, another generates code, another visualizes. The spatial data they operate on is passive — retrieved, processed, and returned. No system has agents that are spatially situated, where an agent's identity, neighborhood, and communication partners are determined by its geographic position.

**Why this matters.** Many real geospatial problems are inherently spatial-local: air quality anomalies propagate between neighboring regions; urban heat islands form through interactions between adjacent land parcels; wildfire fronts advance cell by cell. These phenomena naturally decompose by geographic proximity, not by workflow stage. A spatially grounded agent architecture — where agents *are* spatial units and communicate with geographic neighbors — would match the problem structure of these tasks directly, potentially enabling spatial pattern detection (clustering, diffusion, front tracking) that emerges from local interactions rather than being designed top-down.

### 2.2 Hierarchical Grids Are Used for Indexing, Not for Reasoning

Both Wu et al. (2025) and Li and Liang (2026) demonstrate that DGGS hierarchies make spatial operations efficient: parent-child relationships become prefix operations, neighbor queries become table lookups, and multi-resolution data unifies under a single schema. But in both systems, the hierarchy serves data organization — cells store data and get queried. The agents that reason (coordinator, analyst, reasoner) exist outside the grid.

**Why this matters.** The DGGS hierarchy encodes information that could directly support multi-resolution reasoning. A parent cell spatially contains its children. If children show correlated anomalies, the parent is the natural aggregation point. If a coarse cell shows an outlier, its children are the natural place to look for finer-grained explanation. This containment-driven reasoning is implicit in the grid topology but has never been exploited as a reasoning mechanism. Doing so would enable scale-adaptive analysis where coarse summaries guide fine-grained investigation — without a central planner deciding which resolution to examine.

### 2.3 The "Hybrid Mind" Insight Has Not Been Architecturalized

Yang et al. (2025) showed that pairing an LLM with deterministic GIS algorithms (their "Hybrid Mind" approach) nearly triples spatial reasoning accuracy — from <25% to 70.5%. MapEval confirmed the pattern: tool-augmented agents outperform base LLMs by 16--21%. Mai et al. (2024) articulated the root cause: LLMs violate Tobler's First Law of Geography, treating coordinates as token sequences rather than spatial references.

Despite this, the compensatory strategies in the literature remain piecemeal. GeoGPT adds "strong-tone prompts." GIS Copilot adds RAG over tool documentation. GeoCogent adds a CRS inference module. LLM-Find adds source-specific handbooks. Each patches a specific failure mode (wrong tool, wrong projection, wrong API call) without addressing the underlying architectural issue: the LLM is asked to reason about spatial structure that it cannot represent.

**Why this matters.** The field needs a principled framework for partitioning spatial intelligence between LLM capabilities (natural language interpretation, workflow planning, domain knowledge) and structural spatial computation (adjacency, containment, proximity, spatial autocorrelation). The current ad-hoc approach means each new system rediscovers the same failure modes and invents its own compensatory patches. A systematic division of labor — where certain reasoning tasks are provably handled by spatial structure rather than LLM inference — would clarify what LLMs should and should not be asked to do in geospatial contexts.

### 2.4 Communication Overhead Is an Unresolved Scaling Constraint

Lee et al. (2025) found that naive multi-agent communication can be catastrophic: the Magentic-One baseline consumed 210,000 tokens to achieve 34% accuracy, while GeoLLM-Squad used 78,000 tokens for 60%. GeoColab's strict sequential pipeline avoids communication overhead but prevents parallelism and feedback loops. No multi-agent geospatial system has addressed how to scale agent communication efficiently as the number of agents or spatial extent grows.

**Why this matters.** If multi-agent geospatial systems are to handle large spatial extents or high-resolution grids, communication architecture becomes a first-order design concern. Unstructured message passing between agents does not scale. The open question is whether spatial topology can serve as a natural communication constraint — limiting who talks to whom based on geographic proximity — and whether this reduces overhead without sacrificing analytical quality.

### 2.5 No Proactive Spatial Monitoring Exists in LLM-Based Systems

Every LLM-powered geospatial system in the literature is reactive: a user poses a question, the system answers. There is no system that continuously monitors spatial phenomena and initiates analysis when conditions change. The closest work is MARL-based plume tracing (Alarcon Granadeno et al. 2025), which is proactive but operates outside the GIS data ecosystem — in flat continuous space with no GIS data model, no standard spatial references, and no multi-resolution hierarchy.

**Why this matters.** Environmental monitoring, disaster early warning, and infrastructure surveillance all require proactive spatial intelligence: the system should detect an emerging anomaly, not wait for someone to ask about it. Bridging the gap between LLM-based GIS agents (which have rich data access and analytical capabilities but are passive) and MARL-based swarms (which are proactive but spatially unstructured) would open a class of applications that neither approach currently serves.

### 2.6 Evaluation Infrastructure Does Not Cover Multi-Resolution or Temporal Reasoning

All four spatial reasoning benchmarks (GeoLLM, MapEval, Yang et al., GeoAnalystBench) evaluate single-turn, single-scale, reactive reasoning: the system is given a question at one geographic resolution and produces an answer. No benchmark tests whether a system can reason across scales (e.g., detecting a regional trend from county-level data), track phenomena over time (e.g., monitoring a spreading plume), or initiate analysis proactively.

**Why this matters.** The benchmarks shape what gets built. If evaluation only covers "answer a spatial question at a fixed scale," that is what systems will optimize for. Multi-resolution reasoning (zooming in from regional patterns to local causes), temporal tracking (following a spreading anomaly), and proactive detection (alerting without being asked) are critical capabilities for operational geospatial intelligence — but there is no way to measure progress on them. Building evaluation infrastructure for these capabilities would redirect research effort toward the problems that matter most for real-world deployment.

### 2.7 Fine-Tuned Compact Models Have Not Been Tested as Spatial Reasoners

GeoTool-GPT and GTChain demonstrate that 7B models fine-tuned on domain-specific data can match or exceed GPT-4 on GIS tool selection and sequencing. But both benchmarks evaluate tool-use competence, not spatial reasoning. No study has fine-tuned a compact model specifically for spatial pattern recognition (detecting clusters, identifying anomalies, reasoning about containment or adjacency) and evaluated whether the spatial reasoning ceiling observed for large models (MapEval's 67%, Yang et al.'s 25%) also applies to domain-specialized small models.

**Why this matters.** If compact models can be trained to handle specific spatial reasoning tasks (e.g., interpreting neighbor states, classifying spatial patterns, deciding activation thresholds), they could serve as lightweight reasoning engines embedded within larger spatial systems — operating at individual grid cells or sensors. This would make architectures that require many concurrent reasoning agents computationally feasible.

### 2.8 No Bridge Between Agent-Based Modeling Theory and LLM-Based GeoAI Practice

Manson et al. (2020) comprehensively surveyed agent-based modeling methodology in geography, identifying persistent challenges: multi-scale interaction is "theoretically required and practically necessary" yet underimplemented; behavior definition is the central bottleneck; event-driven temporal models are more efficient but rarely used. The ABM community also contributed GAMA (Taillandier et al. 2019), a mature platform supporting GIS-native, large-scale decentralized agent simulations — and GOAM (Song et al. 2019), which pairs grid objects with behavioral agents in a formal bidirectional model.

Meanwhile, the LLM-based GeoAI community has built a parallel world of agent systems that shares almost none of this accumulated knowledge. The ABM literature's minimum agent definition (autonomy, interaction, awareness, decision-making — Manson et al. 2020), its spatial representation debates (absolute vs. relative space), and its hard-won lessons about scale, time, and emergence are absent from GeoAI agent papers. Conversely, the ABM community has not explored LLMs as a mechanism for agent behavior specification.

**Why this matters.** The two communities address complementary halves of the same problem. ABM has mature spatial-agent theory but relies on hand-authored behavioral rules. GeoAI has flexible natural-language behavior specification (via LLMs) but no theory of agent grounding, emergence, or spatial interaction. A synthesis would address both communities' open problems: ABM gets flexible behavior specification; GeoAI gets principled spatial agent design. Without this synthesis, the GeoAI community risks re-learning lessons about scale, emergence, and agent design that ABM researchers documented decades ago.

---

## 3. Summary

The geospatial AI agent field is advancing rapidly along two axes: single-agent tool mastery (RAG, fine-tuning, prompting strategies) and multi-agent workflow decomposition (role-specialized pipelines). Benchmark infrastructure has matured enough to quantify a persistent spatial reasoning gap that current approaches patch but do not resolve.

The gaps identified above point to several directions that remain largely unexplored:

1. **Spatially grounded agents** whose identity and communication are determined by geographic position, not workflow role
2. **Grid hierarchy as a reasoning mechanism**, exploiting containment and adjacency for multi-resolution analysis rather than just data indexing
3. **A principled LLM--spatial computation partition**, moving beyond ad-hoc compensatory patches to a systematic division of inferential and structural reasoning
4. **Topology-constrained communication** as a solution to multi-agent scaling
5. **Proactive spatial intelligence** that bridges LLM-based GIS and MARL-based monitoring
6. **Evaluation infrastructure for multi-resolution, temporal, and proactive spatial reasoning**
7. **Compact spatial reasoning models** tested on spatial pattern recognition, not just tool selection
8. **Cross-pollination between geographic ABM theory and LLM-based GeoAI practice**

These gaps are interconnected. Spatially grounded agents naturally communicate through spatial topology, which constrains communication overhead. Grid hierarchy enables multi-resolution reasoning that current benchmarks cannot evaluate. Compact spatial reasoners make spatially grounded architectures computationally feasible. And ABM theory provides the design principles that spatially grounded LLM agents currently lack.

---

## References

- Akinboyewa, T., Li, Z., Ning, H., and Lessani, M.N. (2025). GIS Copilot: Towards an autonomous GIS agent for spatial analysis. *International Journal of Digital Earth*, 18(1), 2497489.
- Alarcon Granadeno, P.A. et al. (2025). Multi-source plume tracing via multi-agent reinforcement learning. arXiv:2505.08825.
- Bao, R., Yang, C., Yu, D., Tang, Z., Mai, G., and Zhao, L. (2026). Spatial-Agent: Agentic geo-spatial reasoning with scientific core concepts. arXiv:2601.16965.
- Dihan, M.L. et al. (2025). MapEval: A map-based evaluation of geo-spatial reasoning in foundation models. *ICML 2025*, PMLR 267:13774--13813.
- Ding, Z. et al. (2024). Multi-agent coordination via multi-level communication. *NeurIPS 2024*.
- Feng, Y., Zhang, P., Xiao, G., Ding, L., and Meng, L. (2025). Towards a barrier-free GeoQA portal. *International Journal of Applied Earth Observation and Geoinformation*, 144, 104825.
- Hojati, M. and Robertson, C. (2020). Integrating cellular automata and discrete global grid systems. *AGILE: GIScience Series*, 1, 6.
- Hou, S. et al. (2025). GeoCogent: An LLM-based agent for geospatial code generation. *International Journal of Geographical Information Science*, 40(4), 1073--1106.
- Lee, C. et al. (2025). GeoLLM-Squad: Multi-agent geospatial copilots for remote sensing workflows. *IEEE IGARSS 2025*.
- Li, M. and Liang, S.H.L. (2026). DGGS-Q: Multi-agent natural language querying over rHEALPix methane data. *International Journal of Geographical Information Science* (under review).
- Li, Z. and Ning, H. (2023). Autonomous GIS: The next-generation AI-powered GIS. *International Journal of Digital Earth*, 16(2), 4668--4686.
- Li, Z. et al. (2025). GIScience in the era of artificial intelligence: A research agenda towards autonomous GIS. *Annals of GIS*, 31(4).
- Liang, C. et al. (2026). GeoAgentic-RAG: Multi-agent spatial-semantic RAG for geospatial QA. *International Journal of Applied Earth Observation and Geoinformation*, 147, 105195.
- Luo, Q. et al. (2026). GeoJSON Agents: Function calling vs. code generation in multi-agent geospatial analysis. *Big Earth Data*.
- Mai, G. et al. (2024). Foundation models for geospatial artificial intelligence. *ACM Transactions on Spatial Algorithms and Systems*, 10(2).
- Manson, S. et al. (2020). Methodological issues of spatial agent-based models. *JASSS*, 23(1), 3.
- Manvi, R. et al. (2024). GeoLLM: Extracting geospatial knowledge from large language models. *ICLR 2024*.
- Ning, H., Li, Z., Akinboyewa, T., and Lessani, M.N. (2025). LLM-Find: Autonomous geospatial data retrieval. *International Journal of Digital Earth*, 18(1), 2458688.
- Song, Y., Niu, L., and Li, Y. (2019). Individual behavior simulation based on grid object and agent model. *ISPRS International Journal of Geo-Information*, 8(9), 388.
- Taillandier, P. et al. (2019). Building, composing and experimenting complex spatial models with the GAMA platform. *GeoInformatica*, 23(2), 299--322.
- Wei, C. et al. (2024). GeoTool-GPT: A trainable method for facilitating LLMs to master GIS tools. *International Journal of Geographical Information Science*, 39(4), 707--731.
- Wu, C.-C. et al. (2025). Democratizing multi-granularity spatio-temporal intelligence with multi-agent systems. *ACM SIGSPATIAL Workshop GeoGenAgent '25*.
- Wu, H. et al. (2025). GeoColab: Multi-agent collaborative framework for geospatial code generation. *International Journal of Digital Earth*, 18, 2569405.
- Yang, A. et al. (2025). Evaluating and enhancing spatial cognition abilities of large language models. *International Journal of Geographical Information Science*, 39(9).
- Zhang, Q., Gao, S. et al. (2025). GeoAnalystBench: Assessing LLMs for spatial analysis workflow and code generation. *Transactions in GIS*, 29(7), e70135.
- Zhang, Y. et al. (2024). GeoGPT: An assistant for understanding and processing geospatial tasks. *International Journal of Applied Earth Observation and Geoinformation*, 131, 103976.
- Zhang, Y. et al. (2025). GTChain: Geospatial LLM trained with a simulated environment for generating tool-use chains. *International Journal of Applied Earth Observation and Geoinformation*, 136, 104312.
