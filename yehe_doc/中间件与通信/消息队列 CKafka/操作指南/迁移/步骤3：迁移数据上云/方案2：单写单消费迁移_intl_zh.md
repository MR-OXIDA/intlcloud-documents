## 操作场景

本文主要介绍使用单写单消费方案将自建 Kafka 集群的数据迁移到 CKafka 中的方法。

## 前提条件    

- 已 [购买云上 CKafka 实例](https://intl.cloud.tencent.com/document/product/597/41379)。
- 已 [迁移 Topic 上云](https://intl.cloud.tencent.com/document/product/597/41380)。

## 操作步骤

保证消息有序性的前提是严格控制单个消费者来消费数据，因此对于切换的时间节点要求较高。

单写单消费的方式简单清晰便于操作，但是 在生产切到新集群后，旧消费切到新集群之前，新集群会存在一定量的堆积。

其迁移步骤如下所示：![](https://main.qcloudimg.com/raw/a24b388a3259dfe609e94ed14037c862.png)

1. 切换生产流，生产者将数据生产到 CKafka 实例。
   修改 broker-list 中的 IP 为 CKafka 实例的接入网络，在控制台的实例详情页面**接入方式**模块的网络列复制；topicName 为 CKafka 实例中的 Topic 名称。
```bash
 ./kafka-console-producer.sh --broker-list xxx.xxx.xxx.xxx:9092 --topic topicName
```

2. 原有消费者无需做配置，持续消费自建 Kafka 集群的数据，直到消费完成。

3. 原有消费者在消费完成时，通过以下配置切换到新 CKafka 集群消费 CKafka 集群的数据。（单个消费者消费数据，保证消息的有序性）新增消费者，需要配置 `--bootstrap-server` 中的 IP 为 CKafka 实例的接入网络：
>?如果消费者为云服务器，此处也可以继续使用原有消费者进行消费。
>
```bash
./kafka-console-consumer.sh --bootstrap-server xxx.xxx.xxx.xxx:9092 --from-beginning --new-consumer --topic topicName --consumer.config ../config/consumer.properties
```

4. 切换后的消费者持续消费 CKafka 集群中的数据，迁移完毕（如果消费者为云服务器，此处也可以继续使用原有消费者进行消费）。

>!上文给出的是测试命令，正式业务的运行只需要修改相应应用程序配置的 broker 地址，然后重启相应的应用即可。
