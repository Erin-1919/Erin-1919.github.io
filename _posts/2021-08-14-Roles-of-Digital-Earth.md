---
title: "Roles of Digital Earth"
layout: post
---

**The concept of Digital Earth plays multiple roles across research, education, and public engagement. These roles have been broadly categorized into five types: mapping and visualization tool, analytical and modeling tool, underlying basis for derivative applications, data storage structure, and platform for Volunteered Geographic Information (VGI) [1].**

## Mapping and Visualization Tool

### Environmental Monitoring

One of the most prominent uses of Digital Earth is dynamic, real-time, and multi-scale visualization of environmental phenomena. It has been adopted by government organizations and scientific institutions to enhance understanding of environmental challenges, such as monitoring sea ice in the Arctic [2], oil spill imaging [3], disease spread [4], and species habitat distribution [5].

### Interactive Visualization

Digital Earth enables users to explore spatial data interactively, enhancing public participation and environmental awareness. Examples of such applications include Common Ground [6], the Arctic Research Mapping Application [7], and Crusta [8].

### Decision-Making Support

By layering contextual information over satellite imagery or base maps, Digital Earth supports decision-making in areas like disaster response [9], epidemic management [10], energy infrastructure [11], and global meta-analyses [12].

### Dissemination of Research Results

Scientists can use Digital Earth as a platform to communicate findings and educate the public. Yuan et al. [13] simulated fault displacement from a tsunamigenic earthquake and visualized the results in Google Earth. Other studies visualized tsunami hazard zones in the Indian Ocean [14] and interpolated grass lineage richness on a global hexagonal grid [15].

## Analytical and Modeling Tool

### Basic Areal Unit

In ecological fields such as ornithology, agriculture, and wildlife biology, DGGS cells—especially hexagons—serve as equal-area, seamless analytical units. These have been used in bird migration studies to estimate species assemblages [16], summarize species richness [17], map presence or absence globally [18], analyze climate-migration associations [19], explore migration destinations [18], and predict future transatlantic routes under climate change [20]. In some cases, DGGS cells have also functioned as transitional analytical layers within study pipelines [21].

### Data Integration

DGGS greatly facilitates integration of data from various sources by aligning everything within a uniform spatial framework. For example, hexagonal grids were used to combine distribution data for over 1000 chondrichthyan species across global marine environments [22].

### Model Basis

Various geophysical models have been constructed on DGGS grids. These include global shallow-water models on twisted icosahedrons [23, 24] and hexahedrons [25–27], atmospheric models on spherical grids [28, 29], and a vector tile model on pole-oriented quadrangle meshes [30, 31]. Peterson further noted that DGGS is compatible with modeling techniques such as finite element, agent-based, and cellular automata due to its structured cell architecture [32].

### Sampling Design Approach

The equal-area nature of DGGS allows for statistically sound sampling across global domains. Gong et al. [34] partitioned Earth using hexagons and then randomly assigned samples within each cell to test land cover map accuracy. This sampling design was reused in multiple validation studies [35, 36].

### Common Reference Frame

DGGS provides a neutral, consistent frame of reference to compare results across datasets and studies. For instance, urban extent validation has been conducted using DGGS instead of administrative boundaries [37, 38]. Soil moisture datasets were also compared using ISEA 4H9 grids to enable cross-validation for remote sensing products [39, 40], including those from the Soil Moisture and Ocean Salinity (SMOS) Mission [41].

## Underlying Basis for Other Derivative Applications

HEALPix, a widely used DGGS, has served as the basis for numerous cosmological software applications. These include simulations of polarized cosmic microwave background radiation, sky mapping in infrared and submillimeter wavelengths, and calculations of photon flux from dark matter annihilation or decay [42].

## Data Storage Structure

SMOS products are delivered using ISEA 4H9 grids, which have been identified as the most suitable option among several global grid systems including Latitude–Longitude, UTM, QTM, and EASE grids [41]. These gridded data have supported research in biology, ecology, and oceanography [43–45].

## Platform for Volunteered Geographic Information

VGI, introduced by Goodchild [1], describes citizen-contributed geospatial data. It emphasizes active human involvement and complements professional datasets by providing real-time, low-cost observations. De Longueville et al. [47] proposed integrating VGI with Sensor Web Enablement, allowing citizens to act as virtual sensors. In a forest fire scenario, this model enabled timely data reporting for crisis response. Another example demonstrated how Digital Earth supports participatory urban planning using Web Services and Service-Oriented Architecture, allowing users to compare development plans within a 3D globe environment [48].


## Citation 

