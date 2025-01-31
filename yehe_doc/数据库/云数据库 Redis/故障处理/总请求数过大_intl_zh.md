## 现象描述
- 现象1：QPS 指标较高。
![](https://qcloudimg.tencent-cloud.cn/raw/a17ff6a9a1234786ebe2644ff62077bd.png)
- 现象2：响应时延变大。
- 现象3：可能引起连接超时。

## 可能原因
- 自身业务需要优化。
- 实例配置需要升级。

## 解决思路
- 查看节点负载：对于集群架构，查看节点负载情况，如果只有一个或少量节点的 QPS 超过告警值，则说明可能存在热 Key；如果大部分节点都超过，则说明 Redis 整体负载高，这种情况考虑升级实例配置。
- 查看慢查询：您可以打开控制台查看是否存在慢查询，如果存在并且时间与发生问题的时间匹配，那么可能是存在大 Key 的问题。
- 查看 CPU 使用率：您可以查看 CPU 使用率是否过高，如果过高则可能是机器资源不足，可以考虑升级实例配置。

经过判断，如果需要优化业务，您可以针对热 Key、大 Key 进行优化；如果需要升级实例配置，您可以通过开启读写分离和增加分片来满足当前的业务需求。


## 处理步骤
### [业务优化](id:ywyh)
1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，在实例列表，单击实例 ID，进入实例管理页面。
2. 在实例管理页面，选择【系统监控】页，确认 QPS 是否过高或者有突发的热 Key。
3. 在排查异常访问后，您可以对业务逻辑进行优化：
 - 对于热 Key，您可以拆分复杂数据结构，将热点 Key 拆分为若干个新的 Key 分布到不同 Redis 节点上，从而减轻压力。以哈希类型为例，该热 Key 的类型是一个二级数据结构，该哈希元素个数可能较多，可以考虑将当前 hash 进行拆分。
 - 对于大 Key，如果是 value 过大，您可以将对象拆分成多个 key-value，将操作压力平摊到多个 Redis 实例；如果是 Key 过多，您可以参考 hash 结构存储，将多个 Key 存储在一个 hash 结构中。


### [实例升级](id:slsj)
#### 读负载过大场景
读负载过大时，您可以 [开启读写分离](https://intl.cloud.tencent.com/document/product/239/31935)，通过 [增加副本数](#zjfb) 来分摊读负载。
>!开启读写分离可能会导致数据读取不一致（副本节点数据延后于主节点），请先确认业务是否允许数据不一致的问题，请参见 [变更实例规格](https://intl.cloud.tencent.com/document/product/239/31934)。

[](id:zjfb)
1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，在实例列表，选择“操作”列的【配置变更】>【增加副本】。
![](https://qcloudimg.tencent-cloud.cn/raw/babd6ccfe0eb42326fda4e25101e50a4.png)
2. 在弹出的配置变更对话框，选择需更改的配置，单击【确定】。
3. 返回实例列表，待实例状态变更为“运行中”，即可正常使用。

#### 写负载过大场景
- **集群架构**
登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，在实例列表，选择“操作”列的【配置变更】>【增加分片】。
>?
>- 配置变更后，实例将按照新的规格计费。
>- 新增分片操作，系统将自动均衡 Slot 配置，并且迁移数据，迁移操作可能会失败，建议在业务低峰期进行操作， 避免迁移操作对业务访问造成影响。
>- 每分片能提供的 QPS 为8W - 10W，请按需增加。
>
![](https://qcloudimg.tencent-cloud.cn/raw/c9b06662d7f15daf5c7f1c89a4de54fd.png)

- **标准架构**
通过升级为集群版提升 CPU 处理能力，升级集群前需要检测兼容性，请参见 [标准架构迁移集群架构检查](https://intl.cloud.tencent.com/document/product/239/37594)。
 1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，在实例列表，单击实例 ID，进入实例详情页面。
 2. 在实例详情页的“规格信息处”，单击【架构升级】。
![](https://qcloudimg.tencent-cloud.cn/raw/52633dac2a97272cab593fc1eb306221.png)
 3. 升级集群架构后，返回实例列表，选择“操作”列的【配置变更】>【增加分片】。

>?如果以上方法仍未解决问题，您还可以 [提交工单](https://console.intl.cloud.tencent.com/workorder/category) 联系售后。
>
