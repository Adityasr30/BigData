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
