---
title: "What is a Right Resolution of DEMs?"
layout: post
---

![terrain](https://images.unsplash.com/photo-1472101126021-3910d43690a9?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1191&q=80)

### So... How to determine an appropriate resolution for the digital elevation model (DEM)?
> > We need a grid resolution that optimally reflects the complexity of a terrain; one that can represent the majority of the geomorphic features. Suitable cell size can be derived for a given set of sampled elevations (e.g., contours or points), to fit the complexity of the terrain and/or the scale of work for the targeted application (Hengl and Evans, 2009).

### These are some points to be considered after reviewing literature:
1. The original source. 
    * When modeling elevation from vector contours, one needs to consider the horizontal and vertical intervals or the total length of the contours
    * DEM products gained from satellites (e.g., ASTER and SRTM) have fixed resolutions, increasing resolution from available datasets does not generate more information
    * LiDAR can give both fine resolutions and degraded resolutions, and both bare-earth elevation and surface elevation
2. The vertical resolution.
    * If the cell size is too fine in relation to the vertical accuracy, it might introduce local artifacts and slow down the computation of land-surface parameters.
3. The application domain.
    * Hydrological modeling
    * Solar radiation modeling
    * Topographic derivatives
    * Specific features like ridgeline, valley lines, and drainage paths
4. The terrain complexity of the interested area or the process to be modeled
    * Steep terrain (e.g., alpine region) or flat terrain (e.g., prairie)
    * Scale of the processes being modeled
    * Numerical simulation approach
    * Size of the land surface features that are to be resolved
5. Users' demand.
    * Requirement of level of detail
    * Data volume
    * Cost
