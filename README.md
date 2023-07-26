## Introduction to Big Data

- Small data: mostly structured (not used much nowadays)
- 90% of data is unstructured (Big data)
- Structured data is generally of range - MB, GB, TB.
- Big data is stored in PB, EB, ZB ...
- Small data increases gradually (moderate or small)
- Big data increases exponentially (on daily basis, huge amount of data is being generated)
- Small data is stored centrally.
- Big data is distributed.
- Structured data is stored using SQL server, Oracle.
- Big data is stored using Hadoop, Spark.

## Introduction to Hadoop

- Types of data - images, text, videos.
- Size of data after the internet increased drastically.
- Doug cutting - father of hadoop/ big data - founded hadoop in 2002.
- Hadoop was declared open source by Yahoo in 2012.
- Hadoop is an open source framework that allows us to store and process large data sets in a parallel and distributed manner.
- Hadoop was written in Java.
- Main components - HDFS (Hadoop distributed file system), Map reduce.
- Hdfs divides data into chunks and stores in a distributed manner.
- For example: 1280 MB file data is divided into 128 MB and stored on different nodes.
- Data is stored in data node.
- Name node manages the meta data.
- Hdfs replicates data into multiple data blocks (maintains 2 to 3 copies).
- MapReduce - processing element of hadoop.
- MapReduce converts data into key-value pairs.
- Uses divide and conquer approach.

## What is HDFS?

- Ensures efficient storage.
- Hierarchical architecture
- Based on local file system
- Designed for huge amount of data
- Can be deployed on the existing file system/ devices. Thus making it cost effective.
- Components: Namenode (master node) and datanode.
- Divides a file into parts.
- Metadata is stored in namespace in name node.
- Data is replicated to multiple nodes (fault tolerance).
- Data nodes are stored in racks.
- If a data is stored inside a datanode. Then this data node is stored in a rack. The data will also be replicated on another data node. This data node will not be stored in the same rack because, if the rack itself gets corrupted or down, then the data might be lost. This concept is called as Rack awareness.
- While fetching data, hdfs tries to fetch it from the nearest rack. Original data is kept locally.
- Components of name node: FsImage, EditLogs.
- FsImage: Image/ Snapshot of Hdfs.
- EditLogs: log file of every action.
- Secondary name node: Updates FsImage. It merges FsImage and EditLogs file. This is called checkpointing.
- Heartbeat: datanode sends heartbeat signal every 3 seconds to name node, indicating that it is alive.
- When client tries to access data, the request goes to the namenode. The namenode identifies where the data is on the data node through metadata information. Then returns the address where data is stored, to the client.
- Reads are easy/ fast. Writes are difficult. Because to write on one data node, we also need to replicate it to other data nodes as well.

