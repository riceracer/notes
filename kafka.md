## Set Env Variables

Setting this will make the commands below work. Update as needed.

```
export JMX_PORT=9999
export KAFKA_HOME=/opt/kafka
export KAFKA_SERVER=kafka:9092
export ZOOKEEPER_SERVER=zookeeper:2181
```

## List topics

First line is vanilla kafka, second is confluent kafka.

    $KAFKA_HOME/bin/kafka-topics.sh --zookeeper $ZOOKEEPER_SERVER --list
    $KAFKA_HOME/bin/kafka-topics --zookeeper $ZOOKEEPER_SERVER --list

## Read topic with console consumer

    $KAFKA_HOME/bin/kafka-console-consumer.sh --bootstrap-server $KAFKA_SERVER --topic my-topic-name
    $KAFKA_HOME/bin/kafka-console-consumer --bootstrap-server $KAFKA_SERVER --topic my-topic-name

* The JMX_PORT thing may or may not be necessary
* Other args:
    * ```--from-beginning```
    * ```--property "print.key=true"``` - include key in the output

## Describe topic

Shows in sync replicas and status

    $KAFKA_HOME/bin/kafka-topics.sh --zookeeper=$ZOOKEEPER_SERVER --describe --topic my-topic-name 
    $KAFKA_HOME/bin/kafka-topics --zookeeper=$ZOOKEEPER_SERVER --describe --topic my-topic-name

## Read topic-specific config

    $KAFKA_HOME/bin/kafka-configs.sh --zookeeper=$ZOOKEEPER_SERVER --entity-type topics --entity-name TOPIC_NAME --describe
    $KAFKA_HOME/bin/kafka-configs --zookeeper=$ZOOKEEPER_SERVER --entity-type topics --entity-name TOPIC_NAME --describe

## Set topic-specific config

* This examples sets max message bytes config to 1.5 MB

```
$KAFKA_HOME/bin/kafka-configs.sh --zookeeper=$ZOOKEEPER_SERVER --entity-type topics --entity-name TOPIC_NAME --alter --add-config max.message.bytes=1500012
$KAFKA_HOME/bin/kafka-configs --zookeeper=$ZOOKEEPER_SERVER --entity-type topics --entity-name TOPIC_NAME --alter --add-config max.message.bytes=1500012
```

## Check kafka version

Currently kafka bin doesn't have a --version flag. Instead check version numbers in libs:
* First part of version number is scala version, second part is kafka version:
* kafka_2.12-1.0.0.jar -> scala 2.12, kafka 1.0.0

```
ls  $KAFKA_HOME/libs/kafka_*
``` 

## List Consumer Groups

(This does not list zookeeper-based consumers)

```
$KAFKA_HOME/bin/kafka-consumer-groups.sh --bootstrap-server $KAFKA_SERVER --list
$KAFKA_HOME/bin/kafka-consumer-groups --bootstrap-server $KAFKA_SERVER --list
```

## Describe consumer group (show per-partition lag and offsets)

```
$KAFKA_HOME/bin/kafka-consumer-groups.sh --bootstrap-server $KAFKA_SERVER --describe --group CONSUMER-GROUP
$KAFKA_HOME/bin/kafka-consumer-groups --bootstrap-server $KAFKA_SERVER --describe --group CONSUMER-GROUP
```
