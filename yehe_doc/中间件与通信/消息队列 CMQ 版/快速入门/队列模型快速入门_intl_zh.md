## 操作场景

本文为您介绍从零开始创建一个队列服务并使用 TCP SDK 进行收发消息测试的方法，帮助您快速了解客户端接入 TDMQ CMQ 版所需的基本操作。

## 前提条件

已 [注册腾讯云账号](https://intl.cloud.tencent.com/document/product/378/17985)。

## 操作步骤

### 步骤1：创建队列服务

1. 登录 [TDMQ CMQ 版控制台](https://console.cloud.tencent.com/tdmq/cmq-queue)。
2. 在左侧导航栏选择**队列服务**，选择地域后，单击**新建**，配置队列服务相关属性值。
<img src="https://qcloudimg.tencent-cloud.cn/raw/bca2e55dcc0172d192894f345fcfc291.png" width="550px">
 
 
   | 属性                   | 说明                                                         | 取值                                                         |
   | :--------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
   | <nobr>队列名称</nobr>               | QueueName，为队列的名称。                                    | 作为资源的唯一标识，调用 API 接口进行操作时，以 Queue name 为准，创建成功后无法修改。为了防止混淆，不允许创建大小写同名队列，请注意使用时严格区分大小写，并且不能以-retry和-dlq结尾。 |
   | 消息生命周期           | 队列的 msgRetentionSeconds 属性， 消息在本队列中的保留时间，从发送到该队列开始经过此参数指定的时间后，该消息会变得可被删除（不一定会被及时清除）。 | 单位：秒，有效值范围：60 - 1296000秒，即1分钟 - 15天。       |
   | 消息接收长轮询等待时间 | PollingWaitSeconds，长轮询等待时，一个消息消费请求只会在取到有效消息或长轮询超时时才返回响应，类似于Ajax请求的长轮询。 | 单位：秒。有效值范围：0 - 30秒。                             |
   | 取出消息隐藏时长       | 该项为队列的VisibilityTimeout属性，每条Message都有个默认的VisibilityTimeout，Worker在接收到消息后，timeout就开始计时了。如果Worker在timeout时间内没能处理完Message，那么消息就有可能被其他Worker接收到并处理。 | 单位：秒。有效值范围：1 - 43200秒，即1秒 - 12小时。          |
   | 死信队列               | 死信队列用于处理无法被正常消费的消息。达到最大重试次数后，若消费依然失败，则表明消费者在正常情况下无法正确地消费该消息，此时，队列不会立刻将消息丢弃，而是将其发送到该消费者对应的特殊队列中。 | -                                                            |
   | 堆积消息数量上限       | 该限制为单个队列，最大消息堆积个数（未被删除）。             | 单个队列的堆积消息上限为1亿条，最小值为1百万条。如需提升额度，请联系技术支持。 |
   | 消息回溯               | 若未开启“消息回溯”能力，则消费者已消费，且确认删除的消息，会立即删除，开启该功能时，须指定回溯的“可回溯周期”。 | “可回溯周期”的范围，必须小于等于消息的生命周期。建议将回溯周期与消息的生命周期设置为相同的值，便于定位问题。 |
   | 指定时间范围           | 当开启消息回溯后可配置时间范围项。控制台默认不开启。开启后时间默认跟消息生命周期设置相同值。 | 时间范围：1秒 - 15天，最大可回溯时间点 = 当前时间 - 设置的可回溯时间范围。消息生产时间在这个值之前的不可回溯。 |

3. 单击**提交**，在队列服务列表可以看到创建好的队列服务。

### 步骤2：使用 SDK 收发消息

1. [下载 Demo](https://github.com/tencentyun/cmq-java-tcp-sdk) 并解压。
2. 配置生产消息程序 ProducerDemo.java 参数。
   ```java
    Producer producer = new Producer();
           // 私有网络地址： http://{region}.mqadapter.cmq.tencentyun.com 支持腾讯云私有网络的云服务器内网访问
           // 公网地址：    https://cmq-{region}.public.tencenttdmq.com
           producer.setNameServerAddress("https://cmq-****");
           // 设置SecretId，在控制台上获取，必须设置
           producer.setSecretId("****");
           // 设置SecretKey，在控制台上获取，必须设置
           producer.setSecretKey("****");
           // 设置签名方式，可以不设置，默认为SHA1
           producer.setSignMethod(ClientConfig.SIGN_METHOD_SHA256);
           // 设置发送消息失败时，重试的次数，设置为0表示不重试，默认为2
           producer.setRetryTimesWhenSendFailed(3);
           // 设置请求超时时间， 默认3000ms
           producer.setRequestTimeoutMS(5000);
           // 消息发往的队列，在控制台创建
           String queue = "****";
   ```
   
	 
   | 参数                | 说明                                                         |
   | ------------------- | ------------------------------------------------------------ |
   | NameServerAddress   | API 调用地址，在 [TDMQ CMQ 版控制台](https://console.cloud.tencent.com/tdmq) 的**队列服务** > **API请求地址**处复制。<img src="https://qcloudimg.tencent-cloud.cn/raw/fc16b1951c00d63b0f86cf8f4c25691c.png" width="400px"> |
   | SecretId、SecretKey | 云 API 密钥，登录 [访问管理控制台](https://console.cloud.tencent.com/cam/overview)，在**访问密钥** > **API密钥管理**页面复制。![](https://qcloudimg.tencent-cloud.cn/raw/0def1c292b3dc79a320e3fc9921a979e.png) |
   | queue               | 队列名称，在 [TDMQ CMQ 版控制台](https://console.cloud.tencent.com/tdmq) 的**队列服务**列表页面获取。 |
   
3. 配置消费消息程序 SubscribeDemo.java 参数。

   ```java
   Consumer consumer = new Consumer();
           // 私有网络地址： http://{region}.mqadapter.cmq.tencentyun.com 支持腾讯云私有网络的云服务器内网访问
           // 公网地址：    https://cmq-{region}.public.tencenttdmq.com
           consumer.setNameServerAddress("http://cmq-****");
           // 设置SecretId，在控制台上获取，必须设置
           consumer.setSecretId("****");
           // 设置SecretKey，在控制台上获取，必须设置
           consumer.setSecretKey("****");
           // 设置签名方式，可以不设置，默认为SHA1
           consumer.setSignMethod(ClientConfig.SIGN_METHOD_SHA256);
           // 批量拉取时最大拉取消息数量，范围为1-16
           consumer.setBatchPullNumber(16);
           // 设置没有消息时等待时间，默认10s。可在consumer.receiveMsg等方法中传入具体的等待时间
           consumer.setPollingWaitSeconds(6);
           // 设置请求超时时间， 默认3000ms
           // 如果设置了没有消息时等待时间为6s，超时时间为5000ms，则最终超时时间为(6*1000+5000)ms
           consumer.setRequestTimeoutMS(5000);
   
           // 消息拉取的队列名称
           final String queue = "****";
   ```
   
   参数配置与生产消息程序相同。
   
4. 运行生产消息程序 ProducerDemo.java，运行成功结果如下。

	 ![](https://main.qcloudimg.com/raw/60deede4bafd476e6883f21a943f8fad.png)

5. 运行消费消息程序 ConsumerDemo.java，运行成功结果如下。

	 ![](https://main.qcloudimg.com/raw/91bfa8685a3ba390a117398a8e969095.png)

6. 在 [TDMQ CMQ 版控制台](https://console.cloud.tencent.com/tdmq) 的**队列服务** > **监控**页面观察监控数据。



