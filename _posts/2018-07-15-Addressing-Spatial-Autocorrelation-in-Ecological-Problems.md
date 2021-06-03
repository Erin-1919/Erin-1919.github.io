---
title: "Addressing Spatial Autocorrelation in Ecological Problems"
layout: post
---

![Ecological](https://images.unsplash.com/photo-1534709153997-d6659469f951?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1050&q=80)

>> Everything is related to everything else, but near things are more related than distant things.
>> The first law of geography, Tobler, 1970

## The definition of spatial autocorrelation
By the 1990s, the field of spatial analysis had been witnessed to matured in both concepts and methods, becoming increasingly fundamental in a lot of disciplines including geography, ecology, sociology, urban planning, environmental studies, etc. (Getis 2007). As its core concept, spatial autocorrelation has attracted more attention from researchers. Spatial autocorrelation shows the correlation among variables across georeferenced space, defined as the observed value of the variable at one locality is dependent on the values at neighboring localities (Sokal 1977). The larger the correspondence between two paired values of a variable, the greater the degree of spatial autocorrelation. Generally, if high (or low) values of the variate are associated with high (or low) values at surrounding localities, the spatial autocorrelation is positive; while if high (or low) values are surrounded by low (or high) values, the spatial autocorrelation is negative. If they do not show conspicuous similarity or dissimilarity, then spatial autocorrelation will not be in evidence (Getis 2007). The typical classification of the spatial situations is based on the nature of 1) regular or irregular system of sites; 2) individual sites being points or regions, and 3) associated variables being discrete or continuous (Besag 1974)

## Spatial autocorrelation analysis
Spatial analysis is one of the main components of geographic information science. As a branch of spatial analysis, spatial autocorrelation analysis tests if the observed value at one location is independent of the value of the interested variable at neighboring locations by reporting different indices accompanied with their statistical significance tests. Namely, the ecological factor is being tested against itself in autocorrelation analyses (Koenig 1999). These quantitative indices are not only useful to characterize, clarify, and classify the distribution patterns of the interested ground objects but also helps to bridge the gap between ecology mechanism and the behavior of the investigated phenomena (Foster and Townsend 2013). However, if an ecological factor is being tested against another factor, the cross-correlation analysis is being carried out. A cross- correlational analysis can help to reveal the possible cause of a variety of ecological phenomena which are interconnected potentially (Koenig 1999). 

## Benefits of spatial-temporal distribution pattern research 
Strategies of number and position of insect-trapping, as well as frequency of insect-trapping, were traditionally based on logistics, but it will be more efficient and reasonable to base on bionomics and spatial distribution of the target insects (Ryan et al 2004). 

Study of the spread patterns including spatial and temporal spread processes of spruce budworm defoliation is essential because forest resources are profoundly affected by the insect disturbance in terms of local ecosystems as well as forestry finance. The insight of mapping spatial-temporal patterns will allow forest management strategies to be more efficient and sustainable by targeting those “hotspots” in infested forests. 

##Benefits for spatial analysis techniques
Traditionally, insects’ spatial dispersion patterns were studied by the variance-mean-based relationship between samples which did not account for the spatial location of those samples (Liebhold et al 1991). However, spatial autocorrelation determines the degree of dependence of spatially-related data, offering a more efficient measure of spatial dependence than the traditional approaches (Papadopoulos 2003). 

## Typical sources of spatial autocorrelation of responses
1.	Biological processes are distance-related, like speciation, extinction, dispersal, conspecific attraction, synchronous population fluctuations, and species interactions (Augustin et al. 1998).  
2.	Non-linear relationships between environment and species are modeled erroneously as linear (Dormann et al. 2007).
3.	The statistical model fails to account for a spatially structured environmental predictor which is important in explaining the dependent variable, resulting in spatial structuring in the response (Besag 1974). 
4.	Coarser spatial resolution leads to a spatial smoothing of data (Dormann et al. 2007). 