![image](https://github.com/Adityasr30/BigData/assets/86728825/b80de135-85d2-457c-bdea-07a645c2f5ef)

## What is MapReduce?

- Processing unit
- Two tasks: Map and reduce
- Uses divide and conquer approach
- Mapper: converts data into key-value pairs
- Daemons: Job tracker, task tracker
- Job tracker: schedule jobs, provides resources, acts as OS. (Master daemon)
- Task tracker: executes tasks. (Slave)
- MapReduce tries data close to the processing unit. In other words task tracker is kept on data node.
- To reduce delay, data is kept locally.
- MapReduce steps:
  1. Input
  2. Splitting
  3. Mapping
  4. Shuffling
  5. Reducing

![image](https://github.com/Adityasr30/BigData/assets/86728825/23fbd29e-27bb-49d7-a32c-d222775250de)

Word count example

![image](https://github.com/Adityasr30/BigData/assets/86728825/0c8838c6-3229-4c72-9cf7-bc459d6335ca)

## Hadoop Deployement Modes

- Standalone mode
  - All hadoop service daemons run in a single JVM
  - Suitable for test and development
  - No replication of data

![image](https://github.com/Adityasr30/BigData/assets/86728825/ef9fbbfd-fdc7-4fc3-9da2-9c7240e1fe10)

- Pseudo-distributed mode
  - Simulates distributed environment on a single machine.
  - Each hadoop service daemon runs in its own JVM.
  - Appropriate for quality assurance, test and development.
  - Default replication factor = 1

![image](https://github.com/Adityasr30/BigData/assets/86728825/79446404-df0f-44c1-ad71-7e297b07a6be)

- Distributed mode
  - Multiple machines
  - Each hadoop service daemon runs in its own JVM.
  - Best and typical for production environments.
  - Default replication factor = 3

![image](https://github.com/Adityasr30/BigData/assets/86728825/b18190b5-239d-4fe9-aaba-ac6b38d6c98d)

## About YARN

- Yet another resource negotiater.
- Limitations of MapReduce V1:
  - Bottleneck caused by having a single JobTracker
  - Fixed map and reduce slots
  - Can run only MapReduce jobs.
- Yarn solves this problem by brining in central resource management.
- Yarn splits up the functionality of the JobTracker in Hadoop 1.x into two separate processes:
  1. Resource manager (daemon) : for allocating resources and scheduling applications.
  2. Application master: for executing applications and providing failover
- Resource manager commmunicates with node managers, applicaion masters and client applications.
- Node manager (generalised task tracker):
  - Provides resources in the form of containers.
  - Containers executes application specific process.
  - Manages local CPU and RAM resources in the containers on behalf of requesting services.
  - Tracks node health and communicates status to the Resource manager.
- Architecture:

![image](https://github.com/Adityasr30/BigData/assets/86728825/cb0e9e1b-0f9c-4dd4-a16b-bffe851857f5)

- Components:
  1. Client: To submit MapReduce jobs.
  2. Resource manager: To manage the use of resources across the cluster.
  3. Container: Name given to a package of resources including RAM, CPU, network, HDD etc.
  4. Node manager: To oversee the containers running on the cluster nodes.
  5. Application master: negotiates with the resource manager for resources and runs the application-specific process (Map or Reduce tasks) in those clusters.
- Resource manager:
  - Two components: scheduler and application manager.
  - It is a global resource scheduler.
  - Manages and allocates cluster resources.

![image](https://github.com/Adityasr30/BigData/assets/86728825/04a3dca2-c54b-4fc6-b306-c1742af8a69d)

- Application master:
  - Manages application life cycle and task scheduling.
  - Application is a job submitted to the framework. (Ex: MapReduce job).

![image](https://github.com/Adityasr30/BigData/assets/86728825/a56dc70d-7e1d-404a-83fd-5e86dfbb4a74)

- Node manager:
  - Manages single node resources allocations per-node agent'

![image](https://github.com/Adityasr30/BigData/assets/86728825/34260591-48a3-4fc7-b23f-a3eea2db83a0)

- Container:
  - Basic unit of allocation.
- Example: Running a word count application:
  - In HDFS, we have the data. The data is stored across two nodes data node 1 and data node 2.
  - Client contacts the resource manager and asks it to run a application master process.
  - Resource manager contacts a node manager and node manager allocates a container for it.
  - Node manager requests for the resources from resource manager and job is launched over the two data nodes.

![image](https://github.com/Adityasr30/BigData/assets/86728825/760c4be9-34b4-4c36-b7df-5785497df34c)

## Hadoop Ecosystem

![image](https://github.com/Adityasr30/BigData/assets/86728825/51398f9c-b43c-485e-b915-aa579b7662d9)

**Apache Spark**:
Apache Spark is a fast and general-purpose data processing engine. It supports in-memory data processing and provides high-level APIs for batch processing, stream processing, machine learning, and graph processing.

**Apache Hive**:
Apache Hive is a data warehousing and SQL-like query language system built on top of Hadoop. It allows you to query and analyze large datasets using HiveQL, a SQL-like language.

**Apache HBase**:
Apache HBase is a distributed, scalable NoSQL database that runs on top of HDFS. It is designed for random read/write access to large datasets.

**Apache Pig**:
Apache Pig is a high-level platform for creating MapReduce programs using a scripting language called Pig Latin. It simplifies the development of complex data processing tasks.

**Apache ZooKeeper**:
Apache ZooKeeper is a centralized service for maintaining configuration information, naming, synchronization, and group services in distributed systems. It is often used for coordination tasks within Hadoop clusters.

**Apache Oozie**:
Apache Oozie is a workflow scheduler system to manage Hadoop jobs. It allows you to define, schedule, and execute workflows of dependent Hadoop jobs.

**Apache Flume**:
Apache Flume is a distributed, reliable, and available system for efficiently collecting, aggregating, and moving large amounts of log data from different sources to HDFS.

**Apache Kafka**:
While not part of the Hadoop project, Kafka is often considered as part of the Hadoop ecosystem. It is a distributed streaming platform that can be used for real-time data ingestion and processing.

**Apache Sqoop**:
Apache Sqoop is a tool for efficiently transferring data between Hadoop and relational databases. It enables data import and export between Hadoop and various databases.

## Kafka

Kafka is an open-source distributed streaming platform developed by Apache Software Foundation. It is widely used for building real-time data pipelines and streaming applications. Kafka is designed to handle high-throughput, fault-tolerant, and scalable data streams. The main components of Kafka include:

- **Broker**:
A Kafka broker is a server that stores and manages the published data streams. It is responsible for receiving messages from producers, storing them on disk in a distributed manner, and serving them to consumers upon request. Brokers can be part of a Kafka cluster, and they work together to ensure fault tolerance and scalability.

- **Topic**:
A topic in Kafka is a specific category or feed name to which messages are published by producers. Each message published to a topic is distributed to multiple partitions. Topics can be partitioned to enable parallel processing and horizontal scalability of data consumption.

- **Partition**:
A topic can be divided into multiple partitions, and each partition is a linearly ordered, immutable sequence of messages. Partitions allow you to distribute data across multiple brokers and enable parallel processing and read/write operations for better performance.

- **Producer**:
A producer is a client application that publishes data to Kafka topics. It writes messages to one or more Kafka topics, and the messages are then stored in the respective topic partitions within the Kafka brokers.

- **Consumer**:
A consumer is a client application that reads data from Kafka topics. It subscribes to one or more topics and consumes messages from the partitions of those topics. Each consumer keeps track of the offset (a unique identifier) of the last message read from each partition, allowing it to resume from the last read position if needed.

- **Consumer Group**:
Consumers are organized into consumer groups. A consumer group is a set of consumers that collectively consume messages from one or more topics. Each message published to a topic is delivered to only one consumer within each consumer group. This allows for load balancing and parallel consumption of data.

- **Zookeeper**:
Kafka relies on Apache ZooKeeper to manage its distributed nature. ZooKeeper helps with various tasks, including broker discovery, leader election for partitions, and keeping track of Kafka cluster metadata. However, with newer versions of Kafka, there is a move away from the dependency on ZooKeeper towards a self-managing protocol.

These components work together to create a highly scalable and fault-tolerant streaming platform, enabling real-time data processing and analytics for various applications and use cases.

![image](https://github.com/Adityasr30/BigData/assets/86728825/b659c18d-837b-4559-b51a-d1c901ec39dd)

## Hive

Hive is an open-source data warehousing and SQL-like query language system built on top of Hadoop. It was developed by Facebook and later contributed to the Apache Software Foundation. Hive allows you to query and analyze large datasets stored in Hadoop's HDFS (Hadoop Distributed File System) using a familiar SQL-like language called HiveQL. Here are some key aspects and components of Hive:

- **HiveQL**:
Hive Query Language (HiveQL) is a SQL-like language used to interact with data stored in Hadoop. It provides a simple and familiar way for users to write queries for data processing and analysis. HiveQL abstracts the complexities of Hadoop's MapReduce and other distributed computing frameworks, making it easier for data analysts and developers to work with big data.

- **Metastore**:
The Metastore is a centralized metadata repository in Hive that stores metadata about tables, partitions, and other schema information. It includes the schema definition, data types, column names, and storage location of tables. Hive uses this metadata to optimize query execution and facilitate table operations.

- **Tables and Databases**:
In Hive, data is organized into tables, which represent structured datasets. Tables can be partitioned, bucketed, and stored in different formats like Parquet or ORC. Multiple tables are organized into databases, allowing you to logically group related datasets.

- **Hive Execution Engine**:
Hive can work with different execution engines to process queries. Originally, Hive used Hadoop's MapReduce as the execution engine. However, with advancements in the Hadoop ecosystem, other execution engines like Tez and Spark have been integrated with Hive to improve query performance and optimization.

- **Hive CLI and HiveServer2**:
Hive provides two main interfaces for interacting with the system. The Hive Command-Line Interface (CLI) is a command-line tool that allows users to submit HiveQL queries and manage Hive resources. HiveServer2 is a service that enables remote clients to submit queries programmatically using JDBC or Thrift protocols.

- **User-Defined Functions (UDFs)**:
Hive allows you to define custom functions known as User-Defined Functions (UDFs) in Java, Python, or other languages. UDFs enable you to extend the functionality of Hive and perform custom data processing operations.

- **Integration with Hadoop Ecosystem**:
Hive integrates seamlessly with other components of the Hadoop ecosystem, such as HDFS for storage, HBase for NoSQL capabilities, and Spark for data processing. This integration allows you to leverage the strengths of various tools to handle different aspects of big data processing.

Hive's SQL-like interface and integration with Hadoop make it a popular choice for data warehousing, data processing, and business intelligence applications, especially in the big data domain. It enables users to leverage their SQL skills to work with large-scale datasets stored in Hadoop clusters.

## Hive Architecture

![image](https://github.com/Adityasr30/BigData/assets/86728825/1bf24939-134e-4918-8735-08ed02ffcc1b)

- **JDBC Driver** - It is used to establish a connection between hive and Java applications. The JDBC Driver is present in the class org.apache.hadoop.hive.jdbc.HiveDriver.
- **ODBC Driver** - It allows the applications that support the ODBC protocol to connect to Hive.
- **Hive CLI** - The Hive CLI (Command Line Interface) is a shell where we can execute Hive queries and commands.
- **Hive Web User Interface** - The Hive Web UI is just an alternative of Hive CLI. It provides a web-based GUI for executing Hive queries and commands.
- **Hive MetaStore** - It is a central repository that stores all the structure information of various tables and partitions in the warehouse. It also includes metadata of column - and its type information, the serializers and deserializers which is used to read and write data and the corresponding HDFS files where the data is stored.
- **Hive Server** - It is referred to as Apache Thrift Server. It accepts the request from different clients and provides it to Hive Driver.
- **Hive Driver** - It receives queries from different sources like web UI, CLI, Thrift, and JDBC/ODBC driver. It transfers the queries to the compiler.
- **Hive Compiler** - The purpose of the compiler is to parse the query and perform semantic analysis on the different query blocks and expressions. It converts HiveQL statements into MapReduce jobs.
- **Hive Execution Engine** - Optimizer generates the logical plan in the form of DAG of map-reduce tasks and HDFS tasks. In the end, the execution engine executes the incoming tasks in the order of their dependencies.

## Difference between external and managed tables

In Hive, there are two types of tables: External tables and Managed tables. Each type has its own characteristics and use cases. Here are the main differences between them:

- **Location and Data Management**:

Managed Tables: When you create a managed table in Hive, Hive itself manages the lifecycle and storage of the data associated with the table. The data is stored in the Hive data warehouse directory (usually in HDFS). If you drop a managed table, Hive will also remove the table data from the warehouse directory.
External Tables: With external tables, the data is not managed by Hive. The table definition in Hive points to an existing data location outside of the Hive warehouse directory (e.g., in HDFS or an external storage system). If you drop an external table, it does not affect the underlying data since Hive only drops the table metadata, not the actual data files.

- **Data Durability**:

Managed Tables: Since Hive manages the data for managed tables, if a managed table is dropped, the data is also deleted. This could lead to data loss if you accidentally drop a table.
External Tables: With external tables, the data exists independently of the table definition in Hive. The data remains intact even if the external table is dropped, providing more data durability and safety.

- **Data Sharing**:

Managed Tables: Managed tables are ideal for data that is specific to Hive and not shared with other systems. The data is tightly coupled with Hive's lifecycle.
External Tables: External tables are suitable when you want to share data with other systems or when the data is generated and managed by an external process outside of Hive. Since the data exists independently, other systems can access the same data without needing to go through Hive.

- **Backup and Recovery**:

Managed Tables: Since Hive manages the data of managed tables, backup and recovery processes typically involve backing up the entire Hive warehouse directory.
External Tables: In the case of external tables, you only need to backup the external data location, which is separate from the Hive warehouse, making backup and recovery more straightforward.

- **Data Ingestion**:

Managed Tables: When you load data into a managed table, Hive typically moves the data from the source location into the Hive warehouse directory.
External Tables: For external tables, the data is already present at the external location, and Hive only creates metadata to represent the table over that data without moving it.

In summary, managed tables are suitable when you want Hive to manage the data lifecycle, and you don't need to share the data with external systems. On the other hand, external tables are useful when the data is shared among multiple systems, or you have existing data that you want to make accessible through Hive without moving it. The choice between managed and external tables depends on the specific use case and data management requirements of your Hive-based application.

## Sqoop

Sqoop (SQL-to-Hadoop) is an open-source command-line tool and a subproject of Apache Hadoop designed to efficiently transfer data between relational databases and Hadoop (HDFS and Hive). It enables users to import data from databases such as MySQL, Oracle, PostgreSQL, SQL Server, and others into Hadoop, and also export data from Hadoop back to relational databases.

Key features of Sqoop:

- **Data Import and Export**:
Sqoop provides commands to import data from a relational database table into Hadoop, and export data from Hadoop back to the database. This is particularly useful when you want to perform large-scale data processing and analysis using Hadoop's distributed processing capabilities.

- **Parallel Data Transfer**:
Sqoop can perform parallel data transfers, allowing it to efficiently import and export large datasets. It splits the data into multiple chunks, and each chunk is transferred in parallel to leverage the full power of the Hadoop cluster.

- **Data Compression**:
Sqoop supports data compression during data transfers, which reduces the storage space and improves data transfer performance.

- **Support for Hive and HBase**:
Sqoop can directly import data into Hive tables or HBase, allowing you to leverage the benefits of these data storage and processing frameworks in conjunction with Hadoop.

- **Incremental Data Imports**:
Sqoop can perform incremental imports, allowing you to import only the new or updated rows from a database table since the last import. This is useful for efficiently keeping the Hadoop data up-to-date with the source database.

- **Connectivity to Various Databases**:
Sqoop supports various relational databases, and it can work with JDBC drivers to establish connections and interact with them.

- **Extensibility**:
Sqoop is extensible and can be integrated with other data processing tools or systems through custom connectors and plugins.

Example use cases for Sqoop include:

Importing data from a relational database into Hadoop for large-scale data processing and analysis.
Exporting the results of data processing in Hadoop back to a relational database for reporting or serving purposes.
Loading data into Hive or HBase for further analysis or querying.
Sqoop is a valuable tool in the Hadoop ecosystem, providing seamless integration between relational databases and Hadoop, allowing organizations to leverage the strengths of both worlds and efficiently manage their data pipelines.

## Core Hadoop Configuration files

![image](https://github.com/Adityasr30/BigData/assets/86728825/1270caba-008b-4678-bc2b-24bbf695d781)
