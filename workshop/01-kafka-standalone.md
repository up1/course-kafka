### 1. Start Zookeeper server
```
$bin/zookeeper-server-start.sh config/zookeeper.properties
```

### 2. Start Kafka server
```
$bin/kafka-server-start.sh config/server.properties
```

### 3. Create a topic
```
$bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic demo01

// List of topics
$bin/kafka-topics.sh --list --bootstrap-server localhost:9092

// Describe a topic
$bin/kafka-topics.sh --describe --bootstrap-server localhost:9092
```

### 4. Producer : send message to topic
```
$bin/kafka-console-producer.sh --broker-list localhost:9092 --topic demo01
```

### 5. Consumer : start 
```
$bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic demo01 --from-beginning
```

### Others
```
// Delete topic
$bin/kafka-topics.sh  --bootstrap-server localhost:9092 --delete --topic demo01
```

