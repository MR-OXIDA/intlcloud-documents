>!本文档主要介绍__即时通信 IM__ 访问管理功能的相关内容，其他产品访问管理相关内容请参见 [支持 CAM 的产品](https://intl.cloud.tencent.com/document/product/598/10588)。

IM 访问管理实质上是将子账号与策略进行绑定，或者说将策略授予子账号。开发者可以在控制台上直接使用预设策略来实现一些简单的授权操作，复杂的授权操作请参见 [自定义策略](https://intl.cloud.tencent.com/document/product/1047/38088)。
IM 目前提供了以下预设策略：

<table class="table"><thead><tr><th>策略名称</th><th>策略描述</th></tr></thead>
<tbody><tr><td>QcloudAVCFullAccess</td><td>IM 全读写访问权限</td></tr>
<tr><td>QcloudIMReadOnlyAccess</td><td>IM 只读访问权限</td></tr></tbody></table>

## 预设策略使用示例

### 新建拥有即时通信权限的子账号


1. 以腾讯云 [主账号](https://intl.cloud.tencent.com/document/product/598/32633) 的身份访问 CAM 控制台的[**用户列表**](https://console.cloud.tencent.com/cam)，单击**新建用户**。
2. 在“新建用户”页面选择**自定义创建**，进入“新建子用户”页面。
>?请根据 CAM [自定义创建子用户](https://intl.cloud.tencent.com/document/product/598/13674) 的操作指引完成“设置用户权限”之前的步骤。
3. 在“设置用户权限”页面：
  1. 搜索并勾选预设策略`Instant Messaging`。
  2. 单击**下一步**。
4. 在“审阅信息和权限”分栏下单击**完成**，完成子用户的创建，在成功页面下载并保管好该子用户的登录链接和安全凭证，其中包含的信息如下表：
<table class="table"><tbody><tr><td>信息</td><td>来源</td><td>作用</td><td>是否必须保存</td></tr>
<tr><td>登录链接</td><td>在页面中复制</td><td>方便登录控制台，省略填写主账号的步骤</td><td>否</td></tr>
<tr><td>用户名</td><td>安全凭证 CSV 文件</td><td>登录控制台时填写</td><td>是</td></tr>
<tr><td>密码</td><td>安全凭证 CSV 文件</td><td>登录控制台时填写</td><td>是</td></tr>
<tr><td>SecretId</td><td>安全凭证 CSV 文件</td><td>调用服务端 API 时使用，详见 <a href="https://intl.cloud.tencent.com/document/product/598/32675" target="_blank">访问密钥</a></td><td>是</td></tr>
<tr><td>SecretKey</td><td>安全凭证 CSV 文件</td><td>调用服务端 API 时使用，详见 <a href="https://intl.cloud.tencent.com/document/product/598/32675" target="_blank">访问密钥</a></td><td>是</td></tr></tbody></table>
5. 将上述登录链接和安全凭证提供给被授权方，后者即可使用该子用户对 IM 做所有操作，包括访问 IM 控制台、请求 IM 服务端 API 等。

### 将即时通信权限授予已存在的子账号


1. 以腾讯云 [主账号](https://intl.cloud.tencent.com/document/product/598/32633) 的身份访问 CAM 控制台的[**用户列表**](https://console.cloud.tencent.com/cam)，单击想要进行授权的子账号。
2. 单击“用户详情”页面权限栏的**添加策略**，如果子账号的权限非空，则单击**关联策略**。
3. 选择**从策略列表中选取策略关联**，搜索并勾选预设策略`Instant Messaging`。后续按页面提示完成授权流程即可。


### 解除子账号的即时通信权限


1. 以腾讯云 [主账号](https://intl.cloud.tencent.com/document/product/598/32633) 的身份访问 CAM 控制台的[**用户列表**](https://console.cloud.tencent.com/cam)，单击想要解除授权的子账号。
2. 在“用户详情”页面权限栏找到预设策略`Instant Messaging`，单击右侧的**解除**。按页面提示完成解除授权流程即可。
