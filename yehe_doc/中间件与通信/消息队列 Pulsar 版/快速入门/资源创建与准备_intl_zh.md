## 操作场景

该任务指导您通过 TDMQ Pulsar 版控制台创建集群和 Topic 等资源，了解运行一个客户端之前，控制台所需要进行的操作。

## 操作步骤

### 步骤一：新建集群并配置网络

1. 登录 [TDMQ Pulsar 版控制台](https://console.cloud.tencent.com/tdmq)，进入**集群管理**页面，选择目标地域。
2. 单击**新建集群**，创建一个集群。
3. 在创建好的集群中，单击操作列的**接入地址**。
   ![](https://qcloudimg.tencent-cloud.cn/raw/72d7e1f59410ced5ab00403406f29727.png) 
    接入地址获取方式如下：
   <dx-tabs>
   ::: 2.7.1及以上版本集群
   直接获取接入地址，如下图。
      ![](https://qcloudimg.tencent-cloud.cn/raw/cba9bfef826619335cf9ba9c4c8b0e5a.png)
   :::
   ::: 2.6.1版本集群
   在接入点列表页，单击**新建**，新建一个 VPC 接入点（和运行客户端的资源所在 VPC 一致即可）。
   :::
   </dx-tabs>

> ?更多集群相关介绍与操作请参考 [集群管理](https://intl.cloud.tencent.com/document/product/1110/42928)。

### 步骤二：创建命名空间

> ?若您的集群版本为2.6.1版本，则可以直接使用系统自动创建的 default 命名空间。更多命名空间相关介绍与操作请参考 [命名空间](https://intl.cloud.tencent.com/document/product/1110/42929)。

在 TDMQ Pulsar 版控制台的 **[命名空间](https://console.cloud.tencent.com/tdmq/env)** 页面，选择地域和刚刚创建好的集群，单击**新建**，创建一个命名空间。

![](https://qcloudimg.tencent-cloud.cn/raw/9f9eefdc535750ff0bca2d7720fcb5b1.png)

### 步骤三：创建角色并授权

1. 在 TDMQ Pulsar 版控制台的 **[角色管理](https://console.cloud.tencent.com/tdmq/role)** 页面，选择地域和刚刚创建好的集群，单击**新建**进入新建角色页面。
2. 填写角色名称和说明，单击**提交**完成角色创建。
3. 进入 **[命名空间](https://console.cloud.tencent.com/tdmq/env)** 页面，在刚刚创建的命名空间中，单击操作列的**配置权限**进入命名空间的权限列表。
4. 在配置权限页面，单击**添加角色**，将刚刚创建的角色添加进来，分配生产和消费的权限。
   ![](https://qcloudimg.tencent-cloud.cn/raw/2ff48a2715937e0436c101e4f631be95.png)
5. 看到下图即代表配置成功。
   ![](https://qcloudimg.tencent-cloud.cn/raw/4b756a7bf60bb50036805b9890fa4b1d.png)

### 步骤四：创建 Topic 和订阅关系

1. 在 **[Topic管理](https://console.cloud.tencent.com/tdmq/topic)** 页面，选择目标地域、当前集群和命名空间，单击**新建**，创建一个Topic。
2. 单击操作列的**新增订阅**，为刚刚新建好的 Topic 创建一个订阅关系。
3. 单击操作列的**更多**>**查看订阅**，可看到刚刚创建好的订阅。
   ![](https://qcloudimg.tencent-cloud.cn/raw/cbab46518844a44584530d2536d16ff6.png)
