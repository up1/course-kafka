## 2. Prometheus + Grafana
Administrator tools
* [ZooNavigator UI](https://github.com/elkozmon/zoonavigator)
* [Yahoo Kafka Manager](https://github.com/yahoo/kafka-manager)

Monitoring Tools
* [LinkedIn Kafka Monitor](https://github.com/linkedin/kafka-monitor)
* [Prometheus](https://prometheus.io/) + [Grafana](https://grafana.com/)


### Install [Prometheus](https://prometheus.io)
Start Prometheus server
```
$./prometheus
```
Open url=http://localhost:9090 in browser

### Install [Prometheus JMX Exporter](https://github.com/prometheus/jmx_exporter/)
* Download [JAR file](https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/0.12.0/jmx_prometheus_javaagent-0.12.0.jar)
* Download [Kafka configuration file](https://raw.githubusercontent.com/prometheus/jmx_exporter/master/example_configs/kafka-2_0_0.yml)

### Start Zookeeper with JMX exporter
```
$export PATH_TO_JMX=<your path>
$KAFKA_OPTS="-javaagent:$PATH_TO_JMX/jmx_prometheus_javaagent-0.12.0.jar=7071:$PATH_TO_JMX/kafka-2_0_0.yml" ./bin/zookeeper-server-start.sh config/zookeeper.properties
```
Open url=http://localhost:7071 in browser


### Start Kafka server with JMX exporter
```
$export PATH_TO_JMX=<your path>
$KAFKA_OPTS="-javaagent:$PATH_TO_JMX/jmx_prometheus_javaagent-0.12.0.jar=7072:$PATH_TO_JMX/kafka-2_0_0.yml" ./bin/kafka-server-start.sh config/server.properties
```

Open url=http://localhost:7072 in browser

### Start Producer with JMX exporter
```
$export PATH_TO_JMX=<your path>
$KAFKA_OPTS="-javaagent:$PATH_TO_JMX/jmx_prometheus_javaagent-0.12.0.jar=7073:$PATH_TO_JMX/kafka-2_0_0.yml" bin/kafka-console-producer.sh --broker-list localhost:9092 --topic demo01
```

Open url=http://localhost:7073 in browser

### Start Consumer with JMX exporter
```
$export PATH_TO_JMX=<your path>
$KAFKA_OPTS="-javaagent:$PATH_TO_JMX/jmx_prometheus_javaagent-0.12.0.jar=7074:$PATH_TO_JMX/kafka-2_0_0.yml" bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic demo01 --from-beginning
```

Open url=http://localhost:7074 in browser






