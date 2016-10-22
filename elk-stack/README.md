# ELK sample cluster setup on static IPs
* Kibana
 * http://localhost:5601
 * Sample data are around 2016-10-21T05:59:07
 * http://localhost:9200/_plugin/head/

## Start (2x ELK in cluster + Kibana and logstash for simple data upload)

```
docker-compose up -d

docker-compose down -d
```

## Upload mapping

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
