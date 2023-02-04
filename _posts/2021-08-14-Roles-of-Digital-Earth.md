---
title: "Roles of Digital Earth"
layout: post
---
![kuba](/assets/img/20210814/kuba.jpg)

Virtual globe has been found useful in all communities of researchers, educators, and citizens or non-scientists. The roles Digital Earth played have been summarized as five broad categories: mapping and visualization tool, analytical and modeling tool, the underlying basis for other derivative applications, data storage structure, and platform for Volunteered Geographic Information (VGI; [1]). 

## Mapping and Visualization Tool
### Environmental monitoring
The most obvious function of Digital Earth lies in visualization, especially the dynamic, real-time, or multi-scale monitoring of the environmental phenomena and process on the Earth’s surface. Over the decades, governmental departments and organizations have carried out projects based on Digital Earth aimed to enable researchers and citizens better understand environmental issues, relating to sea ice extent in Arctic region [2], oil spill imaging [3], parasitic diseases spreading [4], species habitat distributions [5], etc.

### Interactive visualization
The interactive visualization can be realized by Digital Earth, giving users an opportunity to access, explore and participate the environmental conservation. The example projects include Common Ground [6], Arctic Research Mapping Application [7], Crusta [8], etc.

### Decision-making support
The visualization by Digital Earth not only can deliver the information but also can support decision making in various fields, typically done by overlay the other information layers on the satellite imagery base maps so that area of interests can be identified, upon which necessary decisions can be made. It is particularly useful for natural disaster strategies [9], epidemic management [10], energy utilization [11], and meta-analysis research [12].

### Dissemination of research results
For scientists, visualization by Digital Earth offers a platform to share and communicate their research findings and to attract or educate the public. For example, Yuan et al. [13] developed a new approach to simulate rupture fault displacement during a tsunamigenic earthquake event and integrated their results into Google Earth to supply with the geological context. What is more, the hazards of the tsunami in the Indian Ocean was evaluated and simulated and integrated into the Google Earth context [14]; the latitudinal distributions of species richness for different grass lineages were investigated and mapped by interpolating their model fits onto an equal-area hexagonal grid of the world [15]. 

## Analytical and Modeling Tool
### Basic areal unit
In the biological or ecological fields such as ornithology, agriculture, entomology, and wildlife biology, the DGGS cells, hexagons particularly, have been used as the basic spatial analytical unit because of their equal-area, equal-shape, and seamless coverage properties. For example, in a series of studies on global bird migration, each bird species’ breeding or winter range map polygons were converted to equal-area hexagonal cells for estimating regional assemblages (e.g., [16]), to summarize species richness (e.g., [17]) or to present presences and absences of bird species on a global icosahedron (e.g., [18]). Various studies were then carried out upon this basis to understand seasonal associations between novel climates and bird migratory populations [19], to explain the differences in migratory destinations among bird species [18], and to forecast transatlantic birds’ migration under the global warming context [20]. Except these, hexagonal cells also acted as transitional, analytical units to bridge components of a study (e.g., [21]).

### Data integration
Data integration especially benefits from DGGS, because the information from different sources automatically lined up in DGGS cells which are fixed in area and location. A typical example is that to systematically analyze over 1000 chondrichthyan fishes-sharks, rays, and chimaeras over the global marine area, all species distribution maps were merged into one single shapefile using hexagonal grids as a unified reference frame [22]. 

### Model basis
Global shallow-water models were created on either twisted icosahedron [23, 24] or hexahedron [25-27] based globe, on which many of the problems of stream function-velocity potential form of the shallow water equations associated with the fluid flow on a rotating sphere can be overcome [23, 24]. Other examples included an atmospheric dynamical core model [28] and an ultra-high resolution atmospheric global circulation model [29] built on icosahedron-based spherical geodesic grids, and a vector tile model based on a pole-oriented the quaternary quadrangle mesh DGGS [30, 31]. Peterson also suggested that predictive modeling techniques (e.g., finite element, agent-based, and cellular automaton) can be applied to DGGS because of their cell structure, operations, and data integration characteristics [32].

### Sampling design approach
The equal-area characteristic of DGGS provides the equality of possibility that points within a cell can be chosen as the representatives for the cell [33]. It helps to make a systematical sampling strategy, particularly at a large scale. Gong et al. [34] generated sample points based on a globally systematic unaligned sampling strategy over the Earth’s surface to test the accuracy of their global land-cover maps. Samples were collected by partitioning the entire globe with a hexagonal scheme then randomly assigning samples in each hexagon [34]. The generated random sample points were also used in other studies (e.g., [35, 36]). 

### Common reference frame
DGGS have served as a common reference frame to test and compare results from different studies. To validate the accuracy of the existing global urban maps, the urban area in each tested map was assessed by the DGGS framework which is independent of political boundaries and without the issue of ununiform raster pixel sizes due to geographic projections [37, 38]. To perform a cross-comparison between different datasets for validating coarse-scale remote sensing soil moisture products, those datasets were re-projected to a common, equal-area Icosahedron Snyder Equal Area (ISEA) 4H9 grids as the reference projection [39, 40]. The same grid system has been used as a referenced grid system for the Soil Moisture and Ocean Salinity Mission (SMOS; [41]).

## Underlying Basis for Other Derivative Applications
HEALPix, one of the common DGGSs, has been used as a foundation to create other software or models in the field of astronomy, typically cosmology [42]. The derived software has been used to simulate polarized cosmic microwave background maps and infrared or submm sky, to compute the theoretical spectra of cosmic microwave background anisotropy, and to calculate photon fluxes from dark matter annihilation or decay in galaxy haloes [42].

## Data Storage Structure
SMOS products were provided in the format of ISEA4H9 grids, which has been proved as the best-suited global grid to be used in mapping SMOS imagery among grid systems of Latitude-longitude Universal Transverse Mercator (UTM), Quaternary Triangular Mesh (QTM), ISEA projection, and Equal Area Scalable Earth (EASE; [41]). SMOS products have been used in several studies of biology, ecology, and oceanography (e.g., [43-45]).

## Platform for Volunteered Geographic Information
Volunteered Geographic Information (VGI) has been discussed by Goodchild [1], which includes citizens as sensors in a traditional GIS, potentially enhance people’s understanding of the surface of the Earth with timely, low-cost, and public-accessible sources. Different from the terms “citizen science” or “geo-crowdsourcing”, VGI emphasizes the active mode of human beings who are contributing to the data [46]. These citizen-collected data can help improve, for example, environmental models in terms of validation or predictions, and those VGI platforms can be treated as a part of the Digital Earth infrastructure [46]. De-Longueville et al. [47] proposed an approach to integrate VGI to their designed Digital Earth by Sensor Web Enablement so that citizens played the role of sensors to form the nervous system of the Digital Earth. This concept was applied in the context of a forest fire scenario, where citizens were able to help with up-to-date information collection and eventually decision making. Additionally, citizen-participated urban planning can be realized by Digital Earth using Web Services and Service-Oriented Architecture [48]. In their framework, users can select and compare different urban planning alternatives or solutions in a virtual-globe-based 3D visualization environment [48]. 

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

