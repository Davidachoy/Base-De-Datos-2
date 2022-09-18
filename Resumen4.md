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

Every part of the tree is automatic indixing. Each update makes the tree updates the structure of the index.

There are two ways of mapping a document:

1. forward index mapping, which keeps a map of  (document id, path) tuples.
2.  inverted index mapping, which keeps a map of (path, document id) tuples.


The index tree grows as new documents get added or updated to the collection. Each node of the index tree is an index entry containing the label and position values.

### DocumentDB Queries

Developers can query DocumentDB collections using queries written in SQL and JavaScript. they both are translated and converted to DocumentDB Query IL. This support a list of actions like:

- filters
- projections
- aggregates
- sort
- user defined functions 
- and more

The Query IL is made for taking the best from JSON and JavaScript language inside DocumentDB database engine. 

The unique aspect of DocumentsDb is that they they allow one to refer to properties in JSON documents at any arbitrary depth, including wildcard paths.

## LOGICAL INDEX ORGANIZATION

The index is a union of all the documents and is also represented as a tree. each node of this tree has a list of documents ids corresponding to the documents containing the given label value.

### Directed Paths as Terms
A term represents a unique path in the index tree.

