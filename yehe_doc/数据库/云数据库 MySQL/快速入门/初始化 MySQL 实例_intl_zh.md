创建 MySQL 实例后，对于状态为**未初始化**的实例，需要进行初始化操作后，才能使用实例。

## 操作步骤
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，选择对应地域后，在实例列表，选择状态为**未初始化**的实例，在**操作**列单击**初始化**。
2. 在弹出的初始化对话框，配置初始化相关参数，单击**确定**。
 - **支持字符集**：支持 LATIN1 、GBK、UTF8 、UTF8MB4 字符集，默认字符集编码格式是 UTF8。初始化实例后，亦可在控制台实例详情页修改字符集，更多说明请参见 [字符集说明](https://intl.cloud.tencent.com/document/product/236/7259)。
 - **表名大小写敏感**：表名是否大小写敏感，默认为是。
 - **自定义端口**：数据库的访问端口，默认为3306。
 - **设置root帐号密码**：新创建的 MySQL 数据库的用户名默认为 root，此处用来设置该 root 帐号的密码。
 - **确认密码**：再次输入密码。
3. 在弹出的初始化对话框，单击**确定**。
![](https://qcloudimg.tencent-cloud.cn/raw/cd8d4f83c43cc23b23c50c2e85773473.png)
4. 返回实例列表，待实例状态变为**运行中**，即可正常使用。

## 后续操作
通过 Windows 云服务器或 Linux 云服务器，以内外网两种不同的方式连接云数据库 MySQL，请参见 [连接 MySQL 实例](https://intl.cloud.tencent.com/document/product/236/37788)。
