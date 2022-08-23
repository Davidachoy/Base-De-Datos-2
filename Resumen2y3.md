David Achoy Yakimova
2020053336
Bases De Datos II GR 1
# Resumen 2 y 3 (R2, R3)
# Bigtable: A Distributed Storage System for Structured Data
## Introduction
Bigtable is a storage system that can reliably scale to petabytes of data and thousands of machines. It has achieved various goals
-  Wide applicability
-  Scalability
-  High performance
-  High availability

Some modern tecnologies that uses Bigtable are: Google Analytics, Google Finance, Orkut, Personalized Search, Writely, and Google Earth.
## Data Model
A Bigtable is a multidimensional sorted map. The map is indexed by a row key, column key, and a timestamp.
#### Rows
Rows key in a tablet are arbitrary strings. Each read or write of data is atomic.
Bigtable stores data in a lexicographic order by row key. Its range is dynamic partition, and its called "tablet". 
#### Column Families
Column keys are called "column Families", usually they are data of the same type. It must be cr created before data can be stored.
The following syntaxis is used in the column: *family:qualifier*

#### Timestamps
Each cell is capable of containing multiple versions, this versions are indexed by timestamp.They can represent real time or assigned by the client.
## API
The Bigtable API is capable of creating and deleting tables and column families.
Client aplications can write or delete data, also look up for individual rows data and iterate over subset of data in tables.
Some features that a bigtable can do are:
- Single-row transactions
- Allows cells to be used as integer counters
- Supports the execution of client-supplied scripts in the address spaces of the servers

## Building Blocks
Bigtable is a combination of other pieces of google infrastructure. 
- It uses the distributed Google File for storing logs and data files.
- Its cluster runs in a shared pool of machines that works with a variety of other distributed applications.
- It depends on a management system that schedule jobs, manage resources and errors, and monitor the machine status.
- Bigtable data is internally stored with the Google SSTable file format.
- It uses a distributed lock service called Chubby.

## Implementation
The Bigtable is compose of three major components:
- A library that is linked into every client
- 1 master server
- Many tablet servers

### Tablet Location
To store a tablet location information we have to use a three-level hierarchy b+ tree.
The first level is a file stored in Chubby and it contains the root tablet, the root tablet contains the location of **METADATA** tablet, and last each METADATA tablet contains the location of user tablets.
### Tablet Assignmen
One tablet server is assigned to each tablet at a time. The master server keep traks of the tablet servers.
Bigtable uses Chubby to keep track of tablet servers
**Falta**
### Tablet Serving
### Compactions
## Refinements
Implementing the components describe in Implementation requires a number of refinements for ensuring high performance, availability, and reliability.This section describes with more details these refinements.
### Locality groups
locality groups are multiple column families together. More effective reads are made possible by separating column families that are not frequently accessed together.
### Compression
Clients can control if they want to compressed the SStabels and witch type of format compresion to use. Its common that the clients use a two-pass custom compression scheme. 
1. The first pass uses Bentley and McIlroy’s scheme
2. The second uses a fast compression algorithm that looks for repetitions

### Caching for read performance
Tablet servers use two levels of caching
1. The Scan Cache (Used for reading the same data repeatedly)
2. The Block Cache (Used for reading data that is close to the data they recently read)

### Bloom filters
### Commit-log implementation
### Speeding up tablet recovery
### Exploiting immutability
## Performance Evaluation
## Real Applications
### Google Analytics
### Google Earth
### Personalized Search
## Lessons
## Related Work
## Conclusions


