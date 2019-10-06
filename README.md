# Get to know Kafka

Learn the basics of Kafka with different language implementations

## Kafka CLI Commands

1. Start Zookeeper server (Step 1)

```
./bin/zookeeper-server-start.sh config/zookeeper.properties
```

2. Start Kafka server (Step 2)

```
./bin/kafka-server-start.sh config/server.properties
```

3. Topics

    3.1 Create a topic

    ```
    ./bin/kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic <topic_name> --create --partitions <no_of_partitions> --replication-factor <no_of_replication-factor>
    ```

    For example
    ```
     ./bin/kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic my_topic --create --partitions 3 --replication-factor 1
    ```

    3.2 List the topics

    ```
    ./bin/kafka-topics.sh --zookeeper 127.0.0.1:2181 --list
    ```

    3.3 Describe details of the topic

    ```
    ./bin/kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic <topic_name> --describe
    ```

    3.4 Delete a topic

    ```
    ./bin/kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic <topic_name> --delete
    ```

4. Producer

    4.1 Write with producer with default properties

    ```
    ./bin/kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic <topic_name>
    ```

    Above command will show `>` and expect input message from user as example show below
    
    ```
    > Hello World!
    > Kafka is awesome messaging system and I'm learning it
    > Will implement in Java, Python and Goland
    Press Ctrl+C to come out of the prompt
    ```

    4.2 Add properties and override default

    ```
    ./bin/kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic <topic_name> --producer-property ask=all
    ```

    **Notes:**
    
    * Write with producer on topic which does not exist, new topic (with 1 partition and 1 replication-factor) will get created with warning `LEADER_NOT_AVAILABLE`. This is not recommended.
    * We can also override default properties in `config/server.properties` file.

5. Consumer

    5.1 Read message from a topic with consumer at real time

    ```
    ./bin/kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic <topic_name>
    ```

    **Notes:**
    
    * Consumer will read all the new message from the topic at real time.

    5.2 Read all message from a topic with consumer

    ```
    ./bin/kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic <topic_name> --from-beginning
    ```

    5.3 Read message from a topic with consumer group

    ```
    ./bin/kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic <topic_name> --group <group_name>
    ```

    For example

    ```
    ./bin/kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my_first_consumer_group
    ```

    **Notes:**
    
    * We can read message with multiple consumer with same group and Kafka will load balance between these consumers

    5.4 List all consumer groups

    ```
    ./bin/kafka-consumer-groups.sh --bootstrap-server 127.0.0.1:9092 --list
    ```

    5.5 Describe details of the consumer group

    ```
    ./bin/kafka-consumer-groups.sh --bootstrap-server 127.0.0.1:9092 --describe --group <group_name>
    ```

    5.6 Reset offsets for topic with consumer group

    ```
    ./bin/kafka-consumer-groups.sh --bootstrap-server 127.0.0.1:9092 --group <group_name> --reset-offsets --to-earliest --execute --topic <topic_name>
    ```