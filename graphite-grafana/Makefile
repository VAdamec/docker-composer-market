
.PHONY: all build release

all: build release

build:
	cd graphite/; docker build -t vaclavadamec/docker-composer-market:graphite .
	cd grafana; docker build -t vaclavadamec/docker-composer-market:grafana .

release: build
	cd graphite/; docker push vaclavadamec/docker-composer-market:graphite
	cd grafana; docker push vaclavadamec/docker-composer-market:grafana
