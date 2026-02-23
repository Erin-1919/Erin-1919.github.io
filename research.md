---
title: "Research"
permalink: "/Research/"
layout: page
---

<style>
.tab-buttons {
  margin-bottom: 20px;
}
.tab-buttons button {
  padding: 10px 20px;
  margin-right: 5px;
  border: none;
  background-color: #f0f0f0;
  cursor: pointer;
}
.tab-buttons button.active {
  background-color: #007bff;
  color: white;
}
.tab-content {
  display: none;
}
.tab-content.active {
  display: block;
}
</style>

<div class="tab-buttons">
  <button class="tab-button active" onclick="showTab('publications')">Publications</button>
  <button class="tab-button" onclick="showTab('presentations')">Presentations</button>
  <button class="tab-button" onclick="showTab('talks')">Invited Talks</button>
  <button class="tab-button" onclick="showTab('thesis')">Thesis</button>
</div>

<div id="publications" class="tab-content active">
{% capture publications_content %}

## Peer-reviewed Publications
### 2026
**Li, M.E.**; Liang, S.H.L. Enabling a Digital Earth for Methane Emissions Management with Equal-Area Discrete Global Grids. International Journal of Digital Earth. 19(1), 2607210. [**DOI**](https://doi.org/10.1080/17538947.2025.2607210) / [**PDF**](https://Erin-1919.github.io/assets/pdf/2026%20Li%20and%20Liang.pdf)
<details>
  <summary>Abstract</summary>
We develop a spatially explicit methane inventory for Alberta’s upstream oil and gas sector using the rHEALPix Discrete Global Grid System. The objective is to demonstrate an equal-area, hierarchy-aware framework that assigns facility-reported emissions to native locations and supports multi-scale analysis and reporting. We compile monthly facility activity from Petrinex for 2020 to 2023, geolocate facilities using the Oil and Gas Infrastructure Mapping database, calculate methane emissions from venting, fuel use, and flaring using province-standard factors, and bin results to rHEALPix cells before exact aggregation to coarser levels. Our analysis revealed persistent high-emission hotspots, with 5% of grid cells accounting for 34% of total annual methane emissions. The equal-area lattice enables fair intensity comparisons across latitude, stable hotspot tracking over time, and mass-conserving aggregation that maintains consistent totals across resolutions. Practical implications include a standard spatial fabric that integrates facility reports, satellites, and ground sensors, provides persistent cell buckets for facility and asset management, enables accurate intensity comparisons across space and time with quantitative spatial resolution, preserves spatial integrity in visualization, supports consistent mass conserving aggregation at any scale with multiple granularities for analysis and reporting, allows precise hotspot tracking and trend monitoring, and informs targeted monitoring and survey design.
</details>

**Li, M.E.**; Liang, S.H.L. Natural Language to DGGS-Aware Methane Insights with a Multi-LLM-Agent Framework. Proceedings in Spatial Knowledge and Information Canada 2026. [**DOI**]() / [**PDF**]()
<details>
  <summary>Abstract</summary>
Fragmented spatial data and inconsistent semantics hinder environmental analytics and confound large language models. We present a Discrete Global Grid System powered framework that harmonizes gridded methane inventories and enables explainable, traceable natural language analytics. Demonstrating the methane use case, we standardize spatial and semantic references using DGGS as a global index, then allow the interaction with a modular multi-agent system. Agents parse intent, resolve locations to DGGS cells, and generate validated SQL that powers summaries and maps with cell-level citations. The result is fast, reproducible methane analysis with clear provenance.
</details>

### 2025
Liao, C.; Engwirda, D.; Cooper, M.; **Li, M.**; Fang, Y. Discrete Global Grid System-based flow routing datasets in the Amazon and Yukon basins. Earth System Science Data. 17(5), 2035–2062. [**DOI**](https://doi.org/10.5194/essd-17-2035-2025)

<details>
  <summary>Abstract</summary>
Discrete global grid systems (DGGS) are emerging spatial data structures widely used to organize geospatial datasets across scales. While DGGS have found applications in various scientific disciplines, including atmospheric science and ecology, their integration into physically based hydrological models and Earth system models (ESMs) has been hindered by the lack of flow routing datasets based on DGGS. In response to this gap, this study pioneers the development of new flow routing datasets using icosahedral Snyder equal-area (ISEA) DGGS and a novel mesh-independent flow direction model. We present flow routing datasets for two large basins, the tropical Amazon River basin and the Arctic Yukon River basin. These datasets (1) facilitate the adoption of DGGS for hydrological models and (2) provide flow routing inputs for evaluation of DGGS-based flow routing in the Amazon and Yukon river basins. The data are available at https://doi.org/10.5281/zenodo.8377765 (Liao, 2023).
</details>

### 2024
**Li, M.**; Tousignant, C.; Chaudhuri, C.; Chabbouh, A. Utilizing serverless framework for dynamic visualization and operations in geospatial applications. International Journal of Digital Earth. 17(1), 2392835. [**DOI**](https://doi.org/10.1080/17538947.2024.2392835) / [**PDF**](https://Erin-1919.github.io/assets/pdf/2024%20Li%20et%20al.pdf)

<details>
  <summary>Abstract</summary>
While substantial efforts have been invested in the development of Discrete Global Grid Systems (DGGS) spatial operations and their potential applications in the geospatial domain, it has become evident that there is a demand for an efficient and scalable system to handle the visualization of large-scale DGGS data. This study demonstrated the potential of DGGS in conjunction with the serverless framework for dynamic visualization at various resolutions, which is based on data storage and effective querying using PostgreSQL integrated into Amazon Aurora Serverless. The use of Amazon Web Services (AWS) Lambda for on-the-fly generation of hexagon geometries significantly reduced the storage requirements and improved the speed of the visualization process. In addition, we implemented on-the-fly spatial operations including point binning, thresholding, aggregation, and neighborhood operations in the DGGS, highlighting the capabilities of DGGS in vector and raster processing. The proposed system has shown promising results in terms of efficiency, scalability, and adaptability, making it a viable solution for large-scale geospatial data processing and visualization. Case studies using flood risk data and terrain data further illustrate the system’s practical applicability in on-the-fly spatial operations and rapid visualization.
</details>

Liu, J.; Li, J.; Qiao, L.; **Li, M.**; Stefanakis, E.; Zhao, X.; Huang, Q.; Wang, H.; Zhang, C. QuadGridSIM: A quadrilateral grid-based method for high-performance and robust trajectory similarity analysis. Transactions in GIS. 00, 1–25. [**DOI**](https://doi.org/10.1111/tgis.13126) / [**PDF**](https://Erin-1919.github.io/assets/pdf/2024%20Liu%20et%20al.pdf)

<details>
  <summary>Abstract</summary>
Measuring trajectory similarity is a fundamental algorithm in trajectory data mining, playing a key role in trajectory clustering, pattern mining, and classification, for instance. However, existing trajectory similarity measures based on vector representation have challenges in achieving both fast and accurate similarity measurements. On one hand, most existing methods have a high computational complexity of O ( n × m ), resulting in low efficiency. On the other hand, many of them are sensitive to trajectory sampling rates and lack of accuracy. This article proposes QuadGridSIM, a quadrilateral grid‐based method for trajectory similarity analysis, which enables high‐performance trajectory similarity measure without the cost of low effectiveness. Specifically, we first realize the multiscale coding representation of trajectory data based on quadrilateral discrete grids. Then, a novel trajectory similarity measure is defined to reduce the computational complexity of O ( n ). Several effectiveness properties of QuadGridSIM are further optimized, including the spatial overlap, directionality, symmetry, and robustness to sampling rate variations. Experimental results based on real‐world and simulated taxi trajectory data indicate that QuadGridSIM outperforms most of the other tested algorithms developed previously in terms of effectiveness, particularly in its robustness regarding trajectory sampling rates. Furthermore, QuadGridSIM exhibits superior performance and is approximately one order of magnitude faster than previous methods in the literature. QuadGridSIM provides a solution to the low‐efficiency problem of massive trajectory similarity analysis and can be applied in many application scenarios, such as route recommendation and suspect detection.
</details>

### 2022
**Li, M.**; McGrath, H.; Stefanakis, E. Multi-scale Flood Mapping under Climate Change Scenarios in Hexagonal Discrete Global Grids. ISPRS International Journal of Geo-Information. 11(12), 627. [**DOI**](https://doi.org/10.3390/ijgi11120627) / [**PDF**](https://Erin-1919.github.io/assets/pdf/2022d%20Li%20et%20al.pdf)

<details>
  <summary>Abstract</summary>
Among the most prevalent natural hazards, flooding has been threatening human lives and properties. Robust flood simulation is required for effective response and prevention. Machine learning is widely used in flood modeling due to its high performance and scalability. Nonetheless, data pre-processing of heterogeneous sources can be cumbersome, and traditional data processing and modeling have been limited to a single resolution. This study employed an Icosahedral Snyder Equal Area Aperture 3 Hexagonal Discrete Global Grid System (ISEA3H DGGS) as a scalable, standard spatial framework for computation, integration, and analysis of multi-source geospatial data. We managed to incorporate external machine learning algorithms with a DGGS-based data framework, and project future flood risks under multiple climate change scenarios for southern New Brunswick, Canada. A total of 32 explanatory factors including topographical, hydrological, geomorphic, meteorological, and anthropogenic were investigated. Results showed that low elevation and proximity to permanent waterbodies were primary factors of flooding events, and rising spring temperatures can increase flood risk. Flooding extent was predicted to occupy 135–203% of the 2019 flood area, one of the most recent major flooding events, by the year 2100. Our results assisted in understanding the potential impact of climate change on flood risk, and indicated the feasibility of DGGS as the standard data fabric for heterogeneous data integration and incorporated in multi-scale data mining.
</details>

**Li, M.**; McGrath, H.; Stefanakis, E. Multi-resolution topographic analysis in hexagonal Discrete Global Grid Systems. International Journal of Applied Earth Observation and Geoinformation. 113, 102985. [**DOI**](https://doi.org/10.1016/j.jag.2022.102985) / [**PDF**](https://Erin-1919.github.io/assets/pdf/2022c%20Li%20et%20al.pdf)

<details>
  <summary>Abstract</summary>
Discrete Global Grid Systems (DGGS) have been increasingly adopted as a standard framework for multi-source geospatial data. Previous research largely studied the mathematical foundation of discrete global grids, developed open-source libraries, and explored their application as data integration platforms. This study investigated the multi-resolution terrain analysis in a pure hexagonal DGGS environment, including descriptive statistics, topographic parameters, and topographic indices. Experiments across multiple grid resolutions were carried out in three study areas with different terrain roughness in Alberta, Canada. Five algorithms were proposed to calculate both the slope gradient and terrain aspect. A cell-based pair-wise comparison showed a strong positive correlation between the gradient values as calculated from five algorithms. The grid resolutions as well as the terrain roughness had a clear effect on the computed slope gradient and topographic indices. This research aims to enhance the analytical functionality of hexagonal DGGS to better support decision-making in real world problems.
</details>

**Li, M.**; McGrath, H.; Stefanakis, E. Geovisualization of Hydrological Flow in Hexagonal Grid Systems. Geographies. 2(2), 227–244. [**DOI**](https://doi.org/10.3390/geographies2020016) / [**PDF**](https://Erin-1919.github.io/assets/pdf/2022a%20Li%20et%20al.pdf)

<details>
  <summary>Abstract</summary>
Recent research has extended conventional hydrological algorithms into a hexagonal grid and noted that hydrological modeling on a hexagonal mesh grid outperformed that on a rectangular grid. Among the hydrological products, flow routing grids are the base of many other hydrological simulations, such as flow accumulation, watershed delineation, and stream networks. However, most of the previous research adopted the D6 algorithm, which is analogous to the D8 algorithm over a rectangular grid, to produce flow routing. This paper explored another four methods regarding generating flow directions in a hexagonal grid, based on four algorithms of slope aspect computation. We also developed and visualized hexagonal-grid-based hydrological operations, including flow accumulation, watershed delineation, and hydrological indices computation. Experiments were carried out across multiple grid resolutions with various terrain roughness. The results showed that flow direction can vary among different approaches, and the impact of such variation can propagate to flow accumulation, watershed delineation, and hydrological indices production, which was reflected by the cell-wise comparison and visualization. This research is practical for hydrological analysis in hexagonal, hierarchical grids, such as Discrete Global Grid Systems, and the developed operations can be used in flood modeling in the real world. 
</details>

### 2021
**Li, M.**; McGrath, H.; Stefanakis, E. Integration of Heterogeneous Terrain Data into Discrete Global Grid Systems. Cartography and Geographic Information Science. 48(6), 546-564. [**DOI**](https://doi.org/10.1080/15230406.2021.1966648) / [**PDF**](https://Erin-1919.github.io/assets/pdf/2021%20Li%20et%20al.pdf)

<details>
  <summary>Abstract</summary>
The Canadian Digital Elevation Model (CDEM) and the High-Resolution Digital Elevation Model (HRDEM) released by Natural Resources Canada are primary terrain data sources in Canada. Due to their different coverage, datums, resolutions, and accuracies, a standardized framework for national elevation data across various scales is required. This study provides new insights into the adoption of Discrete Global Grid Systems (DGGS) to facilitate the integration of multi-source terrain data at various granularities. In particular, the Icosahedral Snyder Equal Area Aperture 3 Hexagonal Grid (ISEA3H) was employed, and quantization, integration, and aggregation were conducted on this framework. To demonstrate the modeling process, an experiment was undertaken for two areas in Ontario, taking advantage of parallel computing which was beneficial from the discreteness of DGGS cells. The accuracy of the modeled elevations was estimated by referring to the ground-surveyed values and was included in the spatially referenced metadata as an indicator of data quality. This research can serve as a guide for future development of a national elevation service, providing consistent, multi-resolution elevations and avoiding complex, duplicated pre-processing at the user’s end. Future investigation into an operational integration platform to support real-world decision-making, as well as the DGGS-powered geospatial datacube, is recommended.
</details>

### 2020
**Li, M.**; Stefanakis, E. Geospatial Operations of Discrete Global Grid Systems – A Comparison with Traditional GIS. Journal of Geovisualization and Spatial Analysis. 4(2), 26. [**DOI**](https://doi.org/10.1007/s41651-020-00066-3) / [**PDF**](https://Erin-1919.github.io/assets/pdf/2020%20Li%20and%20Stefanakis.pdf)

<details>
  <summary>Abstract</summary>
As the foundation of the next-generation Digital Earth, Discrete Global Grid Systems (DGGS) have demonstrated both theoretical and practical development, with a variety of state-of-the-art implementations proposed. These emerging DGGS platforms or libraries support preliminary operations such as quantization, cell-level navigation, and conversion between cell addresses and geographical coordinates, while leaving the other more complicated functions unexplored. This paper discusses the functional operations in a DGGS environment, including the essential operations defined by the Open Geospatial Consortium (OGC) Abstract Specification, and the extended operations potentially supported by DGGS. The extended operations are discussed in comparison to the traditional GIS, from the aspects of database techniques, data pre-processing and manipulation, spatial analysis and data interpretation, data computation, and data visualization. It was found that with the OGC-required operations and pre-processing operations as the baseline of development, some function algorithms can facilitate the algorithm development of other analytical functions. Several future research directions regarding the data modeling uncertainties, extended analytic algorithm development, and database and computation technologies are presented. This paper provides a comparison between DGGS and traditional GIS operations and can serve as a reference for future DGGS operation development.
</details>

**Li, M.**; Stefanakis, E. Geo-feature Modeling Uncertainties in Discrete Global Grids: A Case Study of Downtown Calgary, Canada. Geomatica. 74, 175-195.  [**DOI**](https://doi.org/10.1139/geomat-2020-0011) / [**PDF**](https://Erin-1919.github.io/assets/pdf/2020b%20Li%20and%20Stefanakis.pdf)

<details>
  <summary>Abstract</summary>
The Open Geospatial Consortium has officially adopted discrete global grid systems (DGGS) as a new option for Earth reference standards. Many state-of-the-art DGGS implementations have been developed, revealing the potential for DGGS applications. Before the wide application of DGGS in solving real-world problems, however, the potential uncertainties of modeling on DGGS should be investigated and documented. This study focused on the uncertainties of geo-feature modeling on DGGS, quantitatively measured the point position displacement and line and polygon features’ geometry distortion, and evaluated the validity of topological relationships. Specifically, traffic cameras (points), main streets (lines), and land-cover classes (polygons) of downtown Calgary (AB, Canada) were modeled in various DGGS configurations at multiple resolutions. Results showed that the point displacement and polygon distortion generally reduced when being modeled at a higher resolution. The tessellations with the monotonical convergence characteristic are recommended if cell indices are expected to represent levels of model precision. Line features’ fidelity was affected by grid tessellations, resolution levels, grid orientation relative to the Earth, and the rotated line directions. The degree of the line distortion was not straightforward to forecast. Maintaining the topological validity between spatial objects with various granularities was challenging and needed further algorithm development for DGGS implementations. The study outcomes can serve as useful guidelines in the selection among grid types, refinement ratios, and resolution levels when applying DGGS implementations to urban environments. This paper also pinpoints several research directions that can benefit the quantization and analysis of vector features on DGGS.
</details>

**Li, M.**; Stefanakis, E.; McGrath, H. National Terrain Data Management on Discrete Global Grids in Canada. AutoCarto2020. [**PDF**](https://cartogis.org/docs/autocarto/2020/docs/abstracts/3h%20National%20Terrain%20Data%20Management%20on%20Discrete%20Global%20Grids%20in%20Canada.pdf)

<details>
  <summary>Abstract</summary>
Terrain data can be acquired by various technologies with different data formats, spatial resolutions, datum, projections, and update cycles. In Canada, terrain datasets released by Natural Resources Canada (NRCan) mainly include the Canadian Digital Elevation Model (CDEM) and the High Resolution Digital Elevation Model (HRDEM). Because of their different coverage, datum, resolution, and accuracy, users who work with these two data collections may suffer from time-consuming pre-processing and inconsistent results due to different pre-processing methods. To achieve more effective utilization of multi-source terrain data, an integration solution is highly in need to merge and qualitycontrol the terrain data on a standardized framework (Schumann and Bates, 2018). Discrete Global Grid Systems (DGGS) is a new option for Earth reference standards. A DGGS is a system of hierarchical Discrete Global Grids (DGG) where the DGG at each resolution tessellates the entire Earth’s surface by nearly equal-area cells without any overlaps and assigns a single identifier to each cell (OGC, 2017). DGGS can benefit the heterogeneous data integration, multi-scale analysis, consistent observation at a certain location, accurate analysis taking account of Earth’s curvature, and efficient parallel computation given its discrete nature. For Canadian terrain data users, DGGS provide an opportunity to standardize the data acquisition process via data integration.
</details>

### 2019
**Li, M.**; MacLean, D.A.; Hennigar, C.R.; Ogilvie, J. Previous Year Outbreak Conditions and Spring Climate Predict Spruce Budworm Population Changes in the Following Year. Forest Ecology and Management. 458, 117737. [**DOI**](https://doi.org/10.1016/j.foreco.2019.117737) / [**PDF**](https://Erin-1919.github.io/assets/pdf/2019b%20Li%20et%20al.pdf)

<details>
  <summary>Abstract</summary>
We determined effects of local spruce budworm (Choristoneura fumiferana Clem.; SBW) population level, proximity to sites with high SBW populations, insecticide spray, and environmental variables on SBW populations from 2014 to 2018, the outbreak initiation period in northern New Brunswick, Canada. SBW second instar larvae (L2) per branch data collected at 1100–2000 sample points per year were used to create annual interpolated population rasters. Fishnet sample points extracted from these rasters were overlaid with georeferenced layers of 46 possible predictor variables including forest composition, climate, topography, site quality, and insecticide treatment. Results showed that local SBW population in the previous year, proximity to sites with high SBW populations, and early spring climate were consistently the most important predictors over the 5 study years. Simultaneous autoregressive models were used to address spatial autocorrelation when forecasting the SBW L2 population, and a linear mixed effects model was fit to aggregate data for 2015–2018. The models reduced spatial dependence in the residuals, and explained 68–79% of variance in annual L2 levels and 53% of variance over the 4 years combined. Sensitivity analysis showed that locations with 5–10 more SBW L2 per branch than observed values, or 20–40 km closer to high population sites in the previous year could have up to 24 more L2 in the current year. Cumulative degree days in April helped to estimate the upper and lower bounds of the population. Expansion and retraction of SBW outbreak initiation were mathematically described. Understanding which variables influence SBW outbreak initiation and population level assists in design of small area target-specific insecticide spray applications and helps focus SBW L2 sampling on predicted outbreak hot spots.
</details>

**Li, M.**; MacLean, D.A.; Hennigar, C.R.; Ogilvie, J. Spatial-Temporal Patterns of Spruce Budworm Defoliation within Plots in Québec. Forests. 10, 232. [**DOI**](https://doi.org/10.3390/f10030232) / [**PDF**](https://Erin-1919.github.io/assets/pdf/2019a%20Li%20et%20al.pdf)

<details>
  <summary>Abstract</summary>
We investigated the spatial-temporal patterns of spruce budworm (Choristoneura fumiferana (Clem.); SBW) defoliation within 57 plots over 5 years during the current SBW outbreak in Québec. Although spatial-temporal variability of SBW defoliation has been studied at several scales, the spatial dependence between individual defoliated trees within a plot has not been quantified, and effects of defoliation level of neighboring trees have not been addressed. We used spatial autocorrelation analyses to determine patterns of defoliation of trees (clustered, dispersed, or random) for plots and for individual trees. From 28% to 47% of plots had significantly clustered defoliation during the 5 years. Plots with clustered defoliation generally had higher mean defoliation per plot and higher deviation of defoliation. At the individual-tree-level, we determined ‘hot spot trees’ (highly defoliated trees surrounded by other highly defoliated trees) and ‘cold spot trees’ (lightly defoliated trees surrounded by other lightly defoliated trees) within each plot using local Getis-Ord Gi* analysis. Results revealed that 11 to 27 plots had hot spot trees and 27% to 64% of them had mean defoliation 25%, while plots with 75% to 100% defoliation had either cold spot trees or non-significant spots, which suggested that whether defoliation was high or low enough to be a hot or cold spot depended on the defoliation level of the entire plot. We fitted individual-tree balsam fir defoliation regression models as a function of plot and surrounding tree characteristics (using search radii of 3–5 m). The best model contained plot average balsam fir defoliation and subject tree basal area, and these two variables explained 80% of the variance, which was 2% to 5% higher than the variability explained by the neighboring tree defoliation, over the 3–5 m search radii tested. We concluded that plot-level defoliation and basal area were adequate for modeling individual tree defoliation, and although clustering of defoliation was evident, larger plots were needed to determine the optimum neighborhood radius for predicting defoliation on an individual. Spatial autocorrelation analysis can serve as an objective way to quantify such ecological patterns.
</details>
{% endcapture %}
{{ publications_content | markdownify }}
</div>

<div id="presentations" class="tab-content">
{% capture presentations_content %}

## Conference Presentations
### 2026

**Li, M.E.**; Liang, S.H.L. Natural Language to DGGS-Aware Methane Insights with a Multi-LLM-Agent Framework​. Oral presentation at the  9th Conference on Spatial Knowledge and Information (SKI) Canada, Feb. 2026, Banff, Alberta, Canada. [**Short Paper**]()

### 2025

**Li, M.E.**; Liang, S.H.L. Talking to the Planet: Natural Language x Digital Earth for Disasters​. Oral presentation at the 133rd OGC Member Meeting - Innovation Summit, Oct. 2025, Boulder, U.S.

**Li, M.E.**; Liang, S.H.L. Ask, Retrieve, Analyze: A Multi-Agent DGGS Framework for GenAI Driven Methane Data. Oral presentation at the 133rd OGC Member Meeting - Discrete Global Grid Systems DWG, Oct. 2025, Boulder, U.S.

**Li, M.E.**; Liang, S.H.L. Standardizing Spatial Intelligence for Gridded Methane Inventories: DGGS Meets EmissionML. Oral presentation at the 132nd OGC Member Meeting - EmissionML DWG, Jun. 2025, Online.

**Li, M.E.**; Liang, S.H.L. Beyond the Graticule: Spatially Explicit Methane Inventories Using Discrete Global Grids. Oral presentation at the 132nd OGC Member Meeting - Discrete Global Grid Systems DWG, Jun. 2025, Online.

**Li, M.E.**; Liang, H.L.S. Beyond the Graticule: Spatially Explicit Methane Inventories Using Discrete Global Grids. Oral and poster presentation at CanCH4 Symposium, May 2025, Ottawa, Canada. [**Poster**](https://Erin-1919.github.io/assets/pdf/CanCH4_Poster_May_2025_EL.pdf) / [**Recorded Presentation**](https://youtu.be/_FMQk5I4agQ) / [**Panel Discussion**](https://youtu.be/r7FaFNzNV-o)

### 2024
**Li, M.E.**; Liang, H.L.S. Mapping Methane: A Review of Bottom-up Gridded Inventories. Oral presentation at the 130th OGC Member Meeting - EmissionML DWG ad-hoc, Nov. 2024, Online.

### 2023
**Li, M.**; McGrath, H.; Stefanakis, E. Flood susceptibility analysis on hexagonal grid meshes: a case study in southern New Brunswick, Canada. Poster presentation at GIS in Education and Research Conference, Mar. 2023, Toronto, Canada. [**Poster**](https://Erin-1919.github.io/assets/pdf/ESRI_poster_Li_2022.pdf)

### 2022
**Li, M.**; McGrath, H.; Stefanakis, E. Analytical operations for terrain data modeled in Discrete Global Grid Systems. Oral presentation at Canadian Cartographic Association Conference, May 2022, Online. [**Recorded Presentation**](https://drive.google.com/file/d/1DECGOtfzUCyaSrtsDGUxXjXPVS3JcYSJ/view?usp=sharing)
  
### 2021
**Li, M.**; McGrath, H.; Stefanakis, E. Integration of multi-source terrain data on Discrete Global Grids in Canada. Oral presentation at Canadian Cartographic Association Conference, May 2021, Online. [**Recorded Presentation**](https://drive.google.com/file/d/1I0YnzykCr2wq41E5z4sy4xFBjiChINmA/view?usp=sharing)

### 2020
**Li, M.**; Stefanakis, E.; McGrath, H. National terrain data management on Discrete Global Grids in Canada. Oral presentation at AutoCarto 2020, Oct. 2020, Online. [**PDF**](https://cartogis.org/docs/autocarto/2020/docs/abstracts/3h%20National%20Terrain%20Data%20Management%20on%20Discrete%20Global%20Grids%20in%20Canada.pdf) / [**Recorded Presentation**](https://cartogis.org/docs/autocarto/2020/docs/presentations/3h%20National%20Terrain%20Data%20Management%20on%20Discrete%20Global%20Grids%20in%20Canada.mp4)

### 2018
**Li, M.**; MacLean, D.A.; Hennigar, C.R.; Ogilvie, J. Spatial-tempol patterns of spruce budworm defoliation within measured plots in Québec. Oral presentation at the 9th Bi-Annual Eastern Canada - USA Forest Science Conference, Oct. 2018, Fredericton, Canada.

**Li, M.**; MacLean, D.A. GIS analyses of factors influencing spruce budworm outbreak initiation in northern New Brunswick. Oral presentation at SERG International Workshop, Feb. 2018, Edmonton, Canada.
{% endcapture %}
{{ presentations_content | markdownify }}
</div>

<div id="talks" class="tab-content">
{% capture talks_content %}

## Other Invited Talks
### 2026
Introduction to Discrete Global Grid Systems (DGGS). Guest lecture at ENGO 551 Advanced Spatial Topics. University of Calgary. Jan 2026.

### 2025
Discrete Global Grid Systems (DGGS) and Their Role in Methane Emission Inventories. Presented at the Monthly Lunch and Learn at SensorUp Inc., May 2025.

### 2022
Flood Susceptibility Modeling in Discrete Global Grids under Climate Change Scenarios. Presented at the Natural Resources Canada, Oct. 2022.

Geospatial Data Analysis in Discrete Global Grid Systems – Progress and Perspectives. Presented at the China Agricultural University, May 2022.  

Quantization, Analysis, and Application of Terrain Data Modeled in Discrete Global Grid Systems. Presented at the International Society for Photogrammetry and Remote Sensing Work Group IV/7 (Geo-Data Management) Webinar, Jan. 2022. [**Recorded Presentation**](https://www.youtube.com/watch?v=FWGl4lSrIyA)

### 2021
Integration Platform for Canadian Terrain Data: A DGGS Perspective. Presented at the Natural Resources Canada, Apr. 2021.
{% endcapture %}
{{ talks_content | markdownify }}
</div>

<div id="thesis" class="tab-content">
{% capture thesis_content %}

## Thesis
### 2023 
### Ph.D. Dissertation
Hexagonal Discrete Global Grid Systems in Topographical and Hydrological Modeling. [**URL**](http://hdl.handle.net/1880/115923)

<details>
  <summary>Abstract</summary>
Geographic Information Systems (GIS) have dominated geospatial analysis since the 1960s, where spatial phenomena were normally represented by individual thematic layers at a specific resolution, and commonly projected to a two-dimensional Cartesian coordinate system for analysis. Discrete Global Grid Systems (DGGS), as a “congruent geography”, hierarchically partition the Earth’s surface into nearly uniform cells at various resolutions to provide great opportunities for innovation of legacy GIS. In the past few decades, the development of DGGS focused on fundamental implementations, such as polyhedral projections, indexing mechanisms, and generation of hierarchical grids, while limited efforts were given to the applicability studies in real-world scenarios. This dissertation aimed to bridge the gap between the existing DGGS implementations and DGGS-driven decision-making in the real world, and specifically, demonstrate the applicability of hexagonal DGGS in the domain of topographical and hydrological modeling. To achieve the above goal, this dissertation first reviewed the functional operations in a DGGS environment and compared them to those in the traditional GIS. This dissertation then focused on the terrain data integration, management, and analysis in the Icosahedral Snyder Equal Area Aperture 3 Hexagonal Grid (ISEA3H) DGGS. Specifically, the integration process, including quantization and aggregation, of multi-source terrain data at various granularities was demonstrated. Various topographical and hydrological functions, including slope and aspect, flow direction, flow accumulation, etc., were developed and experimented with various terrain types at different resolutions. Finally, external machine learning algorithms were incorporated into the DGGS and used to predict future flood risks under multiple climate change scenarios. This dissertation promotes the adoption of DGGS in real-world decision-making, particularly in topographical and hydrological modeling. The proposed methodology for heterogenous data integration can facilitate the development of a national elevation data service in the future. The developed spatial operations can enhance the analytical functionality of hexagonal DGGS. The application in flood mapping indicated the feasibility of DGGS as the standard data fabric for multi-source data integration and multi-scale data mining.
</details>
  
### 2019 
### M.Sc. Thesis
Spatial patterns and factors influencing spruce budworm infestation in Eastern Canada forests. [**URL**](https://unbscholar.lib.unb.ca/handle/1882/14562)

<details>
  <summary>Abstract</summary>
A spruce budworm (Choristoneura fumiferana Clem.; SBW) outbreak in Québec spread southward into New Brunswick in 2014. This thesis used spatial analyses of 5 years of SBW population data in northern New Brunswick and tree defoliation data in Québec to examine spatial patterns and factors influencing SBW infestation. Local previous-year SBW population level, proximity to outbreak hot-spots, and April degree-days were important in predicting SBW population levels in New Brunswick, although relationships were inconsistent across years. Models incorporating spatial stuctures [sic] explained 68–79% of the annual variance, and performed better than non-spatial models. A combined-year model with R [squared] = 0.53 consistently underestimated upcoming-year populations. Defoliation patterns quantified in 57 plots in Québec were clustered in 28-47% of cases, which had higher plot-level defoliation and higher deviations. Plot-level defoliation and basal area explained 80% of the variance in individual-tree-defoliation. The thesis contributed to efficient sampling allocation and insecticide treatment targeting infestation.
</details>
{% endcapture %}
{{ thesis_content | markdownify }}
</div>

<script>
function showTab(tabId) {
  // Hide all content sections
  document.querySelectorAll('.tab-content').forEach(content => {
    content.style.display = 'none';
  });
  
  // Remove active class from all buttons
  document.querySelectorAll('.tab-button').forEach(button => {
    button.classList.remove('active');
  });
  
  // Show selected content and activate button
  document.getElementById(tabId).style.display = 'block';
  document.querySelector(`button[onclick="showTab('${tabId}')"]`).classList.add('active');
}

// Initialize tab display to show publications by default
document.addEventListener('DOMContentLoaded', function() {
  showTab('publications');
});
</script>
