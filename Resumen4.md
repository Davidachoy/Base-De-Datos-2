David Achoy Yakimova
2020053336
Bases De Datos II GR 1
# Resumen 4

## Introduction
Azure DocumentDB is a Microsoft database service that manages Json files at internet Scale. Apps like Xbox, Skype, Office and MSN has been using DocumentDB since 2012. 
### Overview of the Capabilities
DocumentDB is based on Json data model and JavaScript language directly within databse engine. This features enables the following capabilities for DocumentDB:
1. The query language supports rich relational and hierarchical queries.
2. The database engine is optimized for supporting high volumns of writes.
3. Transactional execution of application logic are made in JavaScript and executed inside the database engine.
4. It offers consistency levels for the developers in different ways to choose from m (strong, bounded-staleness, session and eventual)
5. It offers the users the ability to scale both the
throughput and SSD-backed document storage. This gives the responsability to the developer to manage the resources.
6. it can be Configurable so developers can tradeoff between the storage overhead of index, query consistency and write/query performance using a custom indexing policy.

## SCHEMA AGNOSTIC INDEXING

### No Schema, No Problem!

The schema of a document describes the sturcture and system of the document independent of the document instance.
Json files doesn't have a standard schema. 

### Documents as Trees

DocumentDb represents the Json Documents as trees, this helps  blurring the boundary between the
schema of JSON documents. Each label in a Json becomes a node of the tree. There is a root node which parents the rest of the nodes.

### Index as a Document

Every part of the tree is automatic indixing.