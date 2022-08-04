# Storage in the Cloud

## Google cloud storage

- object storage
- ingestion point for data being moved into the cloud and is frequently the long term storage location of data
- fully manageable, scalable
- Just make objects and the service stores them with high durability and high availability
- use to:
    - serve website
    - store data for archival and disaster recovery
    - or distribute large data objects to your users via direct download
- each object in the cloud storage as a url
- storage objects are immutable
- not a file system
- once data is in cloud storage you can move them onwards to other GCP storage services
- files are organised into buckets
- When you create a bucket you give it a globally unique name. You specify a geographic location where the bucket and its contents are stored and you choose default storage class
- Use Cloud IAM to control access to the buckets
    - access control lists (ACLs - offer finer control, they define who has access to your buckets and objects as well as what level of access they have)
        - Two information:
            - a scope which defines who can perform the specified actions
            - permission which defines what actions can be performed
- Versioning - when turned on, you keep information about modifications, when turned off, the new always overwrites the old
- Life cycle management policies - gets rid of the junk accumulated

![Untitled](Storage%20in%20the%20Cloud%2050bebb43a3c34760aded0c59d0e4e3b0/Untitled.png)

### Cloud storage interactions

- cloud storage lets you choose among four different types of classes:
    - Regional - high performance object storing
        - save data in a specific GCP region
        - cheaper than multi regional
        - offers less redundancy
        - Store data close to your compute engine, virtual machine or Kubernets engine cluster
    - Multi regional - high performance object storing
        - Geo redundant (you pick a road geographical location like the US, EU,Asia and cloud storage stores your data in at least two geographic locations separated by at least 160 km)
        - appropriate to store frequently accessed data (website content, interactive workloads, or data thats part of mobile and gaming applications)
    - Nearline - backup archival
        - low cost
        - high durable for storing infrequently accessed data
        - when you plan to read or modify your data once a month or less on average
    - Coldline - backup archival
        - very low cost, highly durable service for data archiving, online backup and disaster recovery
        - when you plan to access data at most once a year (that is due to slighly lower availability, 90 day minimum storage duration, costs for data ccess and higher per operation costs)
        
        All storage classes incur a cost per gigabyte of data stored per month (nearline also incurs an access fee per gigabyte of data read and coldline storage incurs a higher fee per gigabyte of data read)
        
        Several ways to bring data into cloud storage
        
        ![Untitled](Storage%20in%20the%20Cloud%2050bebb43a3c34760aded0c59d0e4e3b0/Untitled%201.png)
        
        Storage transfer service - when you want to transfer petabytes of data from another cloud provider, another cloud storage or from an GTTPS endpoint
        
        ### Cloud storage works with other GCP services
        
        ![Untitled](Storage%20in%20the%20Cloud%2050bebb43a3c34760aded0c59d0e4e3b0/Untitled%202.png)
        

![Untitled](Storage%20in%20the%20Cloud%2050bebb43a3c34760aded0c59d0e4e3b0/Untitled%203.png)

- accessed using the cloud storage API (milliseconds access time)

## Google cloud Bigtable

- google’s NoSql big database service
- sparsely populated tables that can scale to billions of rows and thousands of columns allowing to store petabytes of data
- you dont have to configure and tune it
- ideal for data that has single lookup key
- you can think of it as persistent hash table
- low latency, high throughput, both read and write
- great for analytical applications
- same API as HBase (native database of Apache Hadoop)
    - enables portability of applications between HBase and Bigtable)
- why Bigtable over HBase?
    - scalability
    - all data is encrypted
    - use IAM permissions to control who has access
- Gmail, search, maps run use Bigtable as database
- Data can be streamed in through a variety of popular stream processing frameworks
    - Cloud Dataflow streaming, Spark Streaming, Storm
- Data can also be written through batch processes like Hadoop map reduce, Dataflow or Spark

![Untitled](Storage%20in%20the%20Cloud%2050bebb43a3c34760aded0c59d0e4e3b0/Untitled%204.png)

## Google cloud SQL and Google Cloud Spanner

- offers MySQL and PostgreSQLBeta databases as a service
- relational database service
- database transactions
- you could also run your own database server inside a compute engine VM which a lot of GCP customers do, but there are some benefits of using Cloud SQL managed service instead
    - Cloud SQL offers replicas, so if outage occurs, cloud SQL can replicate data between multiple zones with automatic failover
    - Cloud SQL helps you backup your data with either on demand or scheduled backups
    - Can scale both vertically and horizontally
    - accesable by other GCP services
- Also contains SQL WorkBench, TOad and other external applications using standard MySQL drivers
- Cloud spanner - if cloud SQL does not ft because you need horizontal scalability
    - horizontal scalable RDBMS
    - offers transactional consistency at a global scale, schemas, SQL and automatic synchronous replication for high availability
    - if you have outgrown any relational database, or you want to sharde your database for throughput high performance, need transactional consistency, global data and strong consistency or just want to consolidate your database
        - financial applications and inventory applications

![Untitled](Storage%20in%20the%20Cloud%2050bebb43a3c34760aded0c59d0e4e3b0/Untitled%205.png)

## Google Cloud Datastore

- another highly scalable NoSQL database
- store structured data from App Engine Apps
- as you would expect from a fully managed service, cloud datastore automatically handles sharding and replication providing you with highly available and durable database that scales automatically to handle load
- unlike Bigtable it also offers transactions that affect multiple database rows
- lets you do SQL like queries
- designed for application backends
- free daily quota

## Comparing storage options

![Untitled](Storage%20in%20the%20Cloud%2050bebb43a3c34760aded0c59d0e4e3b0/Untitled%206.png)

BigQuery 

- sits on the edge between data storing and data processing
- big data analysis and interactive query and capabilities
- not suitable for backend storing