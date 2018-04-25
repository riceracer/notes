## Set Env Variables

Setting this will make the commands below work. Update as needed.

```
export JMX_PORT=9999
export KAFKA_HOME=/opt/kafka
export KAFKA_SERVER=kafka:9092
export ZOOKEEPER_SERVER=zookeeper:2181
```

## Read topic with console consumer

    $KAFKA_HOME/bin/kafka-console-consumer.sh --bootstrap-server $KAFKA_SERVER --topic my-topic-name

* The JMX_PORT thing may or may not be necessary
* Other args:
    * ```--from-beginning```

## List topics

    $KAFKA_HOME/bin/kafka-topics.sh --zookeeper $ZOOKEEPER_SERVER --list

## Describe topic

Shows in sync replicas and status

    $KAFKA_HOME/bin/kafka-topics.sh --zookeeper=$ZOOKEEPER_SERVER --topic my-topic-name --describe

## Read topic-specific config

    $KAFKA_HOME/bin/kafka-configs.sh --zookeeper=$ZOOKEEPER_SERVER --entity-type topics --entity-name TOPIC_NAME --describe

## Set topic-specific config

* This examples sets max message bytes config to 1.5 MB

    $KAFKA_HOME/bin/kafka-configs.sh --zookeeper=$ZOOKEEPER_SERVER --entity-type topics --entity-name TOPIC_NAME --alter --add-config max.message.bytes=1500012

## Check kafka version

Currently kafka bin doesn't have a --version flag. Instead check version numbers in libs:
* First part of version number is scala version, second part is kafka version:
* kafka_2.12-1.0.0.jar -> scala 2.12, kafka 1.0.0

    ls  $KAFKA_HOME/libs/kafka_*
 
