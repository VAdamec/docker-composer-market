
.PHONY: all build release

all: build release

build:
	cd graphite/; docker build -t vaclavadamec/metrics-graphite .
	cd grafana; docker build -t vaclavadamec/metrics-grafana .

release: build
	cd graphite/; docker push vaclavadamec/metrics-graphite
	cd grafana; docker push vaclavadamec/metrics-grafana
