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
A Bloom filter is a feature that filters drastically reduces the number of disk seeks required for read operations.Also, Bloom filters help that most lookups for non-existent rows or columns do not need to touch disk.
### Commit-log implementation
Commit-log implementation adds mutations to a single commit log per tablet server, co-mingling mutations for different tablets in the same physical log file. 
### Exploiting immutability
Various parts of the Bigtable are simplified  by the fact that all of the SSTables that we generate are immutable.
The immutability of SSTables enables the users to split tablets quickly. Instead of generating a new set of
SSTables for each child tablet.
## Performance Evaluation
## Real Applications
On August 2006, there were 388 non-test Bigtable clusters running in various Google machine clusters, with a combined total of about 24,500 tablet servers.
### Google Analytics
Google analytic is a famous application that google has. It is a service that analize traffic patterns in web sites. It gives analytics reports such as visitors per day and page views per URL per day. 
### Google Earth
Google Earth is an app that provides high resolution satellite image of the world. Thi The preprocessing pipeline uses one table to store raw imagery. During preprocessing, the imagery is cleaned
and consolidated into final serving data. This table contains approximately 70 terabytes of data and therefore is
served from disk.

### Personalized Search
Personalized Search is an service that records user queries and clicks across a variety of Google properties such as web search, images, and news. This helps users to revisit their old queries and clicks, and they can ask for personalized search results based on their historical Google patterns.
Personalized Search stores each user’s data in Bigtable.

## Conclusions


