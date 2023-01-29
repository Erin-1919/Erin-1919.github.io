---
title: "TIN vs DGGS in Terrain Modeling"
layout: post
---
![TIN](/assets/img/20230129/TIN.png)

## Geometry
Triangulated Irregular Networks (TINs) consist of irregular triangles and Discrete Global Grid Systems (DGGS) are constructed by uniform, regular cells. Cell geometry is usually among the choices of triangles, quadrilaterals, and hexagons.  
 
## Representation of elevations
TINs represent elevations with sets of triangular faces by storing values at the triangle vertices. DGGS have the elevation value modeled at each cell centroid which represents the elevation of a certain cell. 
 
## Scale
TINs normally deliver elevation information at one single resolution while DGGS is an inherently multi-scale data model which can present elevations at a resolution on demand. 
 
## Storage Format
TINs are essentially vector-based digital geographic data so the format of storing TINs is similar to vectors, where points' coordinates, pointes' elevations, edge directions, and topologies are required information. In terms of a DGGS, cell address and corresponding information are the basic information, which is less complex than that for a TIN. 
