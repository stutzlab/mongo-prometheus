# mongo-prometheus

Mongo Prometheus exporter docker-compose

Point each instance of this container to a MongoDB instance. It may be a standalone mongo, cluster router, configserver or a shard instance.

Use Prometheus to record and monitor metrics and view them in Grafana. A good Grafana dashboard for MongoDB is https://grafana.com/grafana/dashboards/2583

## Usage

* Create docker-compose.yml:

```yml
version: '3.5'
services:
  mongo-prometheus:
    image: bitnami/mongodb-exporter:0.11.0-debian-10-r75
    ports:
      - 8880:9216
    environment:
      - MONGODB_URI=mongodb://admin:admin123@mongo:27017
  mongo:
    image: mongo:4.2.8-bionic
    restart: always
    ports:
      - 27017:27017
    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
      - MONGO_INITDB_ROOT_PASSWORD=admin123
      - MONGO_INITDB_DATABASE=sample
```

* Run ```docker-compose up -d```

* Run ```curl localhost:8880/metrics```
  * See some metrics

* Add this target to your own Prometheus instance
  * See /docker-compose.yml for a more comprehensive example
