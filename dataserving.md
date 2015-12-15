---
layout: page
title: Data serving
bench: "true"
---


[![Pulls on DockerHub][dhpulls]][dhrepo]
[![Stars on DockerHub][dhstars]][dhrepo]

The data serving benchmark relies on the Yahoo! Cloud Serving Benchmark (YCSB). YCSB is a framework to benchmark data store systems. This framework comes with the interfaces to populate and stress many popular data serving systems. Here we provide the instructions and pointers to download and install YCSB and use it with the Cassandra data store.

## Generating Datasets

The YCSB client has a data generator. After starting Cassandra, YCSB can start loading the data. First, you need to create a keyspace named usertable and a column family for YCSB. This is a must for YCSB to load data and run.

###Server Container
Start the server container:

    $ docker run -it --name cassandra-server dataserving/cassandra:server bash

In order to create a keyspace and a column family, you can use the following commands after connecting to the server with the cassandra-cli under the directory Cassandra is unpacked in. (A link to a basic tutorial with cassandra-cli: http://wiki.apache.org/cassandra/CassandraCli )

1. Run the server:     
```
$ cassandra
```

2. Run the command:
```
$ cassandra-cli
```

3. Use the following commands to create a keyspace and column family for YCSB:
```
$ create keyspace usertable;
$ use usertable;
$ create column family data;
```

You can use other commands in the cassandra-cli to verify the correctness of the setup :

    $ dshow keyspaces;
    $ show schema;

If you’ve made a mistake you can use the drop command and try again:

    $ drop keyspace usertable;

###Client
If you have successfully created the aforementioned schema, you are ready to benchmark with ycsb.
Start the client container:

    $ docker run -it --name cassandra-client --link cassandra-server:server dataserving/cassandra:client bash	

1. Change to the ycsb directory:
```
$ cd ycsb
```

2. Load dataset on ycsb: 
```
$ ./bin/ycsb load cassandra-10 -p hosts=server -P workloads/workloada
```

More detailed instructions on generating the dataset can be found in Step 5 at [this](http://github.com/brianfrankcooper/YCSB/wiki/Running-a-Workload) link. Although Step 5 in the link describes the data loading procedure, other steps (e.g., 1, 2, 3, 4) are very useful to understand the YCSB settings.

A rule of thumb on the dataset size
-----------------------------------
To emulate a realistic setup, you can generate more data than your main memory size if you have a low-latency, high-bandwidth I/O subsystem. For example, for a machine with 24GB memory, you can generate 30 million records corresponding to a 30GB dataset size.

Note: The dataset resides in Cassandra’s data folder(s).The actual data takes up more space than the total size of the records because data files have metadata structures (e.g., index). Make sure you have enough disk space.

Tuning the server performance
-----------------------------
1. In general, the server settings are under the $CASSANDRA_PATH/conf folder. The main file is cassandra.yaml. The file has comments about all parameters. This parameters can also be found here: http://wiki.apache.org/cassandra/StorageConfiguration
2. You can modify the target and threadcount variables to tune the benchmark and utilize the server. The throughput depends on the number of hard drives on the server. If there are enough disks, the cores can be utilized after running the benchmark for 10 minutes. Make sure that half of the main memory is free for the operating system file buffers and caching.
3. Additionally, the following are useful pointers for performance tuning:

	a. http://spyced.blogspot.com/2010/01/linux-performance-basics.html

	b. http://wiki.apache.org/cassandra/MemtableThresholds

Running the benchmark
---------------------
After you install and run the server, install the YCSB framework files and populate Cassandra, you are one step away from running the benchmark. To specify the run time parameters for the client, a good practice is to create a settings file. You can keep the important parameters (e.g., target , threadcount , hosts , operationcount , recordcount ) in this file.

The settings.dat file defines the IP address(es) of the node(s) running Cassandra, in addition to the recordcount parameter (which should be less than or equal to the number specified in the data generation step to avoid potential errors). 

The operationcount parameter sets the number of operations to be executed on the data store. 

The run.command file takes the settings.dat file as an input and runs the following command:

    $ /ycsb/bin/ycsb run cassandra-10 -p hosts=server -P /ycsb/workloads/workloada

[dhrepo]: https://hub.docker.com/r/cloudsuite/dataserving/ "DockerHub Page"
[dhpulls]: https://img.shields.io/docker/pulls/cloudsuite/dataserving.svg "Go to DockerHub Page"
[dhstars]: https://img.shields.io/docker/stars/cloudsuite/dataserving.svg "Go to DockerHub Page"

