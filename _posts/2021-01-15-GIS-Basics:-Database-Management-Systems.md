---
title: "GIS Basics: Database Management Systems "
layout: post
---

>> Good to begin well, better to end well.
>> 
>> -- June K. Robinson

I set up a [mind map](https://drive.google.com/file/d/11nuzFqrosP19N0ncjL1-rthJ9jmMqWtB/view?usp=sharing) and wrote detailed [documentation](https://drive.google.com/file/d/1hn2AbcAKBWCZrBU3ng4gLPpaCu2OhDs3/view?usp=sharing) to help myself organize, understand, and memorize knowledge and concepts regarding GIS when preparing for my PhD candidacy exam. 

This is the second part of the doc: **Database Management Systems**.

Database management systems or DBMS for geospatial data is the kernel of a GIS. This is a super big topic, and I will stay here for a while. I will go through the DBMS basics and DBMS development. 
 
## DBMS basics
A DBMS can be understood as a collection of two classes of software: one gets access to the physical data storage; one processes the queries. There are three levels of abstraction of this mechanism: physical level, logical level, and external level. I start with the external level, the most straightforward one. Through an external view, a part of the data depending on the queries or specific application is presented to the end-users. There can be concurrent external views presenting data to multiple end-users. The logical level DBMS defines the database structure, data model, and data constraints, which corresponds to the conceptual design and logical design of a DBMS. The physical level DBMS handles a series of functionaries hidden from the users, like physical data storage, access method, index, query processing, query optimization, and concurrency and recovery. This corresponds to the physical design of a DBMS. 
 
Regarding a spatial DBMS, special consideration is needed because of the special data types. These considerations include but are not limited to: a logical and physical representation of geometric data in the database and the corresponding queries/functions to interact with geometric data. In particular, the geographic data model needs to fit the spatial data characteristics, spatial indices are needed to facilitate spatial queries, and new algorithms are needed to conduct spatial analysis based on spatial indices. Some spatial DBMS are available on the market: ArcInfo, ArcView, Oracle extensions for spatial data, PostgreSQL, etc. Among them, ArcInfo is a hybrid system or a loosely coupled system that separates spatial attributes management from the thematic attributes management. ArcView, Oracle Spatial extensions, and PostgreSQL employ an integrated system, in which geographic information is modeled as relations containing one spatial attribute and several non-spatial attributes. 
 
## Conceptual level development
The DBMS development at the conceptual level is independent of any implementation details. It defines the structure of the information to be stored or managed in this information system, including the data types, inter-relationships between entities or relations, dynamic behavior in operations, and integrity constrain which guarantees the data correctness in the database. Four models are most commonly used in this level of development; they are the ER model, EER model, UML model, and OMT model. Among them, the ER model leads toward relational constructs, while the other three lead toward object-oriented modeling.  

### ER model
ER model means the entity-relational model, which is self-explanatory that the main elements are entities and relations, along with attributes of either entities or relations. Relationships have three types depending on the number of instances of entities involved: one to one, one to many, and many to many. Relations can be optional or mandatory. An involuntary relationship means that it relates an entity type to itself. A ternary relationship relates three different entities. An entity can be a weak or dependent entity, where an instance cannot be identified by merely the entity's identifier. In this case, a parent entity and an identifying relationship are needed, where the identifying relationship can only be one to one or one to many. 
 
### EER model
EER model stands for the extended entity-relational model. The most important part it 'extends' is subtype or super-type. If every occurrence of entity A is an occurrence of entity B, then A is a subtype of B and B is the super-type of A. This is different from the one-to-one relationship which relates two different entity types. A remains the identifying attributes and all relationships of B, and may have more attributes and relations; this characteristic is called attribute inheritance. The process of constructing subtypes is called specialization, and the process of constructing super-types is called generalization. These two processes lead to the same results. A specialization may be disjoint or overlapped, depending on whether the subtypes are independent or not. Specialization can be total or partial, depending on if its subtypes cover all possibilities. The concept of the category is closely related to super-type and subtype, where there are more than one super-type in a relation. A category can also be total or partial. EER model can be used to describe spatial information, for example, entity type point can have subtype end-node and start-node which compose a line segment. 
 
### UML model
The unified modeling language is standard for software design and is also commonly used in database design. The basic elements of the UML model are classes and relations, and classes may have an inheritance as with the EER model. A class has class attributes and class methods defining the behavior of such a class, and its subclasses will inherit all attributes and methods. This is different from the EER model, however, where the EER model only allows specialization or generalization of attributes. There are three types of relations in a UML model: aggregation, association, and generalization. Aggregation describes the relation of component, can be total aggregation and partial aggregation. For example, the relation between a wheel and a car is aggregation. Association describes the relation of internal structure, for instance, the relation between an actor and a film is association. Generalization has the same meaning as in the EER model, describing the relation between the superclass and subclass. Generalization can be disjoint or overlapped. UML model can be used to describe spatial information as well. For example: the class road has attributes name and speed, and has behaviors create and set speed; class expressway is a subclass of class road, inheriting all attributes and relations of class road and having an extra attribute level; class centerline has a one to one relationship with the class road; the class point has an aggregation relationship with class centerline because a centerline consists of vertices (points). 
 
### OMT model
The object modeling technique’s model has three types: object model, dynamic model, and functional model. This is beyond the scope and will not be investigated.

## Logical level development
The development of DBMS at the logical level is to translate the result of conceptual level development to data models depending on the particular DBMS chosen. Three most commonly used DBMS are introduced in detail: relational DBMS, object-orientated DBMS, and object-relational DBMS. Other than these, other alternatives will be briefly introduced including those for managing spatial information or non-spatial information. Some NoSQL methods are included at the end.

### Relational DBMS
In a relational DBMS or RDBMS, the management unit is a relation or table. A relation has tuples or records whose ordering is not significant, and the ordering of tuple columns matters so that they are corresponding to the attributes. Tuples are distinct from each other in a table. In a table, one attribute whose values are unique for each tuple is called a candidate key. Among all candidate keys, one attribute or a combination of more than one candidate key is chosen as the primary key of this relation. A relation can have a foreign key which is the primary key of another table to accelerate join operations between tables. Normal forms are used to facilitate the integrity constraint in a relational database. The first normal form, or 1NF, requires all attributes in a table should be atomic rather than nested. 2NF and 3NF require that all attributes in a table should be fully dependent (no partial dependencies) and directly dependent (no transitive dependencies) on the composite key and primary key, respectively. Relational DBMS have been well developed and commonly used for a long time, while they come across inefficiency when handling spatial data. They sure can handle spatial data but with low power. The main reasons are: 1) the structure of spatial data is more complex, for example, polygons consist of lines that consist of points. This violates the 1NF of RDBMS. 2) Joining tables are needed all the time and this weakens the performance of the database. 3) Spatial data need specialized indices because 2D objects are uneasy to be indexed by linear indices used for non-spatial information. 4) Geometric computation is not possible in a purely relational database. SQL or structured query language is the query language in a relational database. SQL is declarative, meaning users can express the query precisely and get precise query results without having to worry about the mechanism under the hood. It also relies on sound mathematical foundations including relational calculus and relational algebra. As one can imagine, SQL is not efficient to work with spatial data, so that extended SQL is developed and will be discussed later. Furthermore, SQL cannot match other complex programming languages to accomplish operations like recursion.
 
