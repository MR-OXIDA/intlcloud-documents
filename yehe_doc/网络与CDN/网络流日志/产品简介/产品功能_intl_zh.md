流日志具有日志采集、查询、数据管理、数据记录等功能，帮助您降低运维门槛，轻松定位业务问题。

## 流日志采集

为弹性网卡创建流日志后，系统将自动采集弹性网卡的日志流，并将日志数据同步至[ 日志服务 CLS](https://intl.cloud.tencent.com/document/product/614/11254)。在 CLS 的主题中，每个弹性网卡有唯一的日志流，其中包含流日志记录。

## 流日志查询
[日志服务 CLS](https://intl.cloud.tencent.com/document/product/614/11254) 支持亿级日志数据检索。您可以进行全文检索、多关键词检索、跨主题查询等操作，秒级返回查询结果。

## 流日志数据
流日志与 [日志服务 CLS](https://intl.cloud.tencent.com/document/product/614/11254) 深度结合，实现对日志数据的存储与管理。

## 流日志记录
流日志将记录特定捕获窗口中，按五元组规则过滤的网络流。

- **五元组**
即源 IP 地址，源端口，目的 IP 地址，目的端口，和传输层协议这五个量组成的一个集合。
- **捕获窗口**
即一段持续时间，在这段时间内流日志服务会聚合数据，然后再发布流日志记录。捕获窗口大约为5 - 10分钟，推送时间约为5分钟。流日志记录是以空格分隔的字符串，采用以下格式：
`version account-id interface-id srcaddr dstaddr srcport dstport protocol packets bytes start end action log-status`。

|字段 | 说明 |
|---------|---------|
|version | 流日志版本。 |
|account-id | 流日志的账户 AppID。|
|interface-id | 弹性网卡 ID。 |
|srcaddr | 源 IP。|
|dstaddr | 目标 IP。|
|srcport | 流量的源端口。当流量为 ICMP 协议时，该字段表示 ICMP 的 id。|
|dstport | 流量的目标端口。当流量为 ICMP 协议时，该字段表示 ICMP 的 type（高8bit）+code（低8bit）组合。|
|protocol | 流量的 IANA 协议编号。有关更多信息，请转到分配的 [ Internet 协议](https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml#protocol-numbers-1) 编号。 |
|packets | 捕获窗口中传输的数据包的数量。 |
|bytes | 捕获窗口中传输的字节数。 |
|start | 捕获窗口启动的时间，采用 Unix 秒的格式。 |
|end | 捕获窗口结束的时间，采用 Unix 秒的格式。 |
|action | 	与流量关联的操作：<br/> ACCEPT：安全组或网络 ACL 允许记录的流量。<br/>  REJECT：安全组或网络 ACL 未允许记录的流量。|
|log-status | 流日志的日志记录状态：<br>OK：表示数据正常记录到指定目标。<br/> NODATA：表示捕获窗口中没有传入或传出网络流量，此时“packets”和“bytes”字段会显示为“-1”。<br/>SKIPDATA：表示捕获窗口中跳过了一些流日志记录。可能是内部容量限制或内部错误引起的。 |


### 示例
- 若允许接受账户 1251762227 中的弹性网卡 eni-lq6mkcis 的 SSH 流量（目标端口 22，TCP 协议），流日志记录如下：

  ```
  2 1251762227 eni-lq6mkcis 172.31.16.139 172.31.16.21 20641 22 6 20 4249 1418530010 1418530070 ACCEPT OK
  ```

- 若拒绝账户1251762227中的弹性网卡 eni-lq6mkcis 的 RDP 流量（目标端口3389，TCP 协议），流日志记录如下：

  ```
  2 1251762227 eni-lq6mkcis 172.31.9.69 172.31.9.12 49761 3389 6 20 4249 1418530010 1418530070 REJECT OK
  ```

- 若在捕获窗口中未记录数据，流日志记录如下：

  ```
  V1 1251762227 eni-lq6mkcis - - - - - - - 1431280876 1431280934 - NODATA
  ```

- 若在捕获窗口中跳过了记录，流日志记录如下：

  ```
  V1 1251762227 eni-lq6mkcis - - - - - - - 1431280876 1431280934 - SKIPDATA
  ```

- 安全组和网络 ACL 规则的流日志记录
 - 安全组为有状态，因此允许响应所有的流量。
 - 网络 ACL 为无状态，因此对流量的响应需要遵守网络 ACL 规则。

  例如，您从家中的计算机（IP 地址为`203.0.113.12`）对您的实例（网络接口的私有 IP 地址为`172.31.16.139`）使用 ping 命令。您的安全组入站规则允许 ICMP 流量，出站规则不允许 ICMP 流量，但是，由于安全组是有状态的，因此允许从您的实例响应 ping。
  您的网络 ACL 允许入站 ICMP 流量，但不允许出站 ICMP 流量。由于网络 ACL 是无状态的，响应 ping 将被丢弃，不会传输到您家中的计算机。在流日志中，它显示为2个流日志记录：
  - 网络 ACL 和安全组都允许（因此可到达您的实例）的发起 ping 的 ACCEPT 记录。
  - 网络 ACL 拒绝的响应 ping 的 REJECT 记录。

  ```
  V1 1251762227 eni-lq6mkcis 203.0.113.12 172.31.16.139 0 0 1 4 336 1432917027 1432917142 ACCEPT OK
  ```

  ```
  V1 1251762227 eni-lq6mkcis 172.31.16.139 203.0.113.12 0 0 1 4 336 1432917094 1432917142 REJECT OK
  ```

  如果您的网络 ACL 允许出站 ICMP 流量，流日志会显示两个 ACCEPT 记录（一个针对发起 ping，一个针对响应 ping）。如果您的安全组拒绝入站 ICMP 流量，流日志会显示一个 REJECT 记录，因为流量未到达您的实例。
