---
layout: page
title: In-memory analytics
bench: "true"
---

### Collaborative filtering benchmark on Spark

Create volumes on each node in the cluster:

    docker create --name data data
    docker create --name bench benchmarks

Start master and workers:

    docker run -dP --volumes-from data --volumes-from bench --net swarm-network \
      --hostname spark-master --name spark-master spark-master
    docker run -dP --volumes-from data --volumes-from bench --net swarm-network \
      --hostname spark-worker --name spark-worker spark-worker spark://spark-master:7077

Monitor via web UI:

    MASTER_IP=$(docker inspect --format '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' spark-master)
    MASTER_PORT=$(docker port spark-master | grep '7077' | cut cut -d: -f2)
    Point browser either to $MASTER_IP:8080 or <NodeIP>:$MASTER_PORT

Run benchmark using client:

    docker run --rm --volumes-from data --volumes-from bench --net swarm-network \
      spark-client bench movielens-als

Run client interactively:

    docker run --rm --volumes-from data --volumes-from bench --net swarm-network \
      -it spark-client bash

Stop everything and remove containers and volumes:

    docker ps -q | xargs docker stop
    docker ps -aq | xargs docker rm -v

