# ELK sample cluster setup on static IPs
* Kibana
 * http://localhost:5601
 * Sample data are around 2016-10-21T05:59:07 (or get some newer from util-backup server or ...)
 * http://localhost:9200/_plugin/head/
  * for fast cluster state verification and mapping setup

## Start stack
* 2x ELK in cluster
 * exposed ports:
  * 9200 / 9300
 * you can spin more of them, just edit composer file
* 1x Kibana
 * exposed port: 5601
 * you can use .raw field for not_analyzed data
* 1x Logstash for easy sample data upload
 * exposed ports:
 * 5000 - json filter
 * 5001 - raw

```
docker-compose up -d
or
docker-compose up --remove-orphans --build

docker-compose down -d
```

## Upload mapping
* elasticsearch/mapping/no_mapping.sh
* or manually:

```
curl -XPUT 'localhost:9200/_template/all' -d '
{
"order": 0,
"template": "*",
"settings": {
"index.number_of_shards": "1"
},
"mappings": {
"default": {
"dynamic_templates": [
{
"string": {
"mapping": {
"index": "not_analyzed",
"type": "string"
},
"match_mapping_type": "string"
}
}
]
}
},
"aliases": {}
}
}
'
```

## Upload sample data via Logstash

```
nc localhost 5000 < samples/access_log
```
