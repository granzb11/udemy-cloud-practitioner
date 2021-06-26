# Database and Analytics

## Amazon Aurora
- Aurora is a propietary technology from AWS (not open sourced)
- PostgreSQL and MySQL are both supported as Aurora DB
- Aurora is "AWS cloud optimized" and claims 5x performance improvement over MySQL on RDS, over 3x the perfoamnce ofPostgres on RDS
- Autora storage automatically grows in increments of 10GB, up to 64TB
- Aurora costs more than RDS (20% more) - but is more efficient
- Not in the free tier

## Amazon ElastiCache Overview
-  The same way RDS  is to get managed Relational Databases...
- ElastiCache is to get managed Redis or Memcached
- Caches are `in-memory databases` with high performance, low latency
- Helps `reduce load off databases for read intensive workloads`
- __If the exam ever asks about in-memory databases, it is ElastiCache__
- AWS takes care of OS maintenance

## DynamoDB Overview
- Fully managed highly avialable with replication across 3 AZ
- __NoSQL database - not a relation database__
- Scales to massive workloads, distributed `"serverless"` database
- Millions of requests per seconds, trillions of row, 100s of TB of storage
- Fast and consistent in performance
- __Single-digit millisecond latency - low latency retrieval__
- Integrated with IAM for security, authorization and administration
- Low cost and auto scaling capabilities

### Type of Data
- DynamoDB is a key/value database

### DynamoDB Accelerator - DAX
- Fully managed `in-memory cache` for DynamoDB
- 10x performance improvement - single-dit millisecond latency to microseconds latency - when accessing your DynamoDB
- Secure, highly scalable and highly available
- Different with ElastiCache at the CCP level: `DAX is only used for and is integrated with DynamoDB`, while ElastiCache can be used for other databases 


## Redshift Overview
- Redshift is based on PostgreSQL, but it’s not used for OLTP
- It’s OLAP – online analytical processing (analytics and data warehousing) 
- Load data once every hour, not every second
- 10x better performance than other data warehouses, scale to PBs of data 
- Columnar storage of data (instead of row based)
- Massively Parallel Query Execution (MPP), highly available
- Pay as you go based on the instances provisioned
- Has a SQL interface for performing the queries
- BI tools such as AWS Quicksight or Tableau integrate with it