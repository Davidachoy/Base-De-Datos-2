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
The filter tree is a runtime data structure we developed that is simultaneously used for extracting the key ranges via bottom-up intersection / union of intervals, and for post-filtering the rows emitted by the correlated self-joins.
# QUERY RESTARTS
Spanner automatically compensates for failures, resharding, and binary rollouts, affecting request latencies in a minimal way. 
## Usage scenarios and benefits
**Hiding transient failures**. Spanner fully hides transient failures during query execution. This is unlike most other distributed query processors that hide some transient failures but not necessarily all. This means that a snapshot transaction will never return an error on which the client needs to retry.


**Simpler programming model: no retry loops** Spanner users are encouraged to set realistic request deadlines and do not need to write retry loops around snapshot transactions and standalone read-only queries.


**Streaming pagination through query results** Spanner enables efficient use of long-running queries in-stead of paging queries. Client code may stop consuming query results for prolonged periods of time (respecting the request deadline) without hogging server resources


**Improved tail latency for online requests** Spanner’s ability to hide transient failures and to redo minimal amount of work when restarting after a failure helps decrease tail latency for online requests. 

**Forward progress for long-running queries**. For long-running queries where the total running time of the query is comparable to mean time to failure it is important to have execution environment that ensures forward progress in case of transient failures.

**Recurrent rolling upgrades** f Spanner development and the ability to deploy bug fixes quickly. Support for queryrestarts complements other resumable operations like schema upgrades and online index building, and allows the Spanner team to deploy new server versions regularly, without significantly affecting request latency and system load.


**Simpler Spanner internal error handling** . As Spanner uses restartable RPCs not only for client-server calls but also for internalserver-server calls, it simplified the architecture in regards to failure handling. Whenever a server cannot execute a request, whether it is a server-wide reason such as memory or CPU overuse, or related to a problematic shard or a dependent service failure.

## Contract and requirements
To support restarts Spanner extended its RPC mechanism with an additional parameter, a restart token. Restart tokens accompany all query results, sent in batches, one restart token per batch.

**Dynamic resharding**. Spanner uses query restarts to continue execution when a server loses ownership of a shard or boundaries of
a shard change.

**Non-determinism**. Many opportunities for improving query performance in a distributed environment present sources of nondeterministic execution, which causes result rows to be returned in some non-repeatable order.
#  COMMON SQL DIALECT
Spanner’s SQL engine shares a common SQL dialect, called “Standard SQL”, 
# BLOCKWISE-COLUMNAR STORAGE
Spanner originally used significant parts of the Bigtable code
base, in particular the on-disk data format and block cache. This was a good decision at the time because it allowed effort and innovation to be focused on distribution, replication, and scaling. The SSTable (sorted string table) data format inherited from Bigtable is optimized for schemaless NoSQL data consisting primarily of large strings. 















