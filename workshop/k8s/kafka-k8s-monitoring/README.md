# kafka-k8s-monitoring

## Create ZooKeeper server
```
$kubectl create ns demo

$kubectl -n demo apply -f setup/zookeeper.yaml
$kubectl get po --namespace demo
$kubectl get svc --namespace demo
```

## Create Kafka server
```
$kubectl -n demo apply -f setup/influxdb.yaml
$kubectl -n demo apply -f setup/kafka.yaml
$kubectl get po --namespace demo
$kubectl get svc --namespace demo
$kubectl get configmap --namespace demo
```
## Create Grafana server
```
$kubectl -n demo apply -f setup/grafana.yaml
$kubectl get po --namespace demo
$kubectl get deployment --namespace demo
$kubectl get secret --namespace demo
```

## Grafana
```
$kubectl -n demo port-forward $(kubectl -n demo get po -lname=grafana -o jsonpath="{.items[0].metadata.name}") 3000:3000
```

## Influx db as Data source
```
$kubectl -n demo port-forward $(kubectl -n demo get po -lname=influxdb -o jsonpath="{.items[0].metadata.name}") 8086:8086
```

Add datasource named "influxdb-kafka"
* user=admin
* pass=adminadmin
* influx server=http://127.0.0.1:8086
* db name=kafka

## Load sample data to Kafka server
```
$kubectl -n demo apply -f job/kafka-load-generator.yaml
```

## Checking we are getting data (consumer)
```
$kubectl -n demo run --rm -it kafkacatjob --image=solsson/kafkacat --restart=OnFailure --command -- kafkacat -C -b kafka -t orders -o -10 -e
```

## Start consumer in console
```
$kubectl -n demo apply -f consumer/console-consumer.yaml
```

## Prometheus

```
$kubectl -n demo apply -f setup/prometheus.yaml
$kubectl -n demo port-forward $(kubectl -n demo get po -lname=prometheus -o jsonpath="{.items[0].metadata.name}") 9090:9090
```



## Create all-in-one
```
kubectl -n demo create -f setup/zookeeper.yaml
kubectl -n demo create -f setup/influxdb.yaml
kubectl -n demo create -f setup/kafka.yaml
kubectl -n demo create -f setup/grafana.yaml
kubectl -n demo create -f setup/prometheus.yaml
kubectl -n demo create -f job/kafka-load-generator.yaml
```

## Delete all-in-one
```
kubectl -n demo delete -f setup/zookeeper.yaml
kubectl -n demo delete -f setup/influxdb.yaml
kubectl -n demo delete -f setup/kafka.yaml
kubectl -n demo delete -f setup/grafana.yaml
kubectl -n demo delete -f setup/prometheus.yaml
kubectl -n demo delete -f job/kafka-load-generator.yaml
```

## Reference Websites
* [Apache Kafka 2.3.0](https://kafka.apache.org)
* [JMX Trans](https://github.com/jmxtrans/jmxtrans)
* [JMX Exporter for Prometheus](https://github.com/prometheus/jmx_exporter)
* [InfluxDB](https://github.com/influxdata/influxdb)
* [Prometheus](https://github.com/prometheus/prometheus)
* [Grafana](https://grafana.com/)
* https://github.com/wurstmeister/kafka-docker
* https://github.com/jeroenr/kafka-k8s-monitoring

