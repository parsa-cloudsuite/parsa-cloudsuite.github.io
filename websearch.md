---
layout: page
title: Web search
bench: "true"
---

This repository contains the docker image for Cloudsuite's Web Search benchmark.

The Web Search benchmark relies on the Apache Solr search engine framework. The benchmark includes a client machine that simulates real-world clients that send requests to the index node.

## Using the benchmark ##

### Dockerfiles ###

Supported tags and their respective `Dockerfile` links:

- [`data`][datadocker] This builds a volume image with the benchmark's dataset.
- [`server`][serverdocker] This builds an image for the Spark worker node. You may spawn several workers.
- [`client`][clientdocker] This builds an image with the Spark client node. The client is used to start the benchmark.

These images are automatically built using the mentioned Dockerfiles available on [`CloudSuite-EPFL/WebSearch`][repo].

### Starting the volume images ###

The first step is to create the volume images that contain the dataset of the Web Search benchmark. First `pull` the volume images, using the following command:

	$ docker pull cloudsuite/websearch:data

The following command will start the volume images, making both the data available for other docker images on the host:

	$ docker create --name data cloudsuite/websearch:data

### Starting the server (Index Node) ###

To start the server you have to first `pull` the server image and then run it. To `pull` the server image, use the following command:

	$ docker pull cloudsuite/websearch:server

The following command will start the server and forward port 8983 to the host, so that the Solr web interface can be accessed from the web browser, using the host IP address.

	$ docker run --volumes-from data --name server -it -p 8983:8983 -t websearch:server

### Starting the client and running the benchmark ###

To start a worker you have to first `pull` the client image and then run it. To `pull` the Spark worker node image, use the following command:

	$ docker pull cloudsuite/websearch:client

The following command will start the client node and run the benchmark:

	$ docker run --volumes-from data -p 9980:9980 --name client --link=server -it -t websearch:client

The output results will show on the screen after the benchmark finishes.

[datadocker]: https://github.com/CloudSuite-EPFL/WebSearch/tree/master/data/Dockerfile "Data volume Dockerfile"
[serverdocker]: https://github.com/CloudSuite-EPFL/WebSearch/tree/master/server/Dockerfile "Server Dockerfile"
[clientdocker]: https://github.com/CloudSuite-EPFL/WebSearch/tree/master/client/Dockerfile "Client Dockerfile"
[repo]: https://github.com/CloudSuite-EPFL/WebSearch "Web Search GitHub Repo"