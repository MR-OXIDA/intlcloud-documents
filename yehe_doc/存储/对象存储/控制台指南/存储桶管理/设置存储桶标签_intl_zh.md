## 简介

存储桶标签是一个键值对（key = value），由标签的键（key）和标签的值（value）与“=”相连组成，例如 group = IT。它可以作为管理存储桶的一个标识，便于用户对存储桶进行分组管理。您可以通过控制台对指定的存储桶进行标签的设定、查询和删除操作。


>!
>- 同个存储桶下最多支持50个标签，且标签键不能重复。
>- 标签键和标签值不得使用`qcs:`、`project`、`项目`保留字段，更多限制请参见 [存储桶标签概述](https://intl.cloud.tencent.com/document/product/436/31509)。

## 在新创建存储桶时添加标签

您可以在 [创建存储桶](https://intl.cloud.tencent.com/document/product/436/13309) 时添加存储桶标签，如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/02d9832d2244e4010d67dc49dee490bf.png)

## 在已创建存储桶中添加标签

若您在创建存储桶时未添加标签，您可以按照下述步骤为存储桶添加标签。

1. 在 [存储桶列表](https://console.cloud.tencent.com/cos5/bucket) 页，找到您需要添加标签的存储桶，单击其名称，进入存储桶配置页面。
2. 单击左侧的【基础配置】，下拉页面找到【标签管理】配置项，单击【添加标签】，添加存储桶标签。
   ![](https://qcloudimg.tencent-cloud.cn/raw/ad3d20fe1e2738de4bb326a8b51b8b36.png)
3. 输入标签键和标签值后，单击【保存】即可添加标签。