### Object-orientated DBMS
In an object-orientated DBMS or OODBMS, a management unit is an object. An object is either atomic or complex, depending on its structure or the operations that can be performed on it. The state of an object is its total attribute values at a certain time, and the behavior or method of an object is the operations it can perform under certain conditions. A class is a collection of objects sharing the same attributes and behaviors. The set of behaviors of a class of objects is called an interface. There are several features of an OODBMS. First, each object has an identity that is immutable and independent of its attribute values. Second, the internal structure and the implementation of the abstract data type is invisible from the outside world, which is called encapsulation. Third, generalization and specialization are workable in the OODBMS, where a subclass can inherit all attributes and behaviors of its super-class. Hence, a class can play different roles in a different context, which is called polymorphism. Inclusion polymorphism means the situation where an instance of a class can be substituted by an instance of its superclass. A mothed defined on a superclass can be redefined on its sub-class, which is called overriding. A sub-class can also inherit from more than one super-class, and this distinguishes the single inheritance or multiple inheritances. The association helps to model complex internal structure by grouping objects together. Aggregation is a special type of association, which highlights the part-whole association between objects. OQL or object query language is used to query data in the OODBMS, and users are allowed to develop query formulations. 
 
Compared to RDBMS, OODBMS have several benefits: 1) It reduces the complexity of conceptual models because it deals with individual objects. 2) It combats impedance mismatch meaning the gaps between different levels of DBMS development. This is because the object-orientated concept can be employed at each level of the DBMS development, from conceptual to physical. 3) It promotes the reuse of the developed components. 4) It has metaphorical power because of the useful metaphor of objects. However, it suffers from drawbacks: 1) Due to its complex object classes the query optimization is difficult in an OODBMS. 2) Indexing is uneasy to be implemented in an OODBMS because an index is used to access an attribute value, but an object is only accessible via an activating message in the OODBMS context. 3) The transactions are more complex in an OODBMS because of the hierarchical nature of the objects. 
 
### Object-relational DBMS
An object-relational DBMS or ORDBMS handles the objects as an atomic value in relations (tables). ORDBMS can encapsulate functions for objects like in an OODBMS and can support the definition of new data types and new functions on the new data types. This structure is meant for handling spatial data in an RDBMS fashion with modifying the pure relational database as little as possible. The most well-known example of ORDBMS in managing spatial data is PostgreSQL. PostgreSQL defines geometry types such as point, line-string, and polygon, and supports the definition of new geometry types like multi-point and multi-polygon along with new functions on new geometry types. It also supports indices such as B tree, R tree, and generalized search trees or GiST. An extended SQL called pgSQL is available in PostgreSQL to facilitate new data type definition, new function definition, and data queries. The problem of ORDBMS is that it did not solve the impedance mismatch in comparison to OODBMS.
 
