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
