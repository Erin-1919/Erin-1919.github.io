---
title: "Why is Hexagon Superior"
layout: post
---
![hex](/assets/img/20230130/hex.jpg)

**The main advantage is their high compactness and uniform adjacency, which is not true for square or triangular grids. This can lead to quite a few concrete merits in statistics, modeling, and analysis.**

## Compactness
One of the most important and straightforward uses of DGGS is to do aggregation statistics because of its consistent cell size and fixed cell locations. From this perspective, hexagons can benefit because distances between every two cells are constantly at a certain level and cell orientation does not alter within a certain area. Think about a use case of point-binning using grid meshes. Hexagons, as the most compact regular polygon that tiles the plane, can minimize the distance between represented points and requires 13% fewer cells in comparison to squares at the same resolution. With the Superior angular resolution, It can solve more different angular relationships between the data points.    

## Uniform adjacency
The first-order neighbors have all same distance from the central cell, and the out neighborhoods are more circular compared to square or triangular meshes. This leads to the fact that hexagonal grid distance can better approximate the Cartesian distance, which makes it a good surrogate. 

## Thus...
From the perspective of spatial operations, hexagonal cells migrate the vagueness of neighborhood definition, so that operations that require consideration of neighboring cells can be distinct and no further consideration of weighing scheme is needed. In hydrological modeling, it can remove the island effect and can better represent the flow width. For image processing algorithms that are radially symmetric, operations on hexagonal grids can be 25-50% more efficient than the square version of those algorithms. 

## By the way...
The Foveal retina, which is the center part of our eyes, is with a hexagonal pattern. When the evolution set out to design a high resolution sampling system for the world, we tiled our eyes with hexagons. Doing this with the Earth is a good idea if we want to the same kind of sampling ourselves. Our brain was also designed to do mapping based on hexagons with different nestings.