### Spatial alternatives
Constraint data models can be used to manage spatial data. Constraint databases extend the relational paradigm to handle infinite relations and can present and manipulate data in arbitrary dimensions in a uniform framework. 
 
### Non-spatial alternatives
Three non-spatial alternative models are introduced briefly here, although they are honestly rare on the market. The hierarchical model organizes data in a tree-like structure with each record is having one parent record and many children. This is an efficient storage structure, but only works for one-to-many relationships and are not expressive enough for modeling everyday phenomena. The network model uses a graph as their schema where relationship types are arcs and object types are nodes. This allows many-to-many relationships, easy accessibility of data, and data integrity. However, the drawbacks are the complexity and inflexibility of the system. The deductive model can make inferences based on the facts and rules stored in the database and has implementations like LDL, Eclipse, and Prolog.
 
### Loosely coupled approach
This has been discussed previously when talking about hybrid architecture. Arc/Info is a typical example of the implementation of this approach, where module Arc is responsible for the spatial information management, and module Info is for the non-spatial or thematic information management. The main drawback of this approach is that when doing a query relating both locations and attributes, the two systems work separately and intersect the results at the end. 
 
### NoSQL DMBS
NoSQL DBMS stands for a broad class of DBMS that is not primarily built on tables or relations and does not use SQL for queries. The appearance of NoSQL is due to the trend of the big data market, semi-structured datasets in high volume, increasing the need for interlinked data, and decoupled architecture. It is featured as availability, correctness, security, and good performance when handling big data by applying techniques such as map-reduce. NoSQL DBMS queries data mainly via three methods: RESTful interface, APIs, or other query languages like SPARQL. There are four main categories of NoSQL DBMS based on the data structure employed. A document store uses a document as the basic unit to store and manage data. A document with a unique key encapsulates and encodes data in standard formats like XML, JSON, BSON, etc., and documents are grouped into collections, then collections are grouped into a database. MongoDB is an example of document-oriented NoSQL DBMS, where BSON is used as the standard document format. MongoDB also supports 2D geospatial indices. A key-value store uses key-value pairs as its basic data model and stores data in a schema-less way. A graph database focuses on the modeling of data interconnectivity. An example of the graph database is Neo4j. A big table can handle semi-structured datasets, where columns are grouped into column families, and column families are then grouped into Access Control Lists or ACL. 

## Physical level development
The physical design of a DBMS is responsible for a series of functionaries hidden from the users, such as physical data storage, access method, index, query processing, query optimization, and concurrency and recovery. Here I focus on the physical data storage, access method, and index, and leave the query processing and query optimization to the topic 'Data manipulation'. I will walk through the basic file organization and access methods and introduce 1D and 2D indices that facilitate the data access. 
 
## File organization basics
So, what is a file? A file consists of inter-related records, and a record consists of fields. This is analogous to the terminologies of the attribute, tuple, and relation in a relational database. Another two important concepts are disk page and disk block. As you may know, the storage in a computer is normally classified as the primary storage (i.e., ROM and RAM) which can be directly manipulated by the CPU and the secondary storage. In the secondary storage media, a file has its records assigned to the disk block(s). Depending on the size of a record, it can be assigned to one disk block, or be spread across several blocks, or several records can be assigned to one disk block. A disk page is just the equivalent of a disk block in the RAM context. 
 
File organization means the physical organization of the records on the secondary storage, the linkage method between blocks of records, and the approach of inserting new records into the storage. There are three main influencing factors of data retrieval performance of an information system: physical placement of data on the disk, index, and access method. When data is stored on the secondary storage media, the typical access time consists of the time of mechanical movement of disk heads to the right disk track (called seek time), the time of rotation of the disk to the right position (called latency), and the time taken for transformation from the disk to the CPU (called CPU transfer time). Thus, the wise physical placement of data on the disk can sure improve the data retrieval performance by decreasing the seek time, although this is not sufficient in more complex situations where appropriate indices come in. For example, an unordered file has a convenient insertion operation, while suffers from an expensive retrieval operation that needs linear research with O(n). The deletion operation of an unordered file can lead to holes on the disk, resulting in the complex new insertion. An ordered file can improve the retrieval operation by adopting the binary search with O(log2n) where less seek time is needed than a linear search. However, the insertion and deletion can still be complex for an ordered file. Another example is hashing, where a hash function is performed on a hash field in a hash file so that the retrieval of a specific record just needs one access to the disk block. A hash function is used to transform the value of the values of a field into the address of the disk block, for example, transforming 'Aug 21, 2013' to '210813'. However, the complexities raise when the disk block overflows, and it is not straightforward to construct an even distribution of records. Plus, one has to know the number of disk blocks to be allocated for storage in advance. 
 
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