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
A term represents a unique path in the index tree.For specifying the path information we should consider the direction of the edges connecting the nodes of the document tree.

### Bitmaps as Posting List
A postings list captures the document ids of all the documents which contain the given term. this size is measured with the document frequency - the number of documents in the collection. An example, a document id space of 8 bytes allos up to 2**64 documents in a collection

**Partitioning a Postings List** This means that each insertion of a document to DocumentDB is assigned a monotonically increasing document Id.

** Dynamic Encoding of Posting Entries** this is a single partition, each document need a short word of 14 bits.

### Customizing the Index
Developers can customize the indexing policy and can change de following aspects:

- Including/Excluding documents and paths to/from index
- Configuring Various Index Types
- Configuring Index Update Modes

## PHYSICAL INDEX ORGANIZATION
### The ???Write??? Data Structure
index maintenance must be performed with the following constrains:

- Index update performance must be a function of the arrival rate of the index-able paths
- Index update performance must be a function of the arrival rate of the index-able paths.
- Index update cannot assume any path locality among the incoming documents. 
- Each index update should incur minimal read amplification
- Each index update should have the least possible write amplification


### The Bw-Tree for DocumentDB

The Bw-Tree uses free in memory updates and log strugtures for persistence. it uses multicore processors with multi-level memory/cache and flash memory based SSDs with fast reads.


## INSIGHTS FROM THE PRODUCTION WORKLOADS
### Document Frequency Distribution

document frequency distribution for the unique terms universally follow Zipf???s Law

### Query Performance
The query performace is define by the number of false positives in posting for a given term lookup.The highest value of query precision is 1.

### Blind Incremental Updates
Using highly performant index updates with memory and IOPS busget is the key for incremental update access.

