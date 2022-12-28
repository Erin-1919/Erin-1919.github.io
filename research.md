---
title: "Research"
permalink: "/Research/"
layout: page
---

## Peer-reviewed Publications
### 2022
**Li, M.**; McGrath, H.; Stefanakis, E. Multi-scale Flood Mapping under Climate Change Scenarios in Hexagonal Discrete Global Grids. ISPRS International Journal of Geo-Information 11(12), 627. [**DOI**](https://doi.org/10.3390/ijgi11120627) / [**PDF**](https://Erin-1919.github.io/assets/pdf/2022d%20Li%20et%20al.pdf)

<details>
  <summary>Abstract</summary>
Among the most prevalent natural hazards, flooding has been threatening human lives and properties. Robust flood simulation is required for effective response and prevention. Machine learning is widely used in flood modeling due to its high performance and scalability. Nonetheless, data pre-processing of heterogeneous sources can be cumbersome, and traditional data processing and modeling have been limited to a single resolution. This study employed an Icosahedral Snyder Equal Area Aperture 3 Hexagonal Discrete Global Grid System (ISEA3H DGGS) as a scalable, standard spatial framework for computation, integration, and analysis of multi-source geospatial data. We managed to incorporate external machine learning algorithms with a DGGS-based data framework, and project future flood risks under multiple climate change scenarios for southern New Brunswick, Canada. A total of 32 explanatory factors including topographical, hydrological, geomorphic, meteorological, and anthropogenic were investigated. Results showed that low elevation and proximity to permanent waterbodies were primary factors of flooding events, and rising spring temperatures can increase flood risk. Flooding extent was predicted to occupy 135–203% of the 2019 flood area, one of the most recent major flooding events, by the year 2100. Our results assisted in understanding the potential impact of climate change on flood risk, and indicated the feasibility of DGGS as the standard data fabric for heterogeneous data integration and incorporated in multi-scale data mining.
</details>

**Li, M.**; McGrath, H.; Stefanakis, E. Multi-resolution topographic analysis in hexagonal Discrete Global Grid Systems. International Journal of Applied Earth Observation and Geoinformation 113, 102985. [**DOI**](https://doi.org/10.1016/j.jag.2022.102985) / [**PDF**](https://Erin-1919.github.io/assets/pdf/2022c%20Li%20et%20al.pdf)

<details>
  <summary>Abstract</summary>
Discrete Global Grid Systems (DGGS) have been increasingly adopted as a standard framework for multi-source geospatial data. Previous research largely studied the mathematical foundation of discrete global grids, developed open-source libraries, and explored their application as data integration platforms. This study investigated the multi-resolution terrain analysis in a pure hexagonal DGGS environment, including descriptive statistics, topographic parameters, and topographic indices. Experiments across multiple grid resolutions were carried out in three study areas with different terrain roughness in Alberta, Canada. Five algorithms were proposed to calculate both the slope gradient and terrain aspect. A cell-based pair-wise comparison showed a strong positive correlation between the gradient values as calculated from five algorithms. The grid resolutions as well as the terrain roughness had a clear effect on the computed slope gradient and topographic indices. This research aims to enhance the analytical functionality of hexagonal DGGS to better support decision-making in real world problems.
</details>

**Li, M.**; McGrath, H.; Stefanakis, E. Geovisualization of Hydrological Flow in Hexagonal Grid Systems. Geographies 2(2), 227–244. [**DOI**](https://doi.org/10.3390/geographies2020016) / [**PDF**](https://Erin-1919.github.io/assets/pdf/2022a%20Li%20et%20al.pdf)

<details>
  <summary>Abstract</summary>
Recent research has extended conventional hydrological algorithms into a hexagonal grid and noted that hydrological modeling on a hexagonal mesh grid outperformed that on a rectangular grid. Among the hydrological products, flow routing grids are the base of many other hydrological simulations, such as flow accumulation, watershed delineation, and stream networks. However, most of the previous research adopted the D6 algorithm, which is analogous to the D8 algorithm over a rectangular grid, to produce flow routing. This paper explored another four methods regarding generating flow directions in a hexagonal grid, based on four algorithms of slope aspect computation. We also developed and visualized hexagonal-grid-based hydrological operations, including flow accumulation, watershed delineation, and hydrological indices computation. Experiments were carried out across multiple grid resolutions with various terrain roughness. The results showed that flow direction can vary among different approaches, and the impact of such variation can propagate to flow accumulation, watershed delineation, and hydrological indices production, which was reflected by the cell-wise comparison and visualization. This research is practical for hydrological analysis in hexagonal, hierarchical grids, such as Discrete Global Grid Systems, and the developed operations can be used in flood modeling in the real world. 
</details>

### 2021
**Li, M.**; McGrath, H.; Stefanakis, E. Integration of Heterogeneous Terrain Data into Discrete Global Grid Systems. Cartography and Geographic Information Science 48(6), 546-564. [**DOI**](https://doi.org/10.1080/15230406.2021.1966648) / [**PDF**](https://Erin-1919.github.io/assets/pdf/2021%20Li%20et%20al.pdf)

<details>
  <summary>Abstract</summary>
The Canadian Digital Elevation Model (CDEM) and the High-Resolution Digital Elevation Model (HRDEM) released by Natural Resources Canada are primary terrain data sources in Canada. Due to their different coverage, datums, resolutions, and accuracies, a standardized framework for national elevation data across various scales is required. This study provides new insights into the adoption of Discrete Global Grid Systems (DGGS) to facilitate the integration of multi-source terrain data at various granularities. In particular, the Icosahedral Snyder Equal Area Aperture 3 Hexagonal Grid (ISEA3H) was employed, and quantization, integration, and aggregation were conducted on this framework. To demonstrate the modeling process, an experiment was undertaken for two areas in Ontario, taking advantage of parallel computing which was beneficial from the discreteness of DGGS cells. The accuracy of the modeled elevations was estimated by referring to the ground-surveyed values and was included in the spatially referenced metadata as an indicator of data quality. This research can serve as a guide for future development of a national elevation service, providing consistent, multi-resolution elevations and avoiding complex, duplicated pre-processing at the user’s end. Future investigation into an operational integration platform to support real-world decision-making, as well as the DGGS-powered geospatial datacube, is recommended.
</details>

### 2020
**Li, M.**; Stefanakis, E. Geospatial Operations of Discrete Global Grid Systems – A Comparison with Traditional GIS. Journal of Geovisualization and Spatial Analysis 4(2), 26. [**DOI**](https://doi.org/10.1007/s41651-020-00066-3) / [**PDF**](https://Erin-1919.github.io/assets/pdf/2020%20Li%20and%20Stefanakis.pdf)

<details>
  <summary>Abstract</summary>
As the foundation of the next-generation Digital Earth, Discrete Global Grid Systems (DGGS) have demonstrated both theoretical and practical development, with a variety of state-of-the-art implementations proposed. These emerging DGGS platforms or libraries support preliminary operations such as quantization, cell-level navigation, and conversion between cell addresses and geographical coordinates, while leaving the other more complicated functions unexplored. This paper discusses the functional operations in a DGGS environment, including the essential operations defined by the Open Geospatial Consortium (OGC) Abstract Specification, and the extended operations potentially supported by DGGS. The extended operations are discussed in comparison to the traditional GIS, from the aspects of database techniques, data pre-processing and manipulation, spatial analysis and data interpretation, data computation, and data visualization. It was found that with the OGC-required operations and pre-processing operations as the baseline of development, some function algorithms can facilitate the algorithm development of other analytical functions. Several future research directions regarding the data modeling uncertainties, extended analytic algorithm development, and database and computation technologies are presented. This paper provides a comparison between DGGS and traditional GIS operations and can serve as a reference for future DGGS operation development.
</details>

**Li, M.**; Stefanakis, E. Geo-feature Modeling Uncertainties in Discrete Global Grids: A Case Study of Downtown Calgary, Canada. Geomatica 74, 175-195.  [**DOI**](https://doi.org/10.1139/geomat-2020-0011) / [**PDF**](https://Erin-1919.github.io/assets/pdf/2020b%20Li%20and%20Stefanakis.pdf)

<details>
  <summary>Abstract</summary>
The Open Geospatial Consortium has officially adopted discrete global grid systems (DGGS) as a new option for Earth reference standards. Many state-of-the-art DGGS implementations have been developed, revealing the potential for DGGS applications. Before the wide application of DGGS in solving real-world problems, however, the potential uncertainties of modeling on DGGS should be investigated and documented. This study focused on the uncertainties of geo-feature modeling on DGGS, quantitatively measured the point position displacement and line and polygon features’ geometry distortion, and evaluated the validity of topological relationships. Specifically, traffic cameras (points), main streets (lines), and land-cover classes (polygons) of downtown Calgary (AB, Canada) were modeled in various DGGS configurations at multiple resolutions. Results showed that the point displacement and polygon distortion generally reduced when being modeled at a higher resolution. The tessellations with the monotonical convergence characteristic are recommended if cell indices are expected to represent levels of model precision. Line features’ fidelity was affected by grid tessellations, resolution levels, grid orientation relative to the Earth, and the rotated line directions. The degree of the line distortion was not straightforward to forecast. Maintaining the topological validity between spatial objects with various granularities was challenging and needed further algorithm development for DGGS implementations. The study outcomes can serve as useful guidelines in the selection among grid types, refinement ratios, and resolution levels when applying DGGS implementations to urban environments. This paper also pinpoints several research directions that can benefit the quantization and analysis of vector features on DGGS.
</details>

### 2019
**Li, M.**; MacLean, D.A.; Hennigar, C.R.; Ogilvie, J. Previous Year Outbreak Conditions and Spring Climate Predict Spruce Budworm Population Changes in the Following Year. Forest Ecology and Management 458, 117737. [**DOI**](https://doi.org/10.1016/j.foreco.2019.117737) / [**PDF**](https://Erin-1919.github.io/assets/pdf/2019b%20Li%20et%20al.pdf)

<details>
  <summary>Abstract</summary>
We determined effects of local spruce budworm (Choristoneura fumiferana Clem.; SBW) population level, proximity to sites with high SBW populations, insecticide spray, and environmental variables on SBW populations from 2014 to 2018, the outbreak initiation period in northern New Brunswick, Canada. SBW second instar larvae (L2) per branch data collected at 1100–2000 sample points per year were used to create annual interpolated population rasters. Fishnet sample points extracted from these rasters were overlaid with georeferenced layers of 46 possible predictor variables including forest composition, climate, topography, site quality, and insecticide treatment. Results showed that local SBW population in the previous year, proximity to sites with high SBW populations, and early spring climate were consistently the most important predictors over the 5 study years. Simultaneous autoregressive models were used to address spatial autocorrelation when forecasting the SBW L2 population, and a linear mixed effects model was fit to aggregate data for 2015–2018. The models reduced spatial dependence in the residuals, and explained 68–79% of variance in annual L2 levels and 53% of variance over the 4 years combined. Sensitivity analysis showed that locations with 5–10 more SBW L2 per branch than observed values, or 20–40 km closer to high population sites in the previous year could have up to 24 more L2 in the current year. Cumulative degree days in April helped to estimate the upper and lower bounds of the population. Expansion and retraction of SBW outbreak initiation were mathematically described. Understanding which variables influence SBW outbreak initiation and population level assists in design of small area target-specific insecticide spray applications and helps focus SBW L2 sampling on predicted outbreak hot spots.
</details>

**Li, M.**; MacLean, D.A.; Hennigar, C.R.; Ogilvie, J. Spatial-Temporal Patterns of Spruce Budworm Defoliation within Plots in Québec. Forests 10, 232. [**DOI**](https://doi.org/10.3390/f10030232) / [**PDF**](https://Erin-1919.github.io/assets/pdf/2019a%20Li%20et%20al.pdf)

<details>
  <summary>Abstract</summary>
We investigated the spatial-temporal patterns of spruce budworm (Choristoneura fumiferana (Clem.); SBW) defoliation within 57 plots over 5 years during the current SBW outbreak in Québec. Although spatial-temporal variability of SBW defoliation has been studied at several scales, the spatial dependence between individual defoliated trees within a plot has not been quantified, and effects of defoliation level of neighboring trees have not been addressed. We used spatial autocorrelation analyses to determine patterns of defoliation of trees (clustered, dispersed, or random) for plots and for individual trees. From 28% to 47% of plots had significantly clustered defoliation during the 5 years. Plots with clustered defoliation generally had higher mean defoliation per plot and higher deviation of defoliation. At the individual-tree-level, we determined ‘hot spot trees’ (highly defoliated trees surrounded by other highly defoliated trees) and ‘cold spot trees’ (lightly defoliated trees surrounded by other lightly defoliated trees) within each plot using local Getis-Ord Gi* analysis. Results revealed that 11 to 27 plots had hot spot trees and 27% to 64% of them had mean defoliation <25%, while plots with 75% to 100% defoliation had either cold spot trees or non-significant spots, which suggested that whether defoliation was high or low enough to be a hot or cold spot depended on the defoliation level of the entire plot. We fitted individual-tree balsam fir defoliation regression models as a function of plot and surrounding tree characteristics (using search radii of 3–5 m). The best model contained plot average balsam fir defoliation and subject tree basal area, and these two variables explained 80% of the variance, which was 2% to 5% higher than the variability explained by the neighboring tree defoliation, over the 3–5 m search radii tested. We concluded that plot-level defoliation and basal area were adequate for modeling individual tree defoliation, and although clustering of defoliation was evident, larger plots were needed to determine the optimum neighborhood radius for predicting defoliation on an individual. Spatial autocorrelation analysis can serve as an objective way to quantify such ecological patterns.
</details>

## Conference Presentations
### 2022
**Li, M.**; McGrath, H.; Stefanakis, E. Analytical operations for terrain data modeled in Discrete Global Grid Systems. Canadian Cartographic Association Conference, May 2022, Online. [**Pre-Recorded Presentation**](https://drive.google.com/file/d/1DECGOtfzUCyaSrtsDGUxXjXPVS3JcYSJ/view?usp=sharing)
  
### 2021
**Li, M.**; McGrath, H.; Stefanakis, E. Integration of multi-source terrain data on Discrete Global Grids in Canada. Canadian Cartographic Association Conference, May 2021, Online. [**Pre-Recorded Presentation**](https://drive.google.com/file/d/1I0YnzykCr2wq41E5z4sy4xFBjiChINmA/view?usp=sharing)

### 2020
**Li, M.**; Stefanakis, E.; McGrath, H. National terrain data management on Discrete Global Grids in Canada. AutoCarto 2020, Oct. 2020, Online. [**PDF**](https://cartogis.org/docs/autocarto/2020/docs/abstracts/3h%20National%20Terrain%20Data%20Management%20on%20Discrete%20Global%20Grids%20in%20Canada.pdf) / [**Pre-Recorded Presentation**](https://cartogis.org/docs/autocarto/2020/docs/presentations/3h%20National%20Terrain%20Data%20Management%20on%20Discrete%20Global%20Grids%20in%20Canada.mp4)

### 2018
**Li, M.**; MacLean, D.A.; Hennigar, C.R.; Ogilvie, J. Spatial-tempol patterns of spruce budworm defoliation within measured plots in Québec. The 9th Bi-Annual Eastern Canada - USA Forest Science Conference, Oct. 2018, Fredericton, Canada.

**Li, M.**; MacLean, D.A. GIS analyses of factors influencing spruce budworm outbreak initiation in northern New Brunswick. SERG International Workshop, Feb. 2018, Edmonton, Canada.

## Other Invited Talks
### 2022
Flood Susceptibility Modeling in Discrete Global Grids under Climate Change Scenarios. Presented at the Natural Resources Canada, Oct. 2022, Online.

Geospatial Data Analysis in Discrete Global Grid Systems – Progress and Perspectives. Presented at the China Agricultural University, May 2022, Online.  

Quantization, Analysis, and Application of Terrain Data Modeled in Discrete Global Grid Systems. Presented at the International Society for Photogrammetry and Remote Sensing Work Group IV/7 (Geo-Data Management) Webinar, Jan. 2022, Online. [**Recorded Presentation**](https://www.youtube.com/watch?v=FWGl4lSrIyA)

### 2021
Integration Platform for Canadian Terrain Data: A DGGS Perspective. Presented at the Natural Resources Canada, Apr. 2021, Online.
