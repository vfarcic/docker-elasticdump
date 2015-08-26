Docker elastic-dump
===================

Lightweight Docker container with [elasticsearch-dump](https://github.com/taskrabbit/elasticsearch-dump).
It is based on Alpine OS and occupies only ~28MB.

Usage
-----

elastic-dump is the entry point and expects parameters to be passed as Docker command.

### Export

To export and zip an entire LogStash index (change MY_DOMAIN):

```bash
sudo docker run --rm vfarcic/elastic-dump \
    --input=http://MY_DOMAIN:9200/logstash-* \
    --output=$ \
    --type=data | gzip >es-logstash.gzip
```

To export Kibana configuration (change MY_DOMAIN):

```bash
sudo docker run --rm vfarcic/elastic-dump \
    --input=http://MY_DOMAIN:9200/.kibana \
    --output=$ \
    --type=data >es-kibana.json
```

### Import

To import LogStash index (change MY_DOMAIN):

```bash
sudo docker run --rm \
    -v $PWD:/data \
    vfarcic/elastic-dump \
    --input=/data/es-logstash.json \
    --output=http://MY_DOMAIN:9200/.kibana \
    --type=data
```

To import Kibana configuration (change MY_DOMAIN):

```bash
sudo docker run --rm \
    -v $PWD:/data \
    vfarcic/elastic-dump \
    --input=/data/es-kibana.json \
    --output=http://MY_DOMAIN:9200/.kibana \
    --type=data
```