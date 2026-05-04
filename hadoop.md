# what is big data?
* big data is large amount of data that cannot be stored and processed in a tradition way i.e. one single compute hardware
* data is categorized as big data if it fits all the below facets:
** volume
** velocity
** variety
** veracity
** value


# what is hadoop?
* hadoop is a framework that manages big data storage in a distributed way and proceses it parallely


# components of hadoop?
## storage unit of hadoop - HDFS (hadoop distributed file system)
* HDPS is specially designed for storing huge datasets in commodity hardware
* HDFS has 2 core components namenode and datanode
* namenode
** there is only 1 namenode typically
** newer versions of hadoop there are 2 namenode the other is a backup but only one is active and processing everything
** these need to be enterprise servers
* datanode
** there can be multiple datanodes
** these can be commodity hardware
* master (namenode) / slave (datanode) nodes typically form the HDFS cluster
** master (namenode) which is the one in charge and slaves are the datanodes
** master controls the slaves and gets them to do all the work
** namenode maintains and manage the datanode. it also stores the metadata i.e. it stores what is going on across the file system
** datanodes store the actual data and do the reading, writing and processing. datanodes perform replication as well
** heartbeat is a signal that datanode continuously sends to the namenode. this signal shows the status of the namenode
* in HDFS data is stored in a distributed manner
** data is loaded into the namenode and the namenode distributes it across the datanodes, typically divided in 128MB blocks each
** blocks are replicated across datanodes for the purpose of fault-tolerance (default replication is 3x)


## processing unit of hadoop - map reduce
* hadoop map reduce is a programming technique where huge amount of data is processed in a parallel and distributed fashion
* as a developer it is important to know how map reduce functions and queries data
* map reduce is used for parallel processing of big data which is stored in the HDFS
* map reduce produces an output which is expected to have value
* in map reduce, processing is done at the slave nodes and the final result is sent to the master node
* the code for the map reduce is typically small, a few KB
* process visualization for map reduce:
** input -> split -> map phase -> shuffle and sort -> reduce (value)
*** split: the input dataset is first split into chunks of data. split could be done by the row, file, twitter feed, email etc
*** map phase: any process you could do on that chunk of data that does not require any other data. these chunks of data are then processed by map tasks parallely. during the map phase we always attach it to a key and assign values.
*** the key is how we are going to shuffle and sort. the shuffle and sort is all handled by the map reduce setup.
*** at the reduce task, the aggregation takes place and the final output is obtained


## resource management unit of hadoop -YARN
* Yet Another Resource Negotiator (YARN)
* YARN acts like a hadoop OS
* its not controlling one computer but all the computers in the cluster
* responsible for managing cluster resources knowing where everything is going making sure you do not overload a machine
* its also responsible for job scheduling making sure the jobs are scheduled in the right place

         (submits job request)                    (manages the nodes and monitors resource usage on the node)
* client ---------------------> resource manager ------------------> (node manager, container, app master) on nodes
  (count                   (responsible for resource  \------------> (node manager, container, app master) on nodes
   words)                   allocation and management) \-----------> (node manager, container) on nodes
                                                          (container is a collection of physical resources such as RAM, CPU)
                                                          (app master requests container from the node manager)

* app master communicates to the node manager, I have a process going on and I need so much RAM and so much CPU
* these requests then are forwarded to the resource manager, responsible for resource allocation and management, responsible for the oveall big picture