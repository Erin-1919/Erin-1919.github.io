---
title: "Innovation Summit - Talking to the Planet: Natural Language × Digital Earth for Disasters"
layout: post
---

![talking-to-planet](/assets/img/20251031/ogc.jpg)

**At the 2025 Innovation Summit, I co-presented a session with Dr. Steve Liang titled *Talking to the Planet: Natural Language × Digital Earth for Disasters*. We explored how pairing Discrete Global Grid Systems (DGGS) with AI agents can make disaster data more explainable, traceable, and accessible to anyone—even through plain English questions.**

## A Simple Idea

We framed our work around a simple yet powerful question:  
What if we could ask the planet a question in natural language—about floods, fires, earthquakes—and get a trustworthy, auditable answer?

Our response combines DGGS, a spatial framework with equal-area, multi-resolution cells, with a chain of AI agents that interpret user intent, resolve spatial context, and query data sources in a structured, referenceable way.

## From Chaos to Clarity

We began with the motivation: disaster data today is siloed and inconsistent—across formats, projections, semantics, and sources. This "multi-everything" chaos makes it hard to integrate and trust.  

DGGS provides a common reference frame—spatially, temporally, and semantically. We introduced it as a foundation that aligns all data into a shared grid of indexed cells.

## AI Agents and Query Flow

We described a three-stage pipeline to handle natural language inputs:  
**Intent Parser → Geo Resolver → Data Query.**  

The user starts with a plain-English question. The intent parser extracts meaning, the geo resolver maps references to DGGS cells, and the query engine builds DGGS-aware SQL to fetch results—with full traceability to cell IDs and sources.

To bring this idea to life, I demoed our methane emissions prototype. A user asks a simple question like “Where are the methane hotspots in Alberta this month?” and receives a clean, source-linked answer tied to a consistent DGGS grid.

## Engaged Discussion

The room was full and engaged. We received insightful questions around agent orchestration, technical implementation, and future applications. There was strong interest in how this approach might scale across domains like wildfire response, earthquake damage, and climate adaptation planning.

---

**This session marked an exciting step toward more human-centered, explainable access to environmental intelligence. We’re excited to continue advancing the integration of AI agents with Digital Earth infrastructure.**
