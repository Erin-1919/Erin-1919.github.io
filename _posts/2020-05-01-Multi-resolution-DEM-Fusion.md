---
title: "Multi-resolution DEM Fusion"
layout: post
---

![terrainfusion](https://images.unsplash.com/photo-1520299607509-dcd935f9a839?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1189&q=80)

### General steps of DEM fusion:
1. **Preprocessing.** Systematic differences between the geo-referencing of two independent DEMs, both in planimetry and height, need to be unified. This includes horizontal and vertical datum transformation, projection conversion, grid size standardization (interpolation), and vertical offsets adjustment.
2. **Repairing data quality issues.** Some DEMs may have voids, anomalies, or noise, depending on the data collection techniques, landcover types, and topographical characteristics. To improve the data quality before fusion, void-filling approaches are applied to original DEMs. 
3. **Main fusion/blend processes.** In this step, different algorithms may be applied according to different landcover types and topographical characteristics (e.g., Tran et al. 2014). Another point that needs consideration is the way to deal with the ocean.
4. **Surface smoothing process.** It helps to reduce noise in the output fusion DEM. This may be applied separately on DEMs to be fused before data fusion or be applied on the fused DEM.
5. **Final accuracy assessments.** This can be done by comparing the fused DEM to field-measured control points, or LiDAR generated high-quality DEM values. 
6. **Real-world applications.** Use the fused DEM to generate DEM-derived topographical or hydrological features, and compare the results to those produced from high-quality LiDAR-DEM.

### Methods of DEM fusion:
1. DEM fusion by weighted averaging. Probably the most obvious fusion algorithm is to simply resample the two input DEMs to the same grid and compute an output value at each grid node by weighted averaging of the inputs. 
    * In practice, it works well for most cases.
    * The correct choice of weights has a far greater influence on the results than the mathematical recipe for fusing the inputs. 
    * The way to determine the weighting scheme can be dependent on global measures of error (Fuss 2013: Papasaika et al., 2009); height error maps from the DEM generation process (Reinartz et al., 2005; Roth et al., 2002); terrain derivatives / geomorphologic characteristics (Lucca 2012, Tran et al. 2014); or combinations thereof (Papasaika et al. 2008).
    * Main weaknesses: it looks at each grid point independently, disregarding the resulting surface shape; and the up-sampling of one of the input DEMs could potentially introduce further artifacts, which however is a largely theoretical concern with little practical relevance.
    * Use cases: Papasaika et al. 2008, Lucca 2012, Tran et al. 2014, Robinson et al. 2014, Schindler et al. 2011: Constantini et al. 2006, Reinartz et al. 2005, Schultz et al. 1999, Xu et al. 2010
2. DEM fusion with sparse representations. To mitigate the first weakness of weighted averaging, it has been proposed to exploit the framework of sparse representations for DEM fusion. In a nutshell, the rationale is the following: to be more robust to blunders it would be desirable to include prior knowledge about plausible surface shapes, such that improbable local surface geometries caused by blunders are suppressed.
    * For both described methods (and most other conceivable fusion schemes) weights are required, which govern the relative influence of the two input DEMs at a given raster location. These weights are critical for proper DEM fusion. Under the simplifying assumption that there are no blunders, these weights can be derived by standard error propagation.
    * Use cases: Papasaika et al. 2011
3. DEM fusion in a frequency/spectral domain. Different spectral methods such as Fourier series and polynomial-based expansions can be used in the fusion process.
    * The basis of this technique is that the lower frequency portion of one DEM (i.e. coarser terrain features) can be isolated and merged with the higher frequency portion of another DEM (i.e. finer terrain features) of the same area. 
    * Advantages of merging InSAR and stereo-photogrammetry DEMs: the InSAR DEMs tend to be more accurate in the high frequency, and the stereo-photogrammetric DEMs tend to be more accurate in the low frequencies. Frequency domain filtering such as ideal low-pass and high-pass filters can be applied to remove the erroneous frequency components from both of the DEMs in the frequency domain before they were combined into a single DEM.  
    * Four main steps: 
i. Converting the DEMs into the frequency domain by for example Fourier transform
ii. Applying a low or high pass filter to the appropriate DEM.
iii. Adding the two desired DEM portions, namely summing two spectra to be fused in the frequency domain.
iv. Converting the fused DEM back into a spatial domain (e.g., inverse Fourier transform).
    * Use cases: Karkee et al. 2008, Karakasis et al. 2014, Honikel 1998, Crosetto and Aragues 2000
4. Calibration by linear regression. 
    * Use cases: Furze et al. 2017
5. Collocation method. Collocation is a stochastic method to model and predicts a signal using its stochastic properties (e.g covariance function).
    * It assumes that the signal has a zero mean, otherwise the use of the kriging prediction method is more suitable (Sanso 1986, Koch 1997).
    * The stochastic approach allows the prediction of a point value from an average one.
    * Use cases: Lucca 2012
6. Multi-scale stochastic smoothing. The multi-scale Kalman filter considers the stochastic variability in parameters and is optimal concerning the minimal mean squared error involved in the DEM fusion model.
    * Use cases: Slatton et al. 2002 -- fuse InSAR DEMs of different resolutions
7. Clustering algorithm. The algorithm utilizes k-means clustering to detect elevations at each grid cell location that are in close agreement. 
    * The main assumption of this technique is that elevations in the close agreement will be more accurate than those that are not. 
    * No *a priori* knowledge of the input DEM error is used in this fusion technique.
    * Use cases: Fuss 2013
8. DEM fusion by self-consistency. Two DEMs are generated from the same pair of images by switching the reference and target roles for elevation extraction. If the elevation estimates at the same cell location differ by greater than a threshold distance the estimates are not accepted.
    * Use cases: Schultz et al. 1999, 2002
