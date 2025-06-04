---
title: "Multi-resolution DEM Fusion"
layout: post
---

![terrainfusion](https://images.unsplash.com/photo-1520299607509-dcd935f9a839?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1189&q=80)

### General steps of DEM fusion

1. **Preprocessing**  
Systematic differences in geo-referencing between two independent DEMs—both in planimetry and height—must be unified. This includes horizontal and vertical datum transformation, projection conversion, grid size standardization (via interpolation), and vertical offset adjustment.

2. **Repairing data quality issues**  
Depending on the collection technique, land cover, and terrain type, DEMs may have voids, anomalies, or noise. Void-filling methods are applied to address these issues before fusion.

3. **Main fusion or blending processes**  
Different fusion algorithms may be applied depending on land cover and topography. For example, Tran et al. (2014) proposed methods tailored to varying terrain types. Treatment of ocean areas also requires special consideration.

4. **Surface smoothing**  
Smoothing can be applied before or after fusion to reduce noise in the final DEM.

5. **Final accuracy assessment**  
The fused DEM is evaluated against ground control points or high-quality LiDAR data.

6. **Real-world applications**  
Fused DEMs can be used to derive topographic and hydrologic features, which are then compared to LiDAR-derived equivalents to validate performance.

### Methods of DEM fusion

1. **Weighted averaging**  
Input DEMs are resampled to the same grid, and output values at each grid node are calculated by weighted averaging.  
- Works well in most cases  
- Choice of weights is critical and can be informed by global error metrics (Fuss 2013; Papasaika et al. 2009), error maps (Reinartz et al. 2005; Roth et al. 2002), terrain derivatives (Lucca 2012; Tran et al. 2014), or combinations (Papasaika et al. 2008)  
- Limitations: ignores spatial continuity and may introduce artifacts from up-sampling  
- Use cases: Papasaika et al. 2008, Lucca 2012, Tran et al. 2014, Robinson et al. 2014, Schindler et al. 2011, Constantini et al. 2006, Reinartz et al. 2005, Schultz et al. 1999, Xu et al. 2010

2. **Sparse representations**  
This approach includes prior knowledge of plausible surface shapes to suppress unrealistic local geometries.  
- Weights are still required and can be derived using standard error propagation  
- More robust to blunders  
- Use case: Papasaika et al. 2011

3. **Frequency or spectral domain fusion**  
Uses methods like Fourier transforms to separate and merge low-frequency (coarse) and high-frequency (fine) features from different DEMs.  
- Useful when combining InSAR and photogrammetric DEMs  
- Steps include transforming to frequency domain, filtering, summing spectra, and inverse transforming  
- Use cases: Karkee et al. 2008, Karakasis et al. 2014, Honikel 1998, Crosetto and Aragues 2000

4. **Linear regression calibration**  
A simple method where elevation differences between DEMs are modeled with a linear regression.  
- Use case: Furze et al. 2017

5. **Collocation method**  
A stochastic method using covariance functions to predict signal values.  
- Suitable when signals have zero mean; otherwise, kriging is preferred  
- Allows point prediction from area-averaged values  
- Use case: Lucca 2012

6. **Multi-scale stochastic smoothing (Kalman filtering)**  
Applies a Kalman filter across scales, minimizing mean squared error while fusing DEMs.  
- Especially useful for fusing InSAR data of different resolutions  
- Use case: Slatton et al. 2002

7. **Clustering algorithm**  
Uses k-means to detect and average consistent elevation values at each cell location.  
- Assumes similar values are more accurate  
- No prior error knowledge is required  
- Use case: Fuss 2013

8. **Self-consistency checks**  
Two DEMs are generated from the same stereo image pair with reversed roles. Cells with differences above a threshold are discarded.  
- Use cases: Schultz et al. 1999, 2002
