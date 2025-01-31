Grafana 可视化服务支持添加告警通道，告警支持通过 Webhook、邮件、短信和电话等多种形式通知用户。

## 操作前提
1. 登录 [Grafana 可视化服务控制台](https://console.cloud.tencent.com/monitor/grafana)。
2. 在实例列表中，找到对应的实例，单击**实例 ID**。

## 操作步骤
1. 进入实例详情页，单击左侧列表的**告警通道**。
2. 在“告警通道”管理页，单击左上角的**新建**。
3. 在“新建告警”页，输入通道名称，选择或创建通知模板。如需创建通知模板请参考 [新建通知模板](https://intl.cloud.tencent.com/zh/document/product/248/38922)。
   ![](https://qcloudimg.tencent-cloud.cn/raw/cfbd2902effaa7fb77a5222ebf5c7340.png)
4. 创建完后，您可以返回告警通道创建页面，重新选择新建的模板，并单击**保存**，实例重建后即可在 Grafana Alert Notification Channel 页面中查看。
5. 在配置 Grafana 告警时，在 Notification Channel 配置块选择您添加的告警通道名，即可完成配置。
![](https://qcloudimg.tencent-cloud.cn/raw/840edc2f4a0cac66f1dade64d1ac467f.png)

