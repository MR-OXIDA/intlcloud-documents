## Overview

This document describes how to access CKafka to receive/send messages with the SDK for Java through SASL_SSL on the public network.

An SSL certificate is mainly used to protect server-client communication. Once data is encrypted by the SSL certificate, it cannot be accessed via a private key but by the server.

## Prerequisites

- [Install JDK 1.8 or later](https://www.oracle.com/java/technologies/javase-downloads.html)
- [Install Maven 2.5 or later](http://maven.apache.org/download.cgi#)
- [Configure an ACL policy](https://intl.cloud.tencent.com/document/product/597/39084)
- [Download demo](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/javakafkademo/PUBLIC_SASL)
- [Download the SASL_SSL certificate](https://ckafka-public-certs-1255613487.cos.ap-guangzhou.myqcloud.com/ssl-certs/client.truststore.jks)

## Directions

### Step 1. Create resources in the console
1. Create an access point.
	1. On the **[Instance List](https://console.cloud.tencent.com/ckafka/index)** page in the CKafka console, click the target instance ID to enter the instance details page.
	2. In **Basic Info** > **Access Mode**, click **Add a routing policy**. In the pop-up window, select `Route Type: Public domain name access`, `Access Mode: SASL_SSL`.
![](https://qcloudimg.tencent-cloud.cn/raw/fb9e6cb8740ecff2f2c13c88a128c270.png)

2. Create a role.
On the **User Management** tab page, create a role and set the password.
![](https://qcloudimg.tencent-cloud.cn/raw/c9e06ace7d959ae91331a241c2126cc5.png)

3. Create a topic.
Create a topic on the **Topic Management** tab page as instructed in [Creating a topic](https://intl.cloud.tencent.com/document/product/597/32554).


### Step 2. Add the configuration file

1. Add the following dependencies to the `pom.xml` file:
```xml
<dependency>
   <dependency>
      <groupId>org.apache.kafka</groupId>
      <artifactId>kafka-clients</artifactId>
      <version>2.1.0</version>
   </dependency>
   <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
      <version>1.7.5</version>
   </dependency>
   <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-simple</artifactId>
      <version>1.6.4</version>
   </dependency>
</dependency>

```

2. Create a JAAS configuration file named `ckafka_client_jaas.conf` and modify it with the user created on the **User Management** tab page.
```properties
KafkaClient {
org.apache.kafka.common.security.plain.PlainLoginModule required
username="yourinstance#yourusername"
password="yourpassword";
};
```
>?Set `username` to a value in the format of `Instance ID` + `#` + `Configured username`, and `password` to a configured password.

3. Create a Kafka configuration file named `kafka.properties`.
```properties
## Configure the accessed network by copying the information in the **Network** column in the **Access Mode** section on the instance details** page in the console
bootstrap.servers=xx.xx.xx.xx:xxxx
## Configure the topic by copying the information on the **Topic Management** page in the console
topic=XXX
## Configure the consumer group as needed
group.id=XXX
## SASL configuration
java.security.auth.login.config.plain=/xxxx/ckafka_client_jaas.conf
## SSL certificate configuration, which takes effect when the access mode is specified as SASL_SSL
ssl.truststore.location=/xxxx/client.truststore.jks
ssl.truststore.password=5fi6R!M
ssl.endpoint.identification.algorithm=
```

| Parameter | Description |
| ------------------------------------- | ------------------------------------------------------------ |
| `bootstrap.servers`                      | Accessed network, which can be copied from the **Network** column in the **Access Mode** section in **Basic Info** on the instance details page in the console.<br/>![](https://qcloudimg.tencent-cloud.cn/raw/d1ce0a815917ed6375dde270d916bd9c.png) |
| `topic`                                  | Topic name, which can be copied from the **Topic Management** page in the console.<br/>![](https://main.qcloudimg.com/raw/1b34ab83490f228ba0683609e0202c54.png) |
| `group.id`                               | You can customize it. After the demo runs successfully, you can see the consumer on the **Consumer Group** page. |
| `java.security.auth.login.config.plain` | Enter the path of the JAAS configuration file `ckafka_client_jaas.conf`.              |
| `client.truststore.jks`                  | Certificate path that is required when the access mode is `SASL_SSL`.          |


4. Create a configuration file loading program named `CKafkaConfigurer.java`.
```java
public class CKafkaConfigurer {

    private static Properties properties;

    public static void configureSaslPlain() {
        //If you have used the `-D` parameter or another method to set the path, do not set it again here
        if (null == System.getProperty("java.security.auth.login.config")) {
            // Replace `XXX` with your own path
            System.setProperty("java.security.auth.login.config",
                    getCKafkaProperties().getProperty("java.security.auth.login.config.plain"));
        }
    }

    public synchronized static Properties getCKafkaProperties() {
        if (null != properties) {
            return properties;
        }
        //Obtain the content of the configuration file `kafka.properties`
        Properties kafkaProperties = new Properties();
        try {
            kafkaProperties.load(CKafkaProducerDemo.class.getClassLoader().getResourceAsStream("kafka.properties"));
        } catch (Exception e) {
            System.out.println("getCKafkaProperties error");
        }
        properties = kafkaProperties;
        return kafkaProperties;
    }
}
```

### Step 3. Send messages

1. Create a message sending program named `KafkaSaslProducerDemo.java`.
```java
   public class KafkaSaslProducerDemo {

   public static void main(String[] args) {
      //Set the path to the JAAS configuration file
      CKafkaConfigurer.configureSaslPlain();

      //Load `kafka.properties`
      Properties kafkaProperties = CKafkaConfigurer.getCKafkaProperties();

      Properties props = new Properties();
      //Set the access point. Obtain the access point of the corresponding topic via the console
      props.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG,
              kafkaProperties.getProperty("bootstrap.servers"));

      //
      //  Public network access through SASL_SSL
      //
      //  Access protocol
      props.put(CommonClientConfigs.SECURITY_PROTOCOL_CONFIG, "SASL_SSL");
      //  Select `PLAIN` for the SASL mechanism.
      props.put(SaslConfigs.SASL_MECHANISM, "PLAIN");
      //  SSL encryption
      props.put(SslConfigs.SSL_TRUSTSTORE_LOCATION_CONFIG, kafkaProperties.getProperty(SslConfigs.SSL_TRUSTSTORE_LOCATION_CONFIG));
      props.put(SslConfigs.SSL_TRUSTSTORE_PASSWORD_CONFIG, kafkaProperties.getProperty(SslConfigs.SSL_TRUSTSTORE_PASSWORD_CONFIG));
      props.put(SslConfigs.SSL_ENDPOINT_IDENTIFICATION_ALGORITHM_CONFIG,kafkaProperties.getProperty(SslConfigs.SSL_ENDPOINT_IDENTIFICATION_ALGORITHM_CONFIG));

      //Set the method for serializing Kafka messages
      props.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG,
              "org.apache.kafka.common.serialization.StringSerializer");
      props.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG,
              "org.apache.kafka.common.serialization.StringSerializer");
      //Set the maximum time to wait for a request
      props.put(ProducerConfig.MAX_BLOCK_MS_CONFIG, 30 * 1000);
      //Set the number of retries for the client
      props.put(ProducerConfig.RETRIES_CONFIG, 5);
      //Set the interval between retries for the client
      props.put(ProducerConfig.RECONNECT_BACKOFF_MS_CONFIG, 3000);
      //Create a producer object. Note: a producer object is thread-safe, and generally one producer object is sufficient for a process.
      KafkaProducer<String, String> producer = new KafkaProducer<>(props);

      //Create a Kafka message
      String topic = kafkaProperties.getProperty("topic"); //Topic of the message. Enter the topic you created in the console
      String value = "this is ckafka msg value"; //Content of the message

      try {
         //Batch obtaining future objects can speed up the process. Note that the batch size should not be too large.
         List<Future<RecordMetadata>> futures = new ArrayList<>(128);
         for (int i = 0; i < 100; i++) {
            //Send the message and obtain a future object
            ProducerRecord<String, String> kafkaMessage = new ProducerRecord<>(topic,
                    value + ": " + i);
            Future<RecordMetadata> metadataFuture = producer.send(kafkaMessage);
            futures.add(metadataFuture);

         }
         producer.flush();
         for (Future<RecordMetadata> future : futures) {
            //Sync the result that the future object is obtained
            RecordMetadata recordMetadata = future.get();
            System.out.println("Produce ok:" + recordMetadata.toString());
         }
      } catch (Exception e) {
         //If the sending still fails after client internal retries, the system needs to report and handle the error.
         System.out.println("error occurred");
      }
   }
}
```
2. Compile and run `KafkaSaslProducerDemo.java` to send messages.
   
3. View the execution result (output).
```bash
Produce ok:ckafka-topic-demo-0@198
Produce ok:ckafka-topic-demo-0@199
```
4. On the **Topic Management** tab page on the instance details page in the CKafka console, select the target topic, and click **More** > **Message Query** to view the message just sent.
![](https://main.qcloudimg.com/raw/417974c1d8df4a5ff409138e7c6b3def.png)



### Step 4. Consume messages

1. Create a program named `KafkaSaslConsumerDemo.java` for a single consumer to subscribe to messages.
```java
public class KafkaSaslConsumerDemo {

   public static void main(String[] args) {
      //Set the path to the JAAS configuration file
      CKafkaConfigurer.configureSaslPlain();

      //Load `kafka.properties`
      Properties kafkaProperties = CKafkaConfigurer.getCKafkaProperties();

      Properties props = new Properties();
      //Set the access point. Obtain the access point of the corresponding topic via the console
      props.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG,
              kafkaProperties.getProperty("bootstrap.servers"));

      //
      //  Public network access through SASL_SSL
      //
      //  Access protocol
      props.put(CommonClientConfigs.SECURITY_PROTOCOL_CONFIG, "SASL_SSL");
      //  Select `PLAIN` for the SASL mechanism.
      props.put(SaslConfigs.SASL_MECHANISM, "PLAIN");
      //  SSL encryption
      props.put(SslConfigs.SSL_TRUSTSTORE_LOCATION_CONFIG, kafkaProperties.getProperty(SslConfigs.SSL_TRUSTSTORE_LOCATION_CONFIG));
      props.put(SslConfigs.SSL_TRUSTSTORE_PASSWORD_CONFIG, kafkaProperties.getProperty(SslConfigs.SSL_TRUSTSTORE_PASSWORD_CONFIG));
      props.put(SslConfigs.SSL_ENDPOINT_IDENTIFICATION_ALGORITHM_CONFIG,kafkaProperties.getProperty(SslConfigs.SSL_ENDPOINT_IDENTIFICATION_ALGORITHM_CONFIG));

      //Set the maximum interval between two polls
      //If the consumer does not return a heartbeat message within the interval, the broker determines that the consumer is not alive. the broker removes the consumer from the consumer group and triggers rebalancing. The default value is 30s.
      props.put(ConsumerConfig.SESSION_TIMEOUT_MS_CONFIG, 30000);
      //Set the maximum number of messages that can be polled at a time
      //Do not set this parameter to an excessively large value. If polled messages are not all consumed before the next poll starts, load balancing is triggered and lagging occurs.
      props.put(ConsumerConfig.MAX_POLL_RECORDS_CONFIG, 30);
      //Set the method for deserializing messages.
      props.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG,
              "org.apache.kafka.common.serialization.StringDeserializer");
      props.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG,
              "org.apache.kafka.common.serialization.StringDeserializer");
      //Set the consumer group of the current consumer instance after you apply for one in the console
      //The instances in the same consumer group consume messages in load balancing mode
      props.put(ConsumerConfig.GROUP_ID_CONFIG, kafkaProperties.getProperty("group.id"));
      //Create a consumer object, which means generating a consumer instance.
      KafkaConsumer<String, String> consumer = new KafkaConsumer<String, String>(props);
      //Set one or more topics to which the consumer group subscribes
      //You are advised to subscribe to the same topics if the values of GROUP_ID_CONFIG are the same
      List<String> subscribedTopics = new ArrayList<String>();
      //If you want to subscribe to multiple topics, add the topics here
      //You must create the topics in the console in advance
      String topicStr = kafkaProperties.getProperty("topic");
      String[] topics = topicStr.split(",");
      for (String topic : topics) {
         subscribedTopics.add(topic.trim());
      }
      consumer.subscribe(subscribedTopics);

      //Consume messages in loop
      while (true) {
         try {
            ConsumerRecords<String, String> records = consumer.poll(1000);
            //All messages must be consumed before the next poll, and the total duration cannot exceed the timeout interval specified by `SESSION_TIMEOUT_MS_CONFIG`
            for (ConsumerRecord<String, String> record : records) {
               System.out.println(
                       String.format("Consume partition:%d offset:%d", record.partition(),
                               record.offset()));
            }
         } catch (Exception e) {
            System.out.println("consumer error!");
         }
      }
   }
}
```
2. Compile and run `KafkaSaslConsumerDemo.java` to consume messages.
   
3. View the execution result (output).
```bash
   Consume partition:0 offset:298
   Consume partition:0 offset:299   
```
4. On the **Consumer Group** page in the Ckafka console, select the corresponding consumer group name, enter the topic name, and click **Query Details** to view the consumption details.
![](https://main.qcloudimg.com/raw/22b1e4dd27a79cb96c76f01f2aa7e212.png)
