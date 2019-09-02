## 1. Using JMX with jconsole in JDK

### Start Zookeeper with JMX
```
$JMX_PORT=10100 bin/zookeeper-server-start.sh config/zookeeper.properties

// Open JMX Console
$jconsole 127.0.0.1:10100
```

### Start Kafka server with expose JMX port
```
$JMX_PORT=10101 ./bin/kafka-server-start.sh config/server.properties

// Open JMX Console
$jconsole 127.0.0.1:10101
```

### Start Producer with JMX
```
$JMX_PORT=10102 bin/kafka-console-producer.sh --broker-list localhost:9092 --topic demo01

// Open JMX Console
$jconsole 127.0.0.1:10102
```

### Start Consumer with JMX
```
$JMX_PORT=10103 bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic demo01 --from-beginning

// Open JMX Console
$jconsole 127.0.0.1:10103
```