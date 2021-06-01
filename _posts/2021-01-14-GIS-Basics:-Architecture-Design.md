---
title: "GIS Basics: Architecture Design"
layout: post
---

>> Good to begin well, better to end well.
>> 
>> -- June K. Robinson

I set up a [mind map](https://drive.google.com/file/d/11nuzFqrosP19N0ncjL1-rthJ9jmMqWtB/view?usp=sharing) and wrote detailed [documentation](https://drive.google.com/file/d/1hn2AbcAKBWCZrBU3ng4gLPpaCu2OhDs3/view?usp=sharing) to help myself organize, understand, and memorize knowledge and concepts regarding GIS when preparing for my PhD candidacy exam. 

This is the first part of the doc: **Architecture Design**.

This section is about architecture design, generally for all information systems. Two features are essential for a modern information system: interoperability and modularity.
 
## Interoperability
Interoperability is the ability of two or more information systems to communicate. The communication includes but is not limited to data transformation and processing capabilities. If data transformation is the primary task between two systems, then this is called data-oriented interoperability, which is asynchronous in most cases. On the other hand, if sharing the processing capabilities is the primary task, then it needs processing-oriented interoperability, which has to be synchronous. Two main barriers exist during the implementation of interoperability: syntactic heterogeneity and semantic heterogeneity. Syntactic heterogeneity results from different original data formats, models, storage media, etc. which are essentially technical issues. Semantic heterogeneity is due to an incompatible understanding of the synonymy and homonymy in individual systems. To conquer the syntactic heterogeneity, a compatible transfer format is needed between different information systems, here come a bunch of standards, either de jure or de facto, such as the neutral transfer format or NTF, shapefile format, and XML. Semantic heterogeneity can be addressed by compensating a data dictionary. 
 
## Modularity
Modularity is the extent to which an information system can be constructed from individual software units with standardized functions. This is an important feature when setting up a composable architecture.

Here we go through four types of architecture design of an information system: hybrid architecture, integrated architecture, composable architecture, and distributed component architecture. 
 
## Hybrid architecture
It uses a data model so-called the geo-relational model, which was used by ArcInfo. It has two main modules: the spatial management module which handles spatial information, and the non-spatial management module which handles thematic information. These two modules function independently, linked by the unique identifier of each spatial object.
 
## Integrated architecture
Under this architecture, spatial and thematic information is stored in a single database, which can be applied in both object-orientated databases and object-relational databases. An object-orientated database is highly modularized and may suffer from high complexity. This topic will be revisited later when discussing DBMS. Object-relational databases are a hybrid of traditional relational databases and object-orientated databases. Oracle Spatial and PostgreSQL extend their relational DBMS by supporting new spatial data types along with new methods. They also support specialized indexing mechanisms like the z-ordering tree and R tree. 
 
## Composable architecture
This architecture is self-explanatory -- the system is built from different software components, like data storage component, user interface component, network analysis component, a digital communication component, to name a few. The process of building a system from different software components is called mage-programming.
 
## Distributed component architecture
A distributed system is a collection of multiple information systems that are connected via computer networks and simultaneously cooperate to complete a computing task. The high-level distributed systems have three general types: mainframe network architecture, peer-to-peer architecture, and client-server architecture. Mainframe network is a centralized frame, peer-to-peer network is a decentralized frame, while client-server architecture is an intermediate one conducting communication via a request-response protocol, where an information system can be a server, a client, or both a server and client at the same time under a multi-tier client-server architecture. Different from the mainframe network, here in a client-server system, a client can consume services from multiple servers. Depending on where the main computing capability lies, a distributed system can employ either a server-side strategy or a client-side strategy. A generalized distributed component system should have the following parts: interface, registry, and standard protocol. Web services are distributed component systems using XML (and XML vocabularies) as a standard for communication between components. Web services are independent of operating systems and programming languages. 


**Main references**

Linder, W., 2009. Digital photogrammetry, Berlin: Springer.
Rigaux et al., 2002. Spatial databases: with application to GIS, San Francisco: Morgan Kaufmann Publishers.

Stefanakis, E., 2014. Geographic Databases and Information Systems, North Charleston, SC: CreateSpace Independent Publishing Platform.
Stefanakis, E., 2015. Web Mapping and Geospatial Web Services: An Introduction, North Charleston, SC: CreateSpace Independent Publishing Platform.

Tomlin, C.D., 1990. Geographic information systems and cartographic modeling, Englewood Cliffs, N.J.: Prentice-Hall.

Worboys, M. and Duckham, M., 2004. GIS: a computing perspective, Boca Raton: CRC Press.

**Supplement course notes**

UNB GGE 4423 Advanced GIS taught by Dr. Emmanuel Stefanakis

UofC ENGO 645 Spatial Databases and Data Mining taught by Dr. Emmanuel Stefanakis
