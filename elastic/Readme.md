
# Elasticsearch docker usage

## How to run elasticsearch docker container from command line:

```
docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.3.2
```

## Elastic & Kibana

```
docker-compose up
```
