# Kafka Basics for Windowns

### Example

* [Download](https://www.apache.org/dyn/closer.cgi?path=/kafka/2.3.0/kafka_2.12-2.3.0.tgz)

* Start Zookeeper

```
bin/windows/zookeeper-server-start.bat config/zookeeper.properties
```

* Start Broker 1

```
bin/windows/kafka-server-start.bat config/server-1.properties
```

* Start Broker 2

```
bin/windows/kafka-server-start.bat config/server-2.properties
```

* Start Broker 3

```
bin/windows/kafka-server-start.bat config/server-3.properties
```

<details>
  <summary>Detail to start brokers</summary>
  
  Change `broker.id=${id}`, `listeners=PLAINTEXT://:${port}`, `log.dirs=/tmp/kafka-logs-${id}` at `server.properties` to a different number for each broker. 
</details>

* Create topic with replication of 3

```
bin/windows/kafka-topics.bat --create --bootstrap-server localhost:9092,localhost:9093,localhost:9094 --replication-factor 3 --partitions 5 --topic my-replicated-topic
```

* List topics

```
bin/windows/kafka-topics.bat --list --bootstrap-server localhost:9092,localhost:9093,localhost:9094
```

* Describe topic

```
bin/windows/kafka-topics.bat --describe --bootstrap-server localhost:9092,localhost:9093,localhost:9094 --topic my-replicated-topic
```

* Create Producer

```
bin/windows/kafka-console-producer.bat --broker-list localhost:9092,localhost:9093,localhost:9094 --topic my-replicated-topic
```

* Create Consumer

```
bin/windows/kafka-console-consumer.bat --bootstrap-server localhost:9092,localhost:9093,localhost:9094 --topic my-replicated-topic --from-beginning --consumer-property group.id=serviceA
```

* Create Consumers with other group

```
bin/windows/kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic my-replicated-topic --from-beginning --consumer-property group.id=serviceB
```

* Get PID from leader

```
ps aux | grep server-$.properties
```

* Kill the leader

```
sudo kill -9 $PID
```

* List Consumers

```
bin/windows/kafka-consumer-groups.bat --list --bootstrap-server localhost:9092
```

* Describe Consumer Group

```
bin/windows/kafka-consumer-groups.bat --describe --group serviceA --bootstrap-server localhost:9092
```

### Delete topics

* Add this to server-$.properties

```
### Delete Topic
delete.topic.enable=true
```
* Delete

```
bin/windows/kafka-topics.bat --zookeeper localhost:2181 --delete --topic my-replicated-topic
```