1.	Goodchild, M.F., Citizens as sensors: the world of volunteered geography. GeoJournal, 2007. 69: p. 211-221.
2.	Ballagh, L.M., M.A. Parsons, and R. Swick, Visualising cryospheric images in a virtual environment: present challenges and future implications. Polar Record, 2007. 43(4): p. 305-310.
3.	Bradley, E.S., et al., Google Earth and Google Fusion Tables in support of time-critical collaboration: mapping the deepwater horizon oil spill with the AVIRIS airborne spectrometer. Earth Science Informatics, 2011. 4(4): p. 169-179.
4.	Stensgaard, A.-S., et al., Virtual globes and geospatial health: the potential of new tools in the management and control of vector-borne diseases. Geospatial Health, 2009. 3(2): p. 127-141.
5.	Olea, P.P. and P. Mateo-Tomas, Assessing species habitat using Google Street View: a case study of cliff-nesting vultures. PLOS One, 2013. 8(1): p. e54582.
6.	Jankowski, P., M.-H. Tsou, and R.D. Wright, Applying internet geographic information system for water quality monitoring. Geography Compass, 2007. 1/6: p. 1315-1337.
7.	Walker Johnson, G., et al., Development of the Arctic Research Mapping Application (ARMAP): interoperability challenges and solutions. Computers & Geosciences, 2011. 37(11): p. 1735-1742.
8.	Bernardin, T., et al., Crusta: a new virtual globe for real-time visualization of sub-meter digital topography at planetary scales. Computers & Geosciences, 2010. 37(1): p. 75-85.
9.	Brice, T. and A. Foster. The application of virtual globe software in forecasting flash flooding of low water crossing. in Proceeding of the 25th Conference on International Interactive Information and Processing Systems (IIPS) for Meteorology, Oceanography, and Hydrology. 2009. Phoenix, Arizona, USA.
10.	Chang, A.Y., et al., Combining Google Earth and GIS mapping technologies in a dengue surveillance system for developing countries. Int J Health Geogr, 2009. 8(49): p. 11.
11.	Doyle, W. and J. Pearce, Utilization of virtual globes for open source industrial symbiosis. Open Environmental Sciences, 2009. 3: p. 88-96.
12.	Rodrigues, A.S., et al., Complete, accurate, mammalian phylogenies aid conservation planning, but not much. Philos Trans R Soc Lond B Biol Sci, 2011. 366(1578): p. 2652-60.
13.	Yuan, X., et al. Tsunami and earthquake visualization inspired by light interference. in Proceeding of IEEE Visualizatoin. 2006. IEEE.
14.	Zhang, H., et al., Modeling and visualization of tsunamis. Pure and Applied Geophysics, 2008. 165(3-4): p. 475-496.
15.	Visser, V., et al., Mechanisms driving an unusual latitudinal diversity gradient for grasses. Global Ecology and Biogeography, 2014. 23(1): p. 61-75.
16.	La-Sorte, F.A., et al., The phylogenetic and functional diversity of regional breeding bird assemblages is reduced and constricted through urbanization. Diversity and Distributions, 2018. 24(7): p. 928-938.
17.	La Sorte, F.A., D. Fink, and A. Johnston, Time of emergence of novel climates for North American migratory bird populations. Ecography, 2019. 42(6): p. 1079-1091.
18.	Somveille, M., A. Manica, and A.S.L. Rodrigues, Where the wild birds go: explaining the differences in migratory destinations across terrestrial bird species. Ecography, 2018. 42(2): p. 225-236.
19.	La-Sorte, F.A., D. Fink, and A. Johnston, Seasonal associations with novel climates for North American migratory bird populations. Ecol Lett, 2018. 21(6): p. 845-856.
20.	La-Sorte, F.A. and D. Fink, Projected changes in prevailing winds for transatlantic migratory birds under global warming. J Anim Ecol, 2017. 86(2): p. 273-284.
21.	Robeson, S.M., Trends in time-varying percentiles of daily minimum and maximum temperature over North America. Geophysical Research Letters, 2004. 31(4).
22.	Dulvy, N.K., et al., Extinction risk and conservation of the world's sharks and rays. Elife, 2014. 3(e00590).
23.	Heikes, R. and D.A. Randall, Numerical integration of the shallow-water equations on a twisted Icosahedral grid. Part I: basic design and results of tests. Monthly Weather Review, 1995. 123: p. 1862-1880.
24.	Heikes, R. and D.A. Randall, Numerical integration of the shallow-water equations on a twisted Icosahedral grid. Part II: a detailed description of the grid and an analysis of numerical accuracy. Monthly Weather Review, 1995. 123: p. 1881-1887.
25.	Rancic, M., R.J. Purser, and F. Mesinger, A global shallow-water model using an expanded spherical cube: Gnomonic versus conformal coordinates. Q. J. R. Meteorol. Soc., 1996. 122: p. 959-982.
26.	Nair, R.D., S.J. Thomas, and R.D. Loft, A discontinuous Galerkin global shallow water model. Monthly Weather Review, 2004. 133: p. 876-888.
27.	Putman, W.M. and S.-J. Lin, Finite-volume transport on various cubed-sphere grids. Journal of Computational Physics, 2007. 227(1): p. 55-78.
28.	Ringler, T.D., R.P. Heikes, and D.A. Randall, Modeling the atmospheric general circulation using a spherical geodesic grid: a new class of dynamical cores. Monthly Weather Review, 2000. 128: p. 2471-2490.
29.	Satoh, M., et al., Nonhydrostatic icosahedral atmospheric model (NICAM) for global cloud resolving simulations. Journal of Computational Physics, 2008. 227(7): p. 3486-3514.
30.	Zhou, M., J. Chen, and J. Gong, A pole-orienteddiscreteglobalgridsystem: quaternary quadrangle mesh. Computers & Geosciences, 2013. 61: p. 133-143.
31.	Zhou, M., J. Chen, and J. Gong, A virtual globe-based vector data model: quaternary quadrangle vector tile model. International Journal of Digital Earth, 2016. 9(3): p. 230-251.
32.	Peterson, P., Discrete global grid systems, in The International Encyclopedia of Geography., D. Richardson, et al., Editors. 2016, John Wiley & Sons, Ltd.: Chichester, UK.
33.	Alderson, T., et al., Digital earth platforms, in Manual of digital earth, H. Guo, M. Goodchild, and A. Annoni, Editors. 2020, Springer: Singapore. p. 25-54.
34.	Gong, P., et al., Finer resolution observation and monitoring of global land cover: first mapping results with Landsat TM and ETM+ data. International Journal of Remote Sensing, 2013. 34(7): p. 2607-2654.
35.	Lu, M., et al., A synergy cropland of China by fusing multiple existing maps and statistics. Sensors (Basel), 2017. 17(7).
36.	Chen, D., et al., Comparison of two synergy approaches for hybrid cropland mapping. Remote Sensing, 2019. 11(3).
37.	Potere, D., et al., Mapping urban areas on a global scale: which of the eight maps now available is more accurate? International Journal of Remote Sensing, 2009. 30(24): p. 6531-6558.
38.	Potere, D. and A. Schneider, A critical look at representations of urban areas in global maps. GeoJournal, 2007. 69(1-2): p. 55-80.
39.	Loew, A., T. Holmes, and R. de Jeu, The European heat wave 2003: early indicators from multisensoral microwave remote sensing? Journal of Geophysical Research, 2009. 114(D5).
40.	Loew, A. and F. Schlenz, A dynamic approach for evaluating coarse scale satellite soil moisture products. Hydrology and Earth System Sciences, 2011. 15(1): p. 75-90.
41.	Martin Suess, P.M. Processing of SMOS level 1C data onto a discrete global grid. in IEEE International Geoscience and Remote Sensing Symposium (IGARSS 2004). 2004. Anchorage, Alaska, USA.
42.	JPL. HEALPix resources. 2018  [cited 2019 Nov. 25]; Available from: https://healpix.sourceforge.io/resources.php.
43.	Rodríguez-Fernández, N.J., et al., An evaluation of SMOS L-band vegetation optical depth (L-VOD) data sets: high sensitivity of L-VOD to above-ground biomass in Africa. Biogeosciences, 2018. 15(14): p. 4627-4645.
44.	Huntemann, M., et al., Empirical sea ice thickness retrieval during the freeze-up period from SMOS high incident angle observations. The Cryosphere, 2014. 8(2): p. 439-451.
45.	Munoz Sabater, J., A. Fouilloux, and P. de Rosnay, Technical implementation of SMOS data in the ECMWF integrated forecasting system. IEEE Geoscience and Remote Sensing Letters, 2012. 9(2): p. 252-256.
46.	Brovelli, M.A., et al., Citizen Science in Support of Digital Earth, in Manual of Digital Earth. 2020. p. 593-622.
47.	De-Longueville, B., et al., Digital earth's nervous system for crisis events: real-time sensor web enablement of volunteered geographic information. International Journal of Digital Earth, 2010. 3(3): p. 242-259.
48.	Wu, H., Z. He, and J. Gong, A virtual globe-based 3D visualization and interactive framework for public participation in urban planning processes. Computers, Environment and Urban Systems, 2010. 34(4): p. 291-298.

---

_Digital Earth continues to serve as a versatile, scalable, and integrative platform that supports everything from scientific research and education to public participation and global policy-making._

