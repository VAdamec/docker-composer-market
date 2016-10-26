# ELK sample cluster setup on static IPs
* https://github.com/VAdamec/docker-composer-market
* Simple Makefile for change prebuild images in Registry (build and push)
  * ```make all```

#Structure
* README.md - this document
* README_workshop.md - workshop description
* README_mapping.md - mapping examples and how to use them/work with them

## Stack
* 5x ELK in cluster (2x master node, 3x data nodes)
 * exposed ports:
   * 920x / 930x
 * http://localhost:9200/_plugin/head/
   * for fast cluster state verification and mapping setup
* 1x Kibana
 * exposed port: 5601
 * sense and marvel plugin installed
   * http://localhost:5601/app/marvel
   * http://localhost:5601/app/sense
 * URI (to match uploaded sample):
````
http://localhost:5601/app/kibana#/discover?_g=(refreshInterval:(display:Off,pause:!f,value:0),time:(from:'2016-10-21T03:55:50.172Z',mode:absolute,to:'2016-10-21T03:58:26.371Z'))&_a=(columns:!(_source),index:'logstash-*',interval:auto,query:(query_string:(analyze_wildcard:!t,query:'*')),sort:!('@timestamp',desc))
````
* 1x Logstash for easy sample data upload
  * exposed ports:
   * 5000 - json filter
   * 5001 - raw
 * you can use .raw field for not_analyzed data
* 1x Fluentd
 * somehow not working correctly under load, docker logger can be used

````
docker run --log-driver=fluentd --log-opt fluentd-address=172.22.0.17:24224 python:alpine echo HELLO
````

## Spinup whole stack

```
docker-compose up -d
or
docker-compose up -d --remove-orphans

docker-compose down
```

## Mapping
* script for upload default no-mapping-strings, run elasticsearch/mapping/no_mapping.sh or see examples
* [Mapping examples](README_mapping.md)
* fluentd/templates/http-log-example.json

## Upload sample data via Logstash

```
nc localhost 5000 < samples/access_log
```