## Reasons for encountering spatial autocorrelation in ecological data modeling
Because of all the above reasons, spatial autocorrelation may confound the standard analysis of ecological data, like species distribution, gene frequency, land use, etc. Especially for species distribution analysis, in which species abundances tend to be positively autocorrelated, spatial autocorrelation should always be encountered in the study (Tsulyki 2008). When developing ecological models, ignorance of spatial autocorrelation would trigger some independent variables appearing to have effects on a response while actually, their relationships are not statistically significant (Legendre 1993, Tsulyki 2008). Also, if spatial autocorrelation remains in the residuals of a statistical model, it will violate one of the key assumptions of standard statistical analyses that residuals should be independent (Dormann et al. 2007). 

## Previous studies on analyzing spatial distribution patterns 
Over the past few decades, spatial analysis techniques were applied frequently and efficiently to datasets including plants, animals, and human beings, contributing to inferences of selection, migration, drift, and isolation by distance (Sokal et al. 1998). 

### Insects
A study examined the spatial and temporal dispersion patterns of the Mediterranean fruit fly (Ceratitis capitata) within a relatively small geographic area, a farm close to Thessaloniki, northern Greece (Papadopoulos 2003). Moran’s I and correlograms were used in spatial statistics analyses (performed on five lag classes) and spatial autocorrelation significance testing. Spatial patterns of four different mosquito species were analyzed in Redland Shire in southeastern Queensland, Australia (Ryan et al. 2004). In their study, Moran’s I analyses were used to evaluate the degree of spatial autocorrelation and interdependence, and universal kriging was used to assess the predicted number of mosquitoes of each species at unsampled locations within the study area. Boiteau (2005) conducted a project on quantifying the spatial structure of the Colorado Potato Beetle (Coleoptera: Chrysomelidae) in northern New Brunswick. Spherical, Exponential, Gaussian, and Power models were fit, and their sample variograms were visually compared, to analyze the spatial dependency among samples. Spatial distribution of the Cereal Leaf Beetle (Coleoptera: Chrysomelidae) in wheat was studied by Reay-Jones (2010), during which Inverse Distance Weighted (IDW) interpolation was used to examine the *O. melanopus* spatial patterns, and cross-validation was also used to test the fit of IDW model. 

### Plants
Univariate and bivariate Ripley’s K statistics were used to quantify the spatial patterns of individual tree and sapling establishment in four permanent plots of the boreal forest of Quebec after a spruce budworm outbreak (Rossi and Morin 2011). It suggested that saplings were aggregated, whereas trees showed a random pattern of stem distribution. The study of Foster and Townsend (2013) quantified spatial dependence of European gypsy moth (*Lymantria dispar* L.) defoliation on spatial patterns of host species abundance, phenology, topography, and insecticide spray treatment. After fitting a linear model, they found the spatial autocorrelation in residual defoliation of the model, described by Moran’s I, corresponded well with gypsy moth dispersal distances (0.1-1km). The research succeeded not only in explaining exogenous factors of defoliation but also in isolating residual patterns which determined the potential endogenous factors (moth dispersal). A series of spatial autocorrelation analysis including Moran’s I and Geary’ c was performed on tree species, product, defect, and the basal area within Loblolly Pine stand across the southern United States, to test the spatial autocorrelation of these discrete or continuous tree characteristics (Reed and Burkhart 1985). They also assign the investigated tree characteristics to individual trees in computer-generated stands based on their measures of spatial autocorrelation. The research of Czaplewski et al (1994) detected a spatial autocorrelation in reduced growth of undisturbed natural pine stands across Georgia by using spatial statistics and demonstrated that spatial analyses can contribute to testing cause-effect relationships hypotheses (growth loss of pine stands was caused by local stand conditions instead of other causes like air pollution). They also proposed a new spatial statistic, partial Moran’s I, to reveal more details of unusual spatial patterns. 

