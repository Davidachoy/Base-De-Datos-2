David Achoy Yakimova 

2020053336 

Bases De Datos II GR 1

### Resumen 5 y 6

# Spanner: Becoming a SQL System

# ABSTRACT
Spanner is a globally-distributed data management system that backs hundreds of mission-critical services at Google

# INTRODUCTION

When Googles Spanner started they offerd multi-row transactions, external consistency and transparent failover across datacenters. Over the past 7 years they have been involving into a relational database system.
 
 
 A  motivation for the evolution of a more “databaselike” system was driven by the experiences of Google developers trying to build on previous “key-value” storage systems. 

The Spanner query processor implements a dialect of SQL, called Standard SQL, that is shared by several query subsystems. 


# BACKGROUND.

Spanner is a sharded, geo-replicated relational database system.

Spanner’s transactions use a replicated write-ahead redo log, and the Paxos consensus algorithm is used to get replicas to agree on the contents of each log entry.

# QUERY DISTRIBUTION

Spanners distributed query processor is capable of executing code in parallel on multiple machines hosting the data to serve both online and long running queries.

## Distributed query compilation
The Spanner SQL query compiler builds a relational algebra operator tree and optimize it using equivalent rewrites.


**Distributed Union** t is used to ship a subquery to each shard of the underlying persistent or temporary data, and to concatenate the results.

##  Distributed Execution

Distributed Union minimizes latency by using the Spanner coprocessor framework to route a subquery request addressed to a shard to one of the nearest replicas that can serve the request.   

## Distributed joins
Its primary use case is to join a secondary index and its independently distributed base table; it is also used for executing Inner/Left/Semi-joins with predicates involving the keys of the remote table.

## Query distribution APIs
Spanner exposes two kinds of APIs for issuing queries and consuming results.


The single-consumer API is used when a single client process consumes the results of a query. The parallel-consumer API is used for consuming query results in parallel from multiple processes usually running on multiple machines. 

# QUERY RANGE EXTRACTION

## Problem statement
Query range extraction refers to the process of analyzing a query and determining what portions of tables are referenced by the query. The referenced row ranges are expressed as intervals of primary key values.

- Distribution range extraction: Knowing what table shards are referenced by the query is essential for routing the query to the servers hosting those shards.
- Seek range extraction: Once the query arrives at a Spanner server, we figure out what fragments of the relevant shard to read from the underlying storage stack. 
- Lock range extraction: In this case, the extracted key ranges determine what fragments of the table are to be locked (for pessimistic transaction concurrency), or checked for potential pending modifications (for snapshot transactions). 

## Compile-time rewriting
Our implementation of range extraction in Spanner relies on two main techniques: At compile time, we normalize and rewrite a filtered scan expression into a tree of correlated self-joins that extract the ranges for successive key columns. . At runtime, we use a special data structure called a filter tree for both computing the ranges via bottom-up interval arithmetic and for efficient evaluation of postfiltering conditions.
## Filter tree

# QUERY RESTARTS

## Usage scenarios and benefits

## Contract and requirements

#  COMMON SQL DIALECT

# BLOCKWISE-COLUMNAR STORAGE

# CONCLUSIONS 















