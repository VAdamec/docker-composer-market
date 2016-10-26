
.PHONY: all build release

all: build release

build:
	cd elasticsearch/; docker build -t vaclavadamec/docker-composer-market:elasticsearch .
	cd logstash; docker build -t vaclavadamec/docker-composer-market:logstash .
	cd kibana; docker build -t vaclavadamec/docker-composer-market:kibana .
	cd fluentd; docker build -t vaclavadamec/docker-composer-market:fluentd .

release: build
	cd elasticsearch/; docker push vaclavadamec/docker-composer-market:elasticsearch
	cd logstash; docker push vaclavadamec/docker-composer-market:logstash
	cd kibana; docker push vaclavadamec/docker-composer-market:kibana
	cd fluentd; docker push vaclavadamec/docker-composer-market:fluentd
