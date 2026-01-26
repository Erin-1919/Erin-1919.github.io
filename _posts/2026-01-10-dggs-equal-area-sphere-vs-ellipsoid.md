---
title: "Spherical vs Ellipsoidal 'Equal-Area' in Mainstream DGGS Libraries"
layout: post
---

**This post summarizes how major DGGS libraries interpret and implement the “equal-area” property, focusing on the difference between spherical and ellipsoidal reference surfaces.**

## 1. Introduction

Discrete Global Grid Systems (DGGS) provide a hierarchical spatial indexing and tessellation framework for representing the Earth as a set of discrete cells. They are widely used for global aggregation, spatial statistics, resampling, and multi-resolution analysis.

Many modern DGGS implementations accept and return latitude/longitude coordinates in the familiar GIS form (commonly WGS84 geodetic latitude and longitude). However, the mathematical surface on which the grid is actually defined is often not the WGS84 reference ellipsoid. This creates a common source of confusion: when a DGGS is described as “equal-area”, what surface is that equal-area property referring to?

This report clarifies the reference surface assumptions behind mainstream DGGS-like libraries, and explains what “equal-area” means in spherical vs ellipsoidal terms.

## 2. Reference Surface Models in Mainstream DGGS Libraries

### 2.1 Sphere-based DGGS frameworks

Most widely used DGGS or DGGS-like libraries are fundamentally defined on a **sphere** (often a unit sphere), even if they take input/output in a WGS84 latitude/longitude format.

Typical examples include:

* **Uber H3**: hierarchical icosahedron-based hexagon/pentagon system built for a spherical Earth approximation.
* **Google S2 Geometry**: hierarchical cell system using a cube mapped to a sphere (unit sphere geometry).
* **HEALPix**: equal-area pixelization originally designed for the celestial sphere.
* **rHEALPix**: Earth-adapted hierarchical equal-area grid derived from HEALPix logic.
* **ISEA family (e.g., DGGRID implementations)**: based on the Icosahedral Snyder Equal Area concept, which is primarily spherical in formulation.

These frameworks are best understood as **spherical DGGS**, not ellipsoidal DGGS.

### 2.2 WGS84 latitude/longitude usage: what it really means

When these libraries accept “WGS84 lat/lon”, they usually do not run a full ellipsoid-aware geodetic computation internally.

Instead, they treat your latitude and longitude values as:

* **spherical angular coordinates**, and
* immediately convert them into a vector on a unit sphere.

A common internal operation is:

* interpret (lat, lon) as angles on a sphere
* map to 3D Cartesian coordinates (unit sphere point)
* perform indexing / cell geometry operations in spherical space

In other words:

* input/output uses familiar WGS84-like coordinates,
* but the grid logic is spherical.

This is usually sufficient for spatial indexing and aggregation, but it is not equivalent to an ellipsoid-native grid.

## 3. What “Equal Area” Means in DGGS

### 3.1 Equal-area property is always relative to a surface

A key principle is:

**A grid can only be “equal-area” with respect to the surface it is defined on.**

So for a DGGS described as equal-area (for example, ISEA-family grids, HEALPix, rHEALPix), the statement “equal-area” typically means:

All DGGS cells have equal area on the **sphere** used by that DGGS definition.

This does not automatically mean those cell footprints will have equal area when interpreted on the WGS84 ellipsoid.

### 3.2 Face area vs area on the Earth surface

Many DGGS frameworks begin from a polyhedron representation (e.g., icosahedron, cube) and define a mapping between:

* coordinates on the polyhedron faces (a “parametric domain”), and
* the Earth surface representation (usually a sphere).

When the mapping is equal-area:

* equal face-domain areas correspond to equal surface areas on the sphere.

So it is correct to say:

Equal-area DGGS implies “cells are equal area across the globe” **on the spherical surface**.

But it is not required (and usually not true) that:

* the face area itself equals Earth surface area in a literal geometric sense without projection mathematics.

The equal-area property is enforced by the chosen projection/mapping relationship.

## 4. Why Spherical Equal-Area is Not the Same as Ellipsoidal Equal-Area

The Earth is better approximated by an oblate spheroid (ellipsoid), and WGS84 is the standard reference ellipsoid used in most GIS systems.

On an ellipsoid, the local surface area element depends on latitude differently than on a sphere. This means:

* a cell that has exactly equal area on the sphere
* will generally not have exactly equal area when its footprint is interpreted on the ellipsoid

Therefore:

Spherical equal-area grids are not strictly equal-area on the ellipsoid.

This is not a flaw; it is simply a consequence of using different reference surfaces.

## 5. Can a Platonic-Solid DGGS Be Made Truly Equal-Area on WGS84?

### 5.1 Conceptual approach: use an authalic sphere transform

In principle, you *can* design a DGGS such that cells are equal-area on the WGS84 ellipsoid, but you need additional math beyond what most mainstream libraries implement today.

A common concept is:

1. Treat WGS84 as the “true” surface of interest.
2. Convert between WGS84 ellipsoid and an **authalic sphere** using an area-preserving relationship.
3. Define and manage the DGGS geometry on that authalic sphere.
4. Map results back to WGS84 geodetic lat/lon.

If the ellipsoid-to-authalic-sphere mapping is truly area-preserving, and the DGGS is equal-area on that sphere, then the cells can be made equal-area relative to the ellipsoid surface.

### 5.2 Practical difficulty

While feasible in theory, implementing a robust ellipsoid-equal-area DGGS is challenging in practice because the system must remain:

* globally seamless
* hierarchical across refinements
* invertible and stable
* efficient for indexing and geometry
* interoperable with GIS formats

This is why most common DGGS libraries use spherical reference surfaces. It provides simplicity, speed, and clean global geometry, at the cost of small ellipsoid-vs-sphere mismatch.

## 6. Conclusions

1. Most mainstream DGGS alternatives (H3, S2, ISEA/DGGRID, HEALPix, rHEALPix) are fundamentally **sphere-based**, even when using WGS84-like coordinate input/output.

2. “Equal-area DGGS” typically means **equal-area on a spherical surface**, not the WGS84 ellipsoid.

3. Ellipsoidal-equal-area DGGS is possible in theory but complex in practice. Most current libraries opt for the spherical simplification.

