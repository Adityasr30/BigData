## Introduction to Big Data

- Small data: mostly structured (not used much nowadays)
- 90% of data is unstructured (Big data)
- Structured data is generally of range - MB, GB, TB.
- Big data is stored in PB, EB, ZB ...
- Small data increases gradually (moderate or small)
- Big data increases exponentially (on daily basis, huge amount of data is being generated)
- Small data is stored centrally.
- Big data is stored distributed.
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
- Hiearchical architure
- Based on local file system
- Designed for huge amount of data
- Can be deployed on the existing file system/ devices. Thus making it cost effective.
- Namenode (master node) and datanode.
- Divides a file into parts.
- Metadata is stored in namespace in name node.
- Data is replicated to multiple nodes (fault tolerance).
- Data nodes are stored in racks.
- If a data is stored inside a datanode. Then this data node is stored in a rack. The data will also be replicated on another data node. This data node will note be stored in the same rack because, if the rack itself gets corrupted or down, then the data might be lost. This concept is called as Rack awareness.
- While fetching data, hdfs tries to fetch it from the nearest rack. Original data is kept locally.
- Components of name node: FsImage, EditLogs.
- FsImage: Image/ Snapshot of Hdfs.
- EditLogs: log file of every action.
- Secondary name node: Updates FsImage. It merges FsImage and EditLogs file.
- Heartbeat: datanode sends heartbeat signal every 3 seconds to name node, indicating that it is alive.
- When client tries to access data, the request goes to the namenode. The namenode identifies where the data is, on the data node through metadata information. Then returns the address where data is stored to the client.
- Reads are easy/ fast. Writes are difficult. Because to write on one data node, we also need to replicate it to other data nodes as well.

![image](https://github.com/Adityasr30/BigData/assets/86728825/b80de135-85d2-457c-bdea-07a645c2f5ef)

## What is MapReduce?

- Processing unit
- Two tasks: Map and reduce
- Uses divide and conquer approach
- Mapper: converts data into key-value pairs
- Daemons: Job tracker, task tracker
- Job tracker: schedule jobs, provides resources, acts as OS.
- Task tracker: executes tasks.
- MapReduce tries data close to the processing unit. In other words task tracker is kept on data node.
- To reduce delay, data is kept locally.
- MapReduce steps:
  1. Input
  2. Splitting
  3. Mapping
  4. Shuffling
  5. Reducing

![image](https://github.com/Adityasr30/BigData/assets/86728825/23fbd29e-27bb-49d7-a32c-d222775250de)

## Hadoop Deployement Modes

- Standalone mode
  - All hadoop service daemons run in a single JVM
  - Suitable for test and development
  - No replication of data

- Pseudo-distributed mode
  - Simulates distributed environment on a single machine.
  - Each hadoop service daemon runs in its own JVM.
  - Appropriate for quality assurance, test and development.
  - Default replication factor = 1

- Distributed mode
  - Multiple machines
  - Each hadoop service daemon runs in its own JVM.
  - Best and typical for production environments.
  - Default replication factor = 3

## About YARN

- Yet another resource negotiater.
- Yarn splits up the functionality of the JobTracker in Hadoop 1.x into two separate processes:
  1. Resource manager: for allocating resources and scheduling applications.
  2. Application master: for executing applications and providing failover
- Resource manager commmunicates with node managers, applicaion masters and client applications.
- Node manager:
  - Manages local CPU and RAM resources on behalf of requesting services.
  - Tracks node health and communicates status to the Resource manager.
