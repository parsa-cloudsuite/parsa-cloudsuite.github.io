---
layout: page
title: Web serving
bench: "true"
---

[![Pulls on DockerHub][dhpulls]][dhrepo]
[![Stars on DockerHub][dhstars]][dhrepo]

Web Serving is a main service in the cloud. Traditional web services with dynamic and static content are moved into the cloud to provide fault-tolerance and dynamic scalability by bringing up the needed number of servers behind a load balancer. Although many variants of the traditional web stack are used in the cloud (e.g., substituting Apache with other web server software or using other language interpreters in place of PHP), the underlying service architecture remains unchanged. Independent client requests are accepted by a stateless web server process which either directly serves static files from disk or passes the request to a stateless middleware script, written in a high-level interpreted or byte-code compiled language, which is then responsible for producing dynamic content. All the state information is stored by the middleware in backend databases such as cloud NoSQL data stores or traditional relational SQL servers supported by key-value cache servers to achieve high throughput and low latency. This benchmark includes a social networking engine (Elgg) and a client implemented using the Faban workload generator.

## Using the benchmark ##
The benchmark has four tiers: the web server, the database server, the memcached server, and the clients. The web server runs Elgg and it connects to the memcached server and the database server. The clients send requests to login to the social network. Each tier has its own image which is identified by its tag.

### Dockerfiles ###

Supported tags and their respective `Dockerfile` links:

 - [`web_server`][webserverdocker]: This represents the web server.
 - [`memcached_server`][memcacheserverdocker]: This represents the memcached server.
 - [`db_server`][mysqlserverdocker]: This represents the database server which runs MySQL.
 - [`fabanclient`][clientdocker]: This represents the faban client.

These images are automatically built using the mentioned Dockerfiles available on the `CloudSuite-EPFL/WebServing` [GitHub repo][repo].

### Creating a network between the servers and the client(s)

To facilitate the communication between the client(s) and the servers, we build a docker network:

    $ docker network create my_net

We will attach the launched containers to this newly created docker network.

### Starting the Web Server ####
To start the web server you have to first `pull` the server image and then run it. To `pull` the server image use the following command:

    $ docker pull cloudsuite/webserving:web_server

The following command will start the web server, and attach it to the *my_net* network:

    $ docker run -d -t --net=my_net --privileged=true --name=php_server cloudsuite/webserving:web_server /etc/bootstrap.sh


### Starting the Client ####

To start the client you have to first `pull` the client image and then run it. To `pull` the client image use the following command:

    $ docker pull cloudsuite/webserving:faban_client

To start the client container and connect it to the *my_net* network use the following command:

    $ docker run -d -t --net=my_net --privileged=true --name=faban_client cloudsuite/webserving:faban_client /etc/bootstrap.sh -bash

###  Running the benchmark ###

run.sh
To start the client, navigate to the /videoperf/run directory in the client container and launch the *benchmark.sh* script. This script is configured to launch a client process that issues a mix of requests for different videos of various qualities and performs a binary search of experiments to find the peak request rate the client can sustain while keeping the failure rate acceptable. At the end of the script's execution, the client's log files can be found under the /videoperf/run/output directory.

  [webserverdocker]: https://github.com/CloudSuite-EPFL/MediaStreaming/blob/master/server/Dockerfile "Server Dockerfile"

  [clientdocker]: https://github.com/CloudSuite-EPFL/MediaStreaming/blob/master/client/Dockerfile "Client Dockerfile"

  [repo]: https://github.com/CloudSuite-EPFL/MediaStreaming "GitHub Repo"
  [dhrepo]: https://hub.docker.com/r/cloudsuite/mediastreaming/ "DockerHub Page"
  [dhpulls]: https://img.shields.io/docker/pulls/cloudsuite/mediastreaming.svg "Go to DockerHub Page"
  [dhstars]: https://img.shields.io/docker/stars/cloudsuite/mediastreaming.svg "Go to DockerHub Page"
  [nginx_repo]: https://github.com/nginx/nginx "Nginx repo"
  [httperf_repo]: https://github.com/httperf/httperf "httperf repo"



docker build -t memcache_server docker_memcached/
docker run -d -t --net=my_net --privileged=true --name=memcache_server memcache_server

docker build -t mysql_server docker_db_server/
docker run -d -t --net=my_net --privileged=true --name=mysql_server mysql_server