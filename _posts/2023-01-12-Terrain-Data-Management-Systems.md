---
title: "Terrain Data Management Systems"
layout: post
---
![DEMsys](/assets/img/20230112/DEMsys.jpg)

## GMTED2010 
The Global Multi-resolution Terrain Elevation Data 2010 project integrated raster terrain data from 11 sources, where weight-based mosaic functions were used to combine heterogeneous data to create smooth transitions over the overlapping zones of the neighboring grids. [Source](https://www.usgs.gov/centers/eros/science/usgs-eros-archive-digital-elevation-global-multi-resolution-terrain-elevation)
 
## 3DEP
The 3D Elevation Program created national seamless Digital Elevation Models (DEM) by feathering and edge-matching seven sources of data into a successive terrain surface, where high-quality Light Detection and Ranging (LiDAR) and Interferometric Synthetic Aperture Radar (IfSAR) data had the highest priority. [Source](https://www.usgs.gov/3d-elevation-program)
 
## QTM
The Quaternary Triangular Mesh was developed to assemble and manage global terrain data, which started from an octahedron circumscribed by a datum with two vertices at the poles and four vertices at the equator, dividing each triangular parent cell into four child cells. Elevation values were assigned to consecutive triangular facets. [Source](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=dc48cdb302cdec4b356d330a630f0f589d1ab87c)
 
## GEM
The Geodesic Elevation Model began as a cuboctahedron connected into a rhombic dodecahedron, recursively refining each face into nine partially nested equilateral triangles. [Source](https://doi.org/10.3138/R613-191U-7255-082N)
 
## ECM
The Ellipsoidal Cube Map consists of a reference ellipsoid, a circumscribing cube, and a map projection from the ellipsoid surface to the six cube sides. It was proposed to render planetary-scale terrain datasets. [Source](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=ee6ccd6c9e4f2a2030eac18e71c214dd1f523066)
 
## Crusta 
Crusta represents the globe as a 30-sided polyhedron to avoid distortion of the display, in particular, the singularities at the poles characteristic of other projections. It was based on the quadtree and enable the dynamic shading of the terrain surface computed on-the-fly when a user manipulates his point-of-view. [Source](https://doi.org/10.1016/j.cageo.2010.02.006)
