---
title: "Advanced Topics on DGGS"
layout: post
---

**Discrete Global Grid Systems (DGGS) are expanding in both theory and application. This post explores advanced topics in DGGS development, including datacubes, big data integration, sensor networks, and point cloud management.**

## DGGS-Powered Datacubes

According to Purss et al. [1], DGGS and geospatial datacubes are different views of the same foundational concept—**congruent geography** [2]. This means that all layers or themes are represented using the same spatial units, enabling consistent horizontal and vertical analysis.

A datacube built on a DGGS benefits from global consistency, resolution flexibility, and improved integration of multi-source datasets [1]. While early applications (e.g., [3, 4]) show promise, several areas still require deeper exploration:

- Standardizing implementation methods  
- Enhancing support for multi-dimensional arrays  
- Improving data quality and spatio-temporal integrity  
- Optimizing access, querying, and spatial-temporal analytics  
- Developing service interfaces and promoting broad adoption [1, 5–7]

## Big Data Management with DGGS and Cloud Computing

As Earth observation data grows, managing it efficiently is increasingly important. DGGS, when combined with cloud computing, offers a scalable framework for storage and processing [8]. Several national initiatives, such as Open Data Cube [9], use similar principles to support environmental monitoring.

Challenges remain in this integration:

- **Indexing limitations**: Hierarchical and space-filling curve methods are not well suited for parallel or distributed environments [10]  
- **Time dimension**: Temporal partitioning and multi-scale time analysis present new complexities [11]  
- **Model scalability**: Existing Earth observation models require redesign for cloud-native, DGGS-based architectures [8]  
- **Spherical reference systems**: Most cloud analytics platforms still assume a planar system, which does not align with DGGS geometry [8]

## DGGS for Sensor Networks and the Internet of Things (IoT)

The Internet of Things (IoT) connects a vast array of physical and virtual devices. Defined by the ITU [13], IoT enables communication and automation across distributed infrastructures.

DGGS can enhance IoT platforms by:

- Providing a consistent spatial framework  
- Enabling spatial integration across sensor networks  
- Reducing reliance on point-based interpolation  
- Supporting hierarchical aggregation and spatial reasoning [14]

IoT applications on Digital Earth are still emerging, and key research directions include:

1. Discoverability and communication of geospatial data [12]  
2. Enhanced spatial analysis and geospatial object modeling [12]  
3. IoT-assisted decision-making in real-world domains [12]  
4. Development of DGGS-based IoT platforms [14]

## Managing Point Clouds with DGGS

Integrating global point clouds is difficult due to differing reference systems and inconsistent resolution. Recent work has demonstrated the feasibility of extending DGGS into 3D and 4D to handle multi-dimensional point clouds [15].

In this context:

- The third dimension represents elevation above or below the Earth's surface  
- The fourth dimension captures the time of data collection  
- Indexing is implemented via space-filling curves adapted for an ellipsoidal Earth model  
- Visualizations are delivered through web interfaces for exploratory analysis

Future research may focus on new indexing methods, multidimensional querying, dynamic rendering, and global-scale fusion of point cloud datasets.

## References

1. Purss, M., et al. (2019). *Datacubes: a DGGS perspective*. Cartographica, 54(1), 63–71.  
2. Goodchild, M. F. (2018). *Reimagining the history of GIS*. Annals of GIS, 24(1), 1–8.  
3. SEDNA Project: [https://www.sedna-project.eu](https://www.sedna-project.eu)  
4. EO4wildlife: [http://www.eo4wildlife.eu](http://www.eo4wildlife.eu)  
5. Furtado, P., & Baumann, P. (1999). *Storage of multidimensional arrays*. ICDE.  
6. Salehi, M., et al. (2007). *Spatial data cubes integrity constraints*.  
7. Baumann, P., et al. (2018). *Datacubes: space/time analysis-ready data*. In Doellner et al. (Eds.), Springer.  
8. Yao, X., et al. (2019). *Big EO data with cloud computing and DGGS*. Remote Sensing, 12(1).  
9. Mohamed-Ghouse, Z.S., et al. (2020). *Digital Earth in Australia*. In Manual of Digital Earth, Springer.  
10. Mahdavi-Amiri, A., et al. (2015). *A survey of digital earth*. Computers and Graphics, 53, 95–117.  
11. Tong, X., et al. (2019). *Integer coding index for time management*. Data & Knowledge Engineering, 119, 123–138.  
12. Granell, C., et al. (2020). *Internet of Things*. In Manual of Digital Earth.  
13. ITU (2018). *A guide to the Internet of Things infographic*.  
14. Purss, M.B., et al. (2017). *DGGS and IoT*. IGARSS, IEEE.  
15. Sirdeshmukh, N., et al. (2019). *DGGS for point cloud integration*. Cartographica, 54(1), 4–15.

---

_DGGS is not just a spatial reference system. It is a powerful framework for organizing Earth data across platforms, scales, dimensions, and infrastructures. As research continues, DGGS will play a central role in enabling spatial intelligence across technologies._
