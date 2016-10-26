# Usage

````
 docker-compose up
...
 docker-compose down
````

## Graphite + Carbon-cache

- `8888` the graphite web interface admin/admin
- `2003` the carbon-cache line receiver (the standard graphite protocol)
- `2004` the carbon-cache pickle receiver
- `7002` the carbon-cache query port (used by the web interface)

## Kibana
- `3000` Kibana4 admin/admin
- add new data sources

````
Graphite
http://172.23.0.10:80
proxy
````

# Send some fake stats to Graphite
````
while true
do
  echo "local.random.diceroll $(((RANDOM % 10) + 1)) `date +%s`" | nc -c localhost 2003
done
<CTL-C>
````

# Create new dashboard with graph from new datasource
* ````local.random.diceroll````
