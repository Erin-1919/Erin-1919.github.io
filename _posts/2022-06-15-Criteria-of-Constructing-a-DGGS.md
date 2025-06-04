---
title: "Criteria for Constructing a DGGS"
layout: post
---
![monstera](/assets/img/20220615/monstera.jpg)

**In 1994, Michael Goodchild proposed 14 criteria for evaluating DGGS designs. These were refined by Kimerling et al. in 1999. Recognizing that no DGGS can satisfy all criteria perfectly, the Open Geospatial Consortium (OGC) released a formal DGGS standard in 2017 that identifies key design requirements considered achievable and essential. These are summarized below, based on the DGGS Core Conceptual Data Model and Abstract Specification.**

## Global Domain and Area Preservation

A DGGS must fully and uniquely cover the Earth's surface without overlaps or gaps. This guarantees position uniqueness, which is critical for accurate addressing and reliable analytics. This global coverage and uniqueness must be preserved across all resolution levels. Together, these ensure consistent surface area representation, supporting valid spatial aggregation and analysis. This combines Requirements 2, 3, and 5 from the OGC specification.

## Multi-Resolution with Cell Refinement

DGGS are defined by hierarchical tessellations. Each resolution level is produced by subdividing parent cells into child cells. This refinement is described by the system’s aperture. A congruent DGGS ensures that child cells form a complete union of the parent, while an aligned DGGS preserves center alignment between levels. These features enable consistent data aggregation, downsampling, and analysis across scales. This satisfies Requirements 4 and 10.

## Initial Polyhedral Tessellation

DGGS are typically based on tessellations of regular polyhedra—such as the icosahedron, octahedron, hexahedron, dodecahedron, or tetrahedron—mapped to the Earth’s surface. The icosahedron is the most common due to its small face area and near-uniform geometry. Orientation of the polyhedron can vary based on use case, such as placing vertices in oceans or aligning face centers with the poles. The tessellation defines the framework for cell subdivision. This corresponds to Requirement 9.

## Simple Geometry and Equal-Area Cells

Cells must be simple in shape, have well-defined edges and vertices, and enclose a measurable area. Common geometries include triangles, quadrilaterals, and hexagons:

- **Quadrilaterals** are common for hexahedron-based DGGS and work well with existing quadtree algorithms and display systems.
- **Triangles** suit triangle-faced polyhedra but may lead to irregular adjacency and orientation.
- **Hexagons** offer uniform adjacency, high angular resolution, better distance approximation, and minimal tiling error, making them attractive for raster-style analysis.

DGGS must also provide approximately equal-area cells at each resolution level. Equal-area properties ensure fair representation of spatial data and reduce distortion in analyses. While exact equality is mathematically unachievable, acceptable precision must be specified, along with the maximum allowable area variation. Projections such as the Snyder Equal Area projection are often used for area preservation. These characteristics fulfill Requirements 6, 7, and 8.

## Cell Addressing

Each DGGS cell must be uniquely and consistently identified. Indexing supports data integration, query efficiency, and spatial analysis. The OGC does not mandate a specific method, but common approaches include:

- Hierarchical indexing  
- Space-filling curves (e.g., Hilbert, Peano)  
- Coordinate-based systems  
- Encoded address schemes  

This supports Requirements 11 and 12.

## Centroid-Based Spatial Referencing

Each cell must be referenced by its centroid, which represents the geodesic center of its area. Centroids provide a consistent, geometry-independent method for spatial referencing across the entire DGGS domain. This is Requirement 13.

---

**In summary**, the OGC DGGS Abstract Specification does not prescribe a one-size-fits-all system. Instead, it outlines core requirements that allow flexibility in implementation. Trade-offs are often necessary based on application needs. No single DGGS will simultaneously optimize for congruence, alignment, low aperture, and equal-area precision, so design choices must balance practical goals with technical constraints.
