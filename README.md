# Docker compose collection

## Consul

Latest consul docker image

## Elastic search & Kibana

ELK Stack containg Elasticsearch with single node and kibana server
Elasticsearch configuration is mounted and can be customized.
Repository is configured.

## Core Services

Following services are defined

- Consul

    - Default port: 8500
    - https://hub.docker.com/_/consul
- Vault

    - Default port: 8200
    - How to install Vault (https://www.bogotobogo.com/DevOps/Docker/Docker-Vault-Consul.php)
- Vault-ui

    - Default port: 8000    
- Elasticsearch

    - Default port elasticsearch: 9200
    - https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html
- Kibana

    - Default port kibana: 5601    
    - https://www.elastic.co/guide/en/kibana/current/docker.html
- Mailhog

    - Mailserver mockup for developers (https://github.com/mailhog/MailHog)
    - Default port: 1025
- Minio

    - Blob storage service
    - https://github.com/minio/minio


## Startup & Tear down

    - docker-compose up -d
    - docker-compose down
