## 功能介绍
日志搜索功能提供组件的运行日志采集和搜索功能，支持当前集群核心服务日志和节点系统日志进行关键词搜索，可以在不登录节点的情况下快速查看服务关键日志。

日志搜索支持根据当前集群、日志文件、节点 IP 和时间范围条件过滤，日志结果包含节点 IP、日志在节点上的绝对路径和日志内容。

## 操作步骤
1. 登录 [EMR 控制台](https://console.cloud.tencent.com/emr)，在**集群列表**中单击对应的集群**ID/名称**进入集群详情页。
2. 在集群详情页中选择**集群监控**>**日志搜索**可根据当前集群、日志文件、节点 IP 和时间范围条件过滤，查看日志内容。

**查看上下文：**在排查问题的时候，经常需要关注关键词的上下文日志，在日志搜索结果列表中，选择**操作**>**查看上下文**，可以查看日志的上下文信息。


## 日志搜索支持的服务类型

>!
>- 当前仅支持15天日志搜索。
>- 若集群未开启日志采集，如需开启日志采集，请联系您的专属售后。
	
支持 hdfs、yarn、hive、hbase 四个组件的日志采集，目录和文件列表如下：

```
/data/emr/hdfs/logs:
hadoop-hadoop.log
hadoop-hadoop-namenode-x.x.x.x.out
hadoop-hadoop-datanode-x.x.x.x.out

/data/emr/yarn/logs:
yarn-hadoop-resourcemanager-x.x.x.x.out
yarn-hadoop-resourcemanager-x.x.x.x.log
yarn-hadoop-nodemanager-x.x.x.x.out
yarn-hadoop-nodemanager-x.x.x.x.log

/data/emr/hive/logs:
hadoop-hive
hcat.err
hcat.out

/data/emr/hbase/logs:
hbase-hadoop-master-x.x.x.x.out
hbase-hadoop-master-x.x.x.x.log
hbase-hadoop-regionserver-x.x.x.x.out
hbase-hadoop-regionserver-x.x.x.x.log
```

