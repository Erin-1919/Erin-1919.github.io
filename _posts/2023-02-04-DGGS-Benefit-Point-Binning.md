---
title: "DGGS Benefit Point Binning"
layout: post
---
![bin](/assets/img/20230204/bin.jpg)

**One of the major applications of DGGS is to grid and aggregate point data with their spherical polygons serving as bins. This can be useful in census investigation, natural disturbance monitorization, and geographical mapping.**
 
## Equal-sized cells/bins for spatial statistics
DGGS tessellates the Earth's surface with almost equal size cells and preserves the Earth's curvature, this offers an ideal framework for spatial statistics where we do not need to worry about projections and spatial bias due to the fuzzy cell sizes. In traditional situations, what people end up studying is not their data but the space they project the data into, and the purpose of DGGS is to avoid such problems.
 
## Data de-redundancy/down-sampling
Point datasets can be volumetric and redundant which need a down-sampling process to get them ready for follow-up analysis, such as point cloud. Using hexagonal DGGS as a down-sampling framework for point datasets is ideal because of its uniform adjacency and constant cell area over the globe. They can decrease the data size, only preserve the characteristics of interest, and prepare them in a way that more standardized algorithms can be applied directly.
 
## Multi-resolution
DGGS are inherently multi-resolution so multi-scale data aggregation is naturally achievable. DGGS allow large or small-scale binning without projection distortion. This property gives point binning in DGGS more flexibility in terms of spatial resolution. The modifiable areal unit problem (MAUP), which is a source of statistical bias that can significantly impact the results of statistical hypothesis tests, can be easily demonstrated in the DGGS environment. 
 
## Consistent monitorization
DGGS cells have registered, fixed locations at a certain resolution, which exactly benefits the continuous monitoring of geographical phenomena. Census investigation, as an example of consistent monitorization, can benefit from the adoption of DGGS. Traditionally, the use of irregular, complex geometries based on dynamic data as the base unit for statistical analysis is problematic because of heterogeneous census datasets and precision/geospatial errors. DGGS, however, provide a simple, globally consistent, hierarchical, and fixed set of geometries that can support data comparisons within and across statistical datasets. It can also simplify the process of aggregation and spatial queries of enumerated areas.

