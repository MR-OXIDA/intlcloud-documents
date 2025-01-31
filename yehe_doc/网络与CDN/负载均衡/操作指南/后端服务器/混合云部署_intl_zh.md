在混合云部署的场景中，可以使用负载均衡直接绑定云下本地数据中心（IDC）内 IP，实现跨 VPC 与 IDC 之间的后端云服务器的绑定。
目前该功能处于内测阶段，如需体验，请提交 [内测申请](https://intl.cloud.tencent.com/apply/p/mzjxboiv2yq)。

## 方案优势
- 快速搭建混合云，无缝连接云上云下，负载均衡可将请求同时转发至云上 VPC 内云服务器和云下 IDC 机房内云服务器。
- 复用腾讯云的高质量公网接入能力。
- 复用腾讯云负载均衡的丰富功能特性，例如四/七层接入、健康检查、会话保持等。
- 内网通过 [云联网](https://intl.cloud.tencent.com/document/product/1003/30049) 互通，支持精细化选路保障质量，支持多样化阶梯计费降低成本。
![](https://main.qcloudimg.com/raw/e09b0e4b6fcaedf44267f6ca1950ee54.png)	

## 限制条件
- 跨网互联绑定云服务器暂不支持传统型负载均衡。
- 该功能仅标准账户类型支持。若您无法确定账户类型，请参见 [判断账户类型](https://intl.cloud.tencent.com/document/product/684/15246)。
- 跨地域绑定2.0和混合云部署，不支持[ 安全组默认放通](https://intl.cloud.tencent.com/document/product/214/14733)，请在后端服务器上放通 Client IP 和服务端口。
- 目前仅广州、深圳、上海、济南、杭州、北京、天津、成都、重庆、中国香港、新加坡、硅谷地域支持该功能。
- TCP 和 TCP SSL 监听器需在 RS 上通过通用 TOA 获取源 IP，详情请参见 [TOA 模块加载方法](https://intl.cloud.tencent.com/document/product/608/18945)。
- HTTP 和 HTTPS 监听器需通过 X-Forwarded-For（XFF）获取源 IP。
- UDP 监听器不支持获取源 IP。

## 前提条件
1. 已提交内测申请，境内跨地域绑定请通过内测申请，境外跨地域绑定请进行 [商务申请](https://intl.cloud.tencent.com/contact-sales)。
2. 已创建负载均衡实例，详情请参见 [创建负载均衡实例](https://intl.cloud.tencent.com/document/product/214/6149)。
3. 已创建云联网实例，详情请参见 [新建云联网实例](https://intl.cloud.tencent.com/document/product/1003/30062)。
4. 将与 IDC 关联的专线网关和需要绑定的目标 VPC 关联至已创建的云联网实例，详情请参见 [关联网络实例](https://intl.cloud.tencent.com/document/product/1003/30064)。

## 操作步骤
1. 登录 [负载均衡控制台](https://console.cloud.tencent.com/loadbalance)。
2. 在负载均衡“实例管理”页面找到目标负载均衡实例，单击实例 ID。
3. 在“基本信息”页面的“后端服务”区域，单击【点击配置】绑定非本 VPC 的内网 IP。
![](https://main.qcloudimg.com/raw/1214576094baa072eb1d3577a5f5781a.png)
4. 在弹出的“打开启用非本 VPC 内 IP”对话框中，单击【提交】。
![](https://main.qcloudimg.com/raw/4f7b99a8532afabe54440ca7819dcd72.png)
5. 在“基本信息”页面的“后端服务”区域，单击【新增 SNAT IP】。
![](https://main.qcloudimg.com/raw/fc41b320241fa4de1d961e1a9c8d428f.png)
6. 在弹出的“新增 SNAT IP”对话框中，选择“子网”，单击【新增】分配 IP，最后单击【保存】。
<img src="https://main.qcloudimg.com/raw/6aad8ac7d4a38a8e74ea7b3b59e36cbb.png" width="50%"/>
7. 在实例详情页面，单击“监听器管理”页签，在配置监听器模块中，为负载均衡实例绑定后端服务，详情请参见 [添加负载均衡后端云服务器](https://intl.cloud.tencent.com/document/product/214/6156)。
8. 在弹出的“绑定后端服务”对话框中，选择“其他内网 IP”，单击【添加内网 IP】，输入需绑定的 IDC 内网 IP 地址，并填写端口与权重，详情请参见 [服务器常用端口](https://intl.cloud.tencent.com/document/product/213/12451)，最后单击【确认】。

9. 返回“已绑定后端服务”区域可以查看已绑定的 IDC 的内网 IP。<br/>
