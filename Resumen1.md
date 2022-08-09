David Achoy Yakimova
2020053336
Bases De Datos II GR 1
# Resumen 1 (R1)
## Introduction
Data has become one of the most valuable asset a business can have. With data enterprise’s can store important information about his clients, analyze that data and learn new things from it. Nowadays business owners have data warehouses that works on the cloud, so they can analice data that they have been receiving. In the past traditional data warehouse were difficult  to scale, they have large cost for administration and they limit the number of users that can access to the data.
## Introducing Amazon Redshift
In the past business owners only had two options with big data volumens, choosing between slow querys performace or paying for expensive upgrades. **Amazon Redshift** came to change how enterprises think about data warehous. they became low cost systems without compromising performance.This service offers a fast, scalable and fully managage data warehouse solution. It was launch in February 2013 and became one of the fastest growing AWS service.
## Modern Analytics and Data Warehousing Architecture
**dataware house** are optimized for batched write operations and reading high volumnes of data
**OLTP database** are optimized for continous write operations and high volumnes of small read operations
### Analytics Architecture
Analytic pipelines are designed to handle large amounts of data from sources like databe, aplications and devices.

Analytics pipeline has the following stages:
1. Collect data
2. Store the data
3. Process the data
4. Analyze and visualize the data. 

## Data Warehouse Technology Options
### Row-Oriented Database
Row-Oriented Database Store rows in a physical block.These type of Database are better for transactional processing than for analytics. They are limited by de resources available on a machine

Developers use the following techniques for better performance
- Building materialized views
- Creating pre-aggregated rollup tables
- Building indexes on every possible predicate combination
- Implementing data partitioning to leverage partition pruning by query optimizer
- Performing index-based joins

### Column-Oriented Database
Column-Oriented Database organize each column in its own set of physical blocks. this type of database is better for warehouse because they are efficient for read-only queries.



## Amazon Redshift Deep Dive
### Performance
#### High performing hardware
Amazon Redshift offers a high speed performace workload that require large amount of compute capacity.
#### AQUA
Is a distributed and hardware-accelerated cache that enables Amazon Redshift to run up to ten times faster than any other cloud data warehouse.
#### Materialized views
Amazon Redshift materialized views enable to achive faster analytical workloads such as dashboarding, quearies and ELT data processing jobs
### Durability and Availability 
Amazon detects and replace any failed node in the data cluster.
## Operations
### Ideal Usage Patterns
Amazon Redshift is a good service for OLAP. Business use this service for:
- Analyze global sales data for multiple products
- Store historical stock trade data
- Analyze ad impressions and clicks
- Aggregate gaming data
- Analyze social trends

### Anti-Patterns
Amazon Redshift is bad the following usage patterns
- OLTP
- Unstructured data
- BLOB data


