---
title: "Major Differences, in Concept, between Traditional GIS and DGGS"
layout: post
---
![grid](/assets/img/20221012/grid.jpg)

## Thematic layers vs. Congruent geography
 
I like the saying "GIS slices the world into layers of information; DGGS brings that information together again.". In the field of GIS, 'layer' is one of the core concepts to model real-world phenomena, where each 'layer' represents one aspect of the geospatial information. This is practical when one is interested in only one type of geospatial information but not convenient when gathering multi-layer information at one certain geospatial location. Vector layers have various basic geometries like point, polyline, and polygon, which need additional operations when extracting information from multiple layers. Raster layers commonly have different resolutions, transformations, origins, etc., which requires pre-processing to standardize matrix shapes before further analysis. This is why datacube is increasingly prevalent in spatial data management. In contrast, DGGS have their cells registered at fixed locations at each resolution level, which is essentially a multi-resolution congruent geography. This benefits the continuous observation of one certain geo-location, and the extraction of all available information at one location becomes straightforward. 
 
## Single resolution vs. Multiple granularities
 
Analysis with traditional GIS is, although not all of them, almost at a single resolution. Even if a multi-scale study is carried out with traditional GIS, the definition of resolution or scale is vague because there is no quantitative, systematic measure of spatial scale. Additionally, people are used to observing the world at a single resolution due to the nature of the human visual system and so does our daily experience. Although scientists have recognized the advantages of multi-scale perspectives, the concept remains challenging to most people, especially those not in the geospatial science domain. DGGS have a hierarchical structure no matter the specific configuration. Each design of DGGS has a certain refinement ratio, and each level of partition exclusively defines a cell size, namely resolution. Such resolutions are systematic because the refinement ratio between levels is consistent. Hence, modeling, analysis, observation, and visualization of geospatial data in a DGGS is essentially multi-scale.
 
## Continuous vs. Discrete
 
The process of digitalization is essentially a process of discretization, think about digital music or photos. One of the key properties of a DGGS is discrete, meaning that a DGGS consists of a finite number of cells at a resolution level. Each cell is computationally independent of the others. A grid system can simplify the modeling process of the real-world phenomenon, and various geographic grid systems existed. DGGS is exceptional because it guarantees global coverage, no overlaps or gaps, uniform grid size, and thus uniform spatial resolution. This outperforms other existing grid systems like graticule and Google's S2. Traditional GIS commonly models geospatial objects in a continuous space where locations are represented by floating-point-based coordinates. This may suffer from problems like storing infinite float digits using finite memory bits, continuous observation of a point-based location, topological ambiguity in neighborhood definition, etc. 
 
## Flat model vs. 3D model
 
Vector or raster are flattened data models because they are frequently projected to a 2D Cartesian space and use floating-point-based coordinates to present spatial locations. Even Google Earth powered a 3D visual representation of the Earth, it remains a flattened technology because the underlying data model is flattened. DGGS is a fully three-dimensional representation of the entire planet which considers Earth's curvature during its construction. Furthermore, flat models always lead to inconsistent spatial resolutions especially across a large geospatial area because no such a projection can retain area, form, and distance unchanged globally. It means that 2D models have an inconsistent spatial resolution among latitudes because of the inherent flattening. On the contrary, 
spatial resolution is always explicit and approximately constant at every level of the hierarchical structure in DGGS.
