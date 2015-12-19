---
layout: page
title: In-memory analytics
bench: "true"
---

[![Pulls on DockerHub][dhpulls]][dhrepo]
[![Stars on DockerHub][dhstars]][dhrepo]

The explosion of accessible human-generated information necessitates automated analytical processing to cluster, classify, and filter this information. Recommender systems are a subclass of information filtering system that seek to predict the 'rating' or 'preference' that a user would give to an item. Recommender systems have become extremely common in recent years, and are applied in a variety of applications. The most popular ones are probably movies, music, news, books, research articles, search queries, social tags, and products in general. Because these applications suffer from I/O operations, nowadays, most of them are running in memory. The In Memory Analytics benchmark runs the alternating least squares (ALS) algorithm which is provided by Spark MLlib. 

Create volumes on each node in the cluster:

    $ docker create --name data data
    $ docker create --name bench benchmarks

Start master and workers:

    $ docker run -dP --volumes-from data --volumes-from bench --net swarm-network \
      --hostname spark-master --name spark-master spark-master
    $ docker run -dP --volumes-from data --volumes-from bench --net swarm-network \
      --hostname spark-worker --name spark-worker spark-worker spark://spark-master:7077

Monitor via web UI:

    $ MASTER_IP=$(docker inspect --format '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' spark-master)
    $ MASTER_PORT=$(docker port spark-master | grep '7077' | cut cut -d: -f2)
    Point browser either to $MASTER_IP:8080 or <NodeIP>:$MASTER_PORT

Run benchmark using client:

    $ docker run --rm --volumes-from data --volumes-from bench --net swarm-network \
      spark-client bench movielens-als

Run client interactively:

    $ docker run --rm --volumes-from data --volumes-from bench --net swarm-network \
      -it spark-client bash

Stop everything and remove containers and volumes:

    $ docker ps -q | xargs docker stop
    $ docker ps -aq | xargs docker rm -v
    
[dhrepo]: https://hub.docker.com/r/cloudsuite/inmemoryanalytics/ "DockerHub Page"
[dhpulls]: https://img.shields.io/docker/pulls/cloudsuite/inmemoryanalytics.svg "Go to DockerHub Page"
[dhstars]: https://img.shields.io/docker/stars/cloudsuite/inmemoryanalytics.svg "Go to DockerHub Page"
