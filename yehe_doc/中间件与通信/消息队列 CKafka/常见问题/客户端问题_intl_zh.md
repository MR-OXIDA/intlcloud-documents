### Kafka Console 客户端测试时看不到数据如何处理？

- 消费者采用 latest 时候只会获取最后的数据，需要同时保持生产才可以看到相应数据。
- 改为 earliest 方式消费数据。

### 新接入客户端时生产或消费错误?

- 检查 telnet 是否通（网络问题，是否 Kafka 和生产者在相同网络环境下）。
- 访问的 vip - port 是否配置正确。
- topic 白名单是否开启，如果开启需要配置正确的 IP 才能访问。




### 客户端生产消息如何保证在同一分区是有序的？

- 如果 Topic 只有一个分区，那么消息会根据服务端收到的数据顺序存储，则数据就是分区有序的。
- 如果 Topic 有多个分区，可以在生产端指定这一类消息的 key，这类消息都用相同的 key 进行消息发送，CKafka 会根据 key 哈希取模选取其中一个分区进行存储，由于一个分区只能由一个消费者进行监听消费，此时消息就具有消息消费的顺序性了。

对于单个生产者来说，对单个分区的生产，是保持有序的。



### 客户端生产消息一般会与 Broker 建立多少个连接？

从单个客户端实例（new 一个 Producer 对象的角度）来看，和所有服务端建立的连接总数公式如下：总连接数 = 1~n（n 是 Broker 的数量）。

每个 Java Producer 端管理 TCP 连接的方式如下：

1. KafkaProducer 实例创建时启动 Sender 线程，从而创建与 bootstrap.servers 中所有 Broker 的 TCP 连接。
2. KafkaProducer 实例首次更新元数据信息之后，还会再次创建与集群中所有 Broker 的 TCP 连接。
3. 如果 Producer 端发送消息到某台 Broker 时发现没有与该 Broke r的 TCP 连接，那么也会立即创建连接。
4. 如果设置 Producer 端 connections.max.idle.ms 参数大于0，则步骤1中创建的 TCP 连接会被自动关闭；默认情况下该参数值是9分钟，即如果在9分钟内没有任何请求“流过”某个 TCP 连接，那么 Kafka 会主动帮您把该 TCP 连接关闭。如果设置该参数=-1，那么步骤1中创建的 TCP 连接将无法被关闭，从而成为“僵尸”连接。



### 使用客户端发送消息后，如何确定是否发送成功？

大部分客户端在发送之后，会返回 Callback 或者 Future，如果回调成功，则说明消息发送成功。

您还可以在控制台通过以下方式确认消息发送是否正常：

- 查看 Topic 的分区状态，可以实时看到各个分区的消息数量。
- 查看 Topic的 流量监控，可以看到生产消息的流量曲线。

可以通过打印 send 方法返回的 partition 和分区信息来确认是否成功：

```java
Future<RecordMetadata> future = producer.send(new ProducerRecord<>(topic, messageKey, messageStr));
RecordMetadata recordMetadata = future.get();
log.info("partition: {}", recordMetadata.partition());
log.info("offset: {}", recordMetadata.offset());
```

如果能够打印出 partition 和 offset，则表示当前发送的消息在服务端已经被正确保存。此时可以通过消息查询的工具去查询相关位点的消息即可。
如果打印不出 partition 和 offset，则表示消息没有被服务端保存，客户端需要重试。

 ![](https://main.qcloudimg.com/raw/417974c1d8df4a5ff409138e7c6b3def.png)
