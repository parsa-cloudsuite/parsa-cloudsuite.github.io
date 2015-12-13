---
layout: page
title: Graph analytics
bench: "true"
---

This repository contains the docker image with Cloudsuite's Graph Analytics Benchmark.

The Graph Analytics Benchmark relies on using the Spark framework to perform graph analytics on large-scale datasets. Apache provides a graph processing library, GraphX, designed to run on top of Spark. The benchmark performs pagerank in the twitter dataset.

## Using the benchmark ##

### Dockerfiles ###

Supported tags and their respective `Dockerfile` links:
- [`benchmark`][benchmarkdocker] This builds a volume image with the benchmark binaries
- [`data`][datadocker] This builds a volume image with the benchmark dataset
- [`spark-master`][sparkmasterdocker] This builds a image with the Spark master node.
- [`spark-worker`][sparkworkerdocker] This builds a image with the Spark worker node. You may spawn many worker clusters.
- [`spark-client`][sparkclientdocker] This builds a image with the Spark client node. The client is used to start the benchmark.

These images are automatically built using the mentioned Dockerfiles available on the [`CloudSuite-EPFL/GraphAnalytics`][repo] and [`CloudSuite-EPFL/spark-base`][sparkrepo].

### Starting the volume images ###

The first step is to create the volume images that contain the binaries and the dataset of the Graph Analytics benchmark. First `pull` the volume images, using the following command:

    $ docker pull cloudsuite/GraphAnalytics:data
    $ docker pull cloudsuite/GraphAnalytics:benchmark

The following command will start the volume images, making both the data and the binaries avaliable for other docker images in the host:

    $ docker create --name data cloudsuite/GraphAnalytics:data
    $ docker create --name bench cloudsuite/GraphAnalytics:benchmark

### Starting the master node ###

To start the server you have to first `pull` the Spark master node image and then run it. To `pull` the Spark master node image, use the following command:

    $ docker pull cloudsuite/spark-base:master

The following command will start the master node and forward port 8080 to the host, so that the Spark web interface can be accessed from the web browser, using the host IP address.

    $ docker run -d -P -p 8080:8008-h master --volumes-from data --volumes-from bench --name spark-master cloudsuite/spark-base:master

### Starting the workers ###

To start the worker you have to first `pull` the Spark worker node image and then run it. To `pull` the Spark worker node image, use the following command:

    $ docker pull cloudsuite/spark-base:worker

The following command will start the worker node.

    $ docker run -d -P --volumes-from data --volumes-from bench --link spark-master --name spark-worker1 cloudsuite/spark-base:worker spark://master:7077

### Starting the client and running the benchmark ###

To start the client you have to first `pull` the Spark client node image and then run it. To `pull` the Spark client node image, use the following command:

    $ docker pull cloudsuite/spark-base:client

The following command will start the client node and run the benchmark:

    $ docker run --rm --volumes-from data --volumes-from bench --link spark-master spark-client graph_analytics

The following command will start the client interactivelly:

    $ docker run --rm --volumes-from data --volumes-from bench --link spark-master -it spark-client bash

To run the benchmark from the interactive container, use the following command:

    $ bash /benchmark/graph_analytics/run_benchmark.sh

[benchmarkdocker]: https://github.com/CloudSuite-EPFL/GraphAnalytics/blob/master/benchmarks/Dockerfile "Benchmark volume Dockerfile"
[datadocker]: https://github.com/CloudSuite-EPFL/GraphAnalytics/blob/master/data/Dockerfile "Data volume Dockerfile"
[sparkmasterdocker]: https://github.com/CloudSuite-EPFL/spark-base/blob/master/spark-master/Dockerfile "Spark Master Node Dockerfile"
[sparkworkerdocker]: https://github.com/CloudSuite-EPFL/spark-base/blob/master/spark-worker/Dockerfile "Spark Worker Dockerfile"
[sparkclientdocker]: https://github.com/CloudSuite-EPFL/spark-base/blob/master/spark-client/Dockerfile "Spark Client Dockerfile"
[repo]: https://github.com/CloudSuite-EPFL/GraphAnalytics "Graph Analytics GitHub Repo"
[sparkrepo]: https://github.com/CloudSuite-EPFL/spark-base "Spark Base GitHub Repo"
