# ELK sample cluster setup on static IPs
* Sample data are around 2016-10-21T05:59:07 (or get some newer from util-backup server or ...)
* Simple Makefile for change prebuild images in Registry (build and push)
  * ```make build``` - just build to local cache
  * ```make all``` - build and push to registry

# Structure
* README.md - this document
* README_workshop.md - workshop description
* README_mapping.md - mapping examples and how to use them/work with them
* README_api_usage.md - small examples about API usage, index recovery, backups, ..., curator

## Stack
* 1x Fluentd ```NEED TO BE RUN FIRST``` see how to run this stack
 * not working correctly under load, but as docker logger it can be used
 * logging containers outputs to ELK
 * index ```platform*```


* 5x ELK in cluster (2x master node, 3x data nodes)
 * exposed ports:
   * 920x / 930x
 * http://localhost:9200/_plugin/head/
   * for fast cluster state verification and mapping setup


* 1x Kibana
 * exposed port: 5601
 * http://localhost:5601/app/kibana
 * consulate installed + example
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
 * index: ```logstash*```

## Spinup whole stack
 1. Start stack
````bash
./_start.sh
````
 2. Stop stack and remove artefacts
````bash
./_stop.sh
````
