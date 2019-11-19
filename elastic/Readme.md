
# Elasticsearch docker usage

## Running elasticsearch from command line

```
docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch
```

## Elastic & Kibana using docker compose

In the current directory run the docker compose command, add -d in order to start in detached mode:

```
docker-compose up -d
```

This docker compose file mountes the elasticsearch.yml configuration file. The benegit is that you could modify and customize it for exampe to support repository path that is used for taking snapshots.

## Elasticsearch snapshot

Follow the instructions in the [documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-snapshots.html) in order to create a repository and then take a snapshot.

Keep in mind that an initial snapshot is created pro repository and the following snapshots are based on incremental data, also only all changed indicies are added to the new snapshot. In addition you could create a snapshot for defined indicies.

This command in Kibana would create snapshot_1 in my_backup repository:

```
PUT /_snapshot/my_backup/snapshot_1?wait_for_completion=true
```

And this command would get the current state of the snapshot process:

```
GET /_snapshot/my_backup/snapshot_1
```

## Searching

Let say one wants to search inside an index with some date conditions: contents modifiedAt 2017 January.

```
GET /contents/_search
{
  "query": {
    "bool": {
      "must": [
        {
          "range": {
            "modifiedAt": {
              "gte": "2017-01-01||/M",
              "lte": "2017-01-31||/M"
            }
          }
        }
      ]
    }
  },
  "sort": [
    {
      "createdAt": {
        "order": "desc"
      }
    }
  ]
}
```

