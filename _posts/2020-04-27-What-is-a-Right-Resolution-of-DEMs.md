---
title: "What is a Right Resolution of DEMs?"
layout: post
---

![terrain](https://images.unsplash.com/photo-1472101126021-3910d43690a9?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1191&q=80)

### So... how to determine an appropriate resolution for the digital elevation model (DEM)?

> We need a grid resolution that optimally reflects the complexity of a terrain, one that can represent the majority of the geomorphic features. Suitable cell size can be derived for a given set of sampled elevations (e.g., contours or points), to fit the complexity of the terrain and the scale of work for the targeted application.  
> *(Hengl and Evans, 2009)*

### These are some key considerations drawn from literature:

1. **The original data source**  
   - When modeling from vector contours, horizontal and vertical intervals or the total contour length affect the resolution choice  
   - DEMs from satellites like ASTER and SRTM have fixed resolutions; artificially increasing resolution adds no new detail  
   - LiDAR supports both high and degraded resolutions and provides both bare-earth and surface elevation models

2. **The vertical resolution**  
   - If spatial resolution is too fine compared to vertical accuracy, it may introduce local noise and slow down the computation of terrain derivatives

3. **The application domain**  
   - Hydrological modeling  
   - Solar radiation analysis  
   - Slope, aspect, and curvature computation  
   - Identification of features like ridgelines, valleys, and drainage paths

4. **The terrain complexity or the process to be modeled**  
   - Steep terrains (alpine zones) versus flat landscapes (prairies)  
   - Scale and resolution of the process being studied  
   - Size of the landform features to be captured  
   - Numerical simulation method used

5. **User demand and constraints**  
   - Desired level of detail  
   - Available storage and processing power  
   - Budget or licensing cost associated with higher-resolution data
