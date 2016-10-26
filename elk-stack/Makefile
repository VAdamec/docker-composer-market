
.PHONY: all build release

all: build release

build:
	cd elasticsearch/; docker build -t vaclavadamec/elkstack-elasticsearch .
	cd logstash; docker build -t vaclavadamec/elkstack-logstash .
	cd kibana; docker build -t vaclavadamec/elkstack-kibana .
	cd fluentd; docker build -t vaclavadamec/elkstack-fluentd .

release: build
	cd elasticsearch/; docker push vaclavadamec/elkstack-elasticsearch
	cd logstash; docker push vaclavadamec/elkstack-logstash
	cd kibana; docker push vaclavadamec/elkstack-kibana
	cd fluentd; docker push vaclavadamec/elkstack-fluentd