## Previous studies on ecological modeling accounting for spatial autocorrelation
The objectives of ecological modeling include 1) exploring the possible relationships between responses and associated covariates which are spatially referenced; 2) making a forecast of the response values at unsurveyed locations; and 3) estimating global characteristics of the distribution (e.g., the average value of a response over the whole region of interest; Augustin 1998). Encountering spatial autocorrelation, many studies have been carried out among different fields, including wildlife distribution, plant species distribution, habitat distribution, gene frequency distribution, land-use change over time, etc. 

### Wildlife distribution
As early as 1996, Augustin et al. (1998) generated three approaches (flexible regression models, autologistic models, and spatio-temporal models) to model spatial data which have spatial autocorrelation among sample grids. Among these, the second approach is appropriate for binary data. After applying on the red deer distribution data, which used the study of Buckland and Elston (1993) as a start point, this modeling strategies succeeded not only in explaining response variable in the surveyed sites but also in estimating the probability of a certain species being present in the unsurveyed sites. In another study that analyzed the mountain yellow-legged frog (*Rana muscosa*) patch occupancy, a semiparametric logistic model and an autologistic model were developed and compared (Knapp et al. 2003). Their results indicated that two models provided good fits of the frog data, while the autologistic model was more useful in forecasting the frog patch occupancy. In the attempts to model the distribution of the Javan Hawk-Eagle (*Spizaetus bartelsi*), Tsuyuki (2008) use the final logistic regression as the starting point for fitting an autologistic regression model, analyzing the distribution of the Javan Hawk-Eagle (*Spizaetus bartelsi*). The constructed autologistic model showed a significant increase in overall model accuracy. 

### Plant species distribution
A study of *O. digyna* distribution in the British Isles encountered autocorrelation in logistic regression by constructing additional variables, i.e., the proportion of available squares containing presences of such species, from the species data to be modeled (Smith 1994). The result suggested a fairly good explanation of relationships between the distribution of *O.digyna* and associated environmental variables, while the model performed poorly in prediction comparatively. Wu and Huffer (1997) applied an autologistic regression model for spatial binary data of two plant species (*Castanea pumila* and *Zanthoxylum clava-herculis*) on a regularly spaced lattice. In their research, three methods of parameter estimation were applied and compared, and the Markov Chain Monte Carlo (MCMC) method was believed to give the best estimates, and the Maximum Pseudolikelihood (MPL) method was determined to require the least computation. 

## Determine the cell size
The model generated by Buckland and Elston (1993) was based on a 1x1 km grid system, which recorded the number of deer counted per grid. Deer data was collected by Natural Habitat Survey carried out by Red Deer Commission, Grampian Regional Council. It means the survey itself determined the grid size.

In the study of Knapp et al. (2003), the objectives within 2km are defined as neighbors which were used to generate the neighbor system in the autologistic regression. The 2km threshold was chosen because the mountain yellow-legged frog (*Rana muscosa*), which was their study object, rarely move between water bodies separated by greater than 1km. It means that the threshold in this study was determined by the frogs’ biological nature. 

The research on the distribution of the Javan Hawk-Eagle (*Spizaetus bartelsi*) used a set of raster layers with 30x30m pixel size as their study basis and tried several different sizes of neighborhood searching window ranging from 450m (15x15 moving window) to 1500m (50x50 moving window; Tsuyuki 2008). 

## References
Augustin, N.H., Mugglestone, M.A., and Buckland, S.T. 1998. The role of simulation in modelling spatially correlated data. Environmetrics 9: 175-196.

Besag, J., 1974. Spatial interaction and the statistical analysis of lattice systems. Journal of the Royal Statistical Society: Series B (Methodological), 36(2), pp.192-225.

Boiteau, G., 2005. Within-field spatial structure of Colorado potato beetle (Coleoptera: Chrysomelidae) populations in New Brunswick. Environmental entomology, 34(2), pp.446-456.

