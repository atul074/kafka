# kafka

npm install -g yarn
yarn init  
yarn add kafkajs

# Commands

Start Zookeper Container and expose PORT 2181.
docker run -p 2181:2181 zookeeper
Start Kafka Container, expose PORT 9092 and setup ENV variables.
docker run -p 9092:9092 \
-e KAFKA_ZOOKEEPER_CONNECT=<PRIVATE_IP>:2181 \
-e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://<PRIVATE_IP>:9092 \
-e KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR=1 \
confluentinc/cp-kafka



# output 
# producer-
atultandan@atul-tandans-MacBook-Air kafka % node producer.js
{"level":"WARN","timestamp":"2025-01-26T10:00:49.921Z","logger":"kafkajs","message":"KafkaJS v2.0.0 switched default partitioner. To retain the same partitioning behavior as in previous versions, create the producer with the option \"createPartitioner: Partitioners.LegacyPartitioner\". See the migration guide at https://kafka.js.org/docs/migration-guide-v2.0.0#producer-new-default-partitioner for details. Silence this warning by setting the environment variable \"KAFKAJS_NO_PARTITIONER_WARNING=1\""}
Connecting Producer
(node:20032) TimeoutNegativeWarning: -1737885649935 is a negative number.
Timeout duration was set to 1.
(Use `node --trace-warnings ...` to show where the warning was created)
Producer Connected Successfully
> arjun north


# consumer-
atultandan@atul-tandans-MacBook-Air kafka % node consumer.js atul-1
(node:20503) TimeoutNegativeWarning: -1737885678859 is a negative number.
Timeout duration was set to 1.
(Use `node --trace-warnings ...` to show where the warning was created)
{"level":"INFO","timestamp":"2025-01-26T10:01:18.864Z","logger":"kafkajs","message":"[Consumer] Starting","groupId":"atul-1"}
{"level":"ERROR","timestamp":"2025-01-26T10:01:18.894Z","logger":"kafkajs","message":"[Connection] Response GroupCoordinator(key: 10, version: 2)","broker":"10.68.2.246:9092","clientId":"my-app","error":"The group coordinator is not available","correlationId":2,"size":55}
{"level":"INFO","timestamp":"2025-01-26T10:01:22.279Z","logger":"kafkajs","message":"[ConsumerGroup] Consumer has joined the group","groupId":"atul-1","memberId":"my-app-d6a628b2-9fc8-404f-8ad0-1e30eed3a3a5","leaderId":"my-app-d6a628b2-9fc8-404f-8ad0-1e30eed3a3a5","isLeader":true,"memberAssignment":{"rider-updates":[0,1]},"groupProtocol":"RoundRobinAssigner","duration":3413}
atul-1: [rider-updates]: PART:0: {"name":"arjun","location":"north"}


# keypoint 
Summary of Kafka Workflow

Producer Workflow:
Sends messages to a topic.
Kafka assigns the message to a partition.
The partition leader writes the message to its log and replicates it to followers.

Broker Workflow:
Stores partitions of topics.
Manages replication and leader election.
Serves data to consumers and producers.

Consumer Workflow:
Pulls messages from topic partitions.
Within a consumer group, each partition is consumed by only one consumer.

Scaling:
Add partitions for more parallelism.
Add consumers for faster message processing.
Add brokers to increase storage and load distribution.