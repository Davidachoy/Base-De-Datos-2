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

## Query distribution APIs

# QUERY RANGE EXTRACTION

## Problem statement

## Compile-time rewriting

## Filter tree

# QUERY RESTARTS

## Usage scenarios and benefits

## Contract and requirements

#  COMMON SQL DIALECT

# BLOCKWISE-COLUMNAR STORAGE

# CONCLUSIONS 