Buckland, S.T. and Elston, D.A., 1993. Empirical models for the spatial distribution of wildlife. Journal of applied Ecology, pp.478-495.

Czaplewski, R.L., Reich, R.M. and Bechtold, W.A., 1994. Spatial autocorrelation in growth of undisturbed natural pine stands across Georgia. Forest Science, 40(2), pp.314-328.

Dormann, C.F., Mcpherson, J.M., Arau, M.B., Bivand, R., Bolliger, J., Carl, G., Davies, R.G., Hirzel, A., Jetz, W., Kissling, W.D., Ohlemu, R., Peres-neto, P.R., Schurr, F.M., and Wilson, R. 2007. Methods to account for spatial autocorrelation in the analysis of species distributional data: a review. Ecography 30: 609-628.

Foster, J.R., Townsend, P.A. and Mladenoff, D.J., 2013. Mapping asynchrony between gypsy moth egg-hatch and forest leaf-out: Putting the phenological window hypothesis in a spatial context. Forest ecology and management, 287, pp.67-76.

Getis, A., 2007. Reflections on spatial autocorrelation. Regional Science and Urban Economics, 37(4), pp.491-496.

Knapp, G. and Hartung, J., 2003. Improved tests for a random effects meta‐regression with a single covariate. Statistics in medicine, 22(17), pp.2693-2710.

Koenig, W.D., 1999. Spatial autocorrelation of ecological phenomena. Trends in Ecology & Evolution, 14(1), pp.22-26.

Legendre, P. 1993. Spatial autocorrelation: trouble or new paradigm? Ecology 74(6): 1659-1673.

Liebhold, A.M., Zhang, X., Hohn, M.E., Elkinton, J.S., Ticehurst, M., Benzon, G.L. and Campbell, R.W., 1991. Geostatistical analysis of gypsy moth (Lepidoptera: Lymantriidae) egg mass populations. Environmental Entomology, 20(5), pp.1407-1417.

Papadopoulos, Y., 2003. Cooperative forms of governance: Problems of democratic accountability in complex environments. European Journal of Political Research, 42(4), pp.473-501.

Reay-Jones, F.P.F., 2010. Spatial and temporal patterns of stink bugs (Hemiptera: Pentatomidae) in wheat. Environmental entomology, 39(3), pp.944-955.

Reed, D.D. and Burkhart, H.E., 1985. Spatial autocorrelation of individual tree characteristics in loblolly pine stands. Forest Science, 31(3), pp.575-587.

Rossi, S., Morin, H., Deslauriers, A. and PLOURDE, P.Y., 2011. Predicting xylem phenology in black spruce under climate warming. Global Change Biology, 17(1), pp.614-625.

Ryan, P.A., Lyons, S.A., Alsemgeest, D., Thomas, P., and Kay, B.H. 2004. Spatial statistical analysis of adult mosquito (Diptera: Culicidae) counts: an example using light trap data, in Redland Shire, southeastern Queensland, Australia. J. Med. Entomol. 41(6): 1143-1156.

Smith, P.A., 1994. Autocorrelation in logistic regression modelling of species' distributions. Global ecology and biogeography letters, pp.47-61.

Sokal, R.R., 1977. Clustering and classification: Background and current directions. In Classification and clustering (pp. 1-15). Academic Press.

Sokal, R.R., Oden, N.L. and Thomson, B.A., 1998. Local spatial autocorrelation in biological variables. Biological Journal of the Linnean Society, 65(1), pp.41-62.

Tsuyuki, S., 2008. GIS-based modeling of Javan Hawk-Eagle distribution using logistic and autologistic regression models. Biological Conservation, 141(3), pp.756-769.

Wu, H. and Huffer, F.R.W., 1997. Modelling the distribution of plant species using the autologistic regression model. Environmental and ecological Statistics, 4(1), pp.31-48.
