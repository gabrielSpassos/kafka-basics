# Kafka Basics

### Example

* [Download](https://www.apache.org/dyn/closer.cgi?path=/kafka/2.3.0/kafka_2.12-2.3.0.tgz)

* Start Zookeeper

bin/zookeeper-server-start.sh config/zookeeper.properties

* Start Broker 0

bin/kafka-server-start.sh config/server-0.properties

* Start Broker 1

bin/kafka-server-start.sh config/server-1.properties

* Start Broker 2

bin/kafka-server-start.sh config/server-2.properties

* Create topic with replication of 3

bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 3 --partitions 5 --topic my-replicated-topic

* List topics

bin/kafka-topics.sh --list --bootstrap-server localhost:9092

* Describe topic

bin/kafka-topics.sh --describe --bootstrap-server localhost:9092 --topic my-replicated-topic

* Create Producer

bin/kafka-console-producer.sh --broker-list localhost:9092 --topic my-replicated-topic

* Create Consumer

bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic my-replicated-topic --from-beginning --consumer-property group.id=serviceA

* Create Consumers with other group

bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic my-replicated-topic --from-beginning --consumer-property group.id=serviceB

* Get PID from leader

ps aux | grep server-$.properties

* Kill the leader

sudo kill -9 $PID

* List Consumers

bin/kafka-consumer-groups.sh --list --bootstrap-server localhost:9092

* Describe Consumer Group

bin/kafka-consumer-groups.sh --describe --group serviceA --bootstrap-server localhost:9092

### Delete topics

* Add this to server-$.properties

```
### Delete Topic
delete.topic.enable=true
```
* Delete

bin/kafka-topics.sh --zookeeper localhost:2181 --delete --topic my-replicated-topic
