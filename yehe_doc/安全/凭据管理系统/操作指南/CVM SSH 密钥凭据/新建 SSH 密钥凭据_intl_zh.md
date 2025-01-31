## 操作场景
在 [凭据管理系统](https://console.cloud.tencent.com/ssm) 控制台中创建 SSH 密钥，SSH 密钥通过 SSM 进行安全加密托管，实现对 SSH Private Key 的安全托管。
> ! 为了能让您更好地使用 **CVM SSH 密钥管理**功能，请提前做好以下准备：
- [确认已开通KMS服务](https://buy.cloud.tencent.com/kms)，SSM 基于密钥管理系统 KMS 托管的密钥进行加密。
- 确保您已经创建 云服务器 CVM 实例。对于具体操作，请查阅 [创建 CVM 实例](https://intl.cloud.tencent.com/document/product/213/36302)。

## 操作步骤
1. 登录 [凭据管理系统](https://console.cloud.tencent.com/ssm) 控制台，在左侧导航栏中，单击 **CVM SSH 密钥管理**，进入 CVM SSH 密钥页面。
   ![](https://qcloudimg.tencent-cloud.cn/raw/8fbd29fd45d563503b3f68dd9ef94336.png)
2. 在 CVM SSH 密钥页面中，单击左上角的“区域下拉框”，切换区域。
   ![](https://qcloudimg.tencent-cloud.cn/raw/8c0901b331cf756f3519dd89701bd57b.png)
3. 在 CVM SSH 密钥页面中，单击左上角的**新建**，进入创建 SSH 密钥页面。
4. 在创建 SSH 密钥页面中，输入相对应的信息后，单击**确定**，返回管理页面，新创建的凭据会出现在列表的首位。
    ![](https://qcloudimg.tencent-cloud.cn/raw/b708e55c58035960525dc9f54e7427e9.png)

**字段说明**
-  **凭据名称：**凭据名称在同一 region 内不可重复，最长128字节，使用字母、数字或者 - _ 的组合，第一个字符必须为字母或者数字。
-  **描述：**描述信息，用于详细描述用途等，最大支持2048字节。
- **项目ID：**密钥对创建后所属的项目 ID 。
- **标签：**非必填。
- **选择加密密钥：**
 - 使用凭据管理系统在密钥管理系统（KMS）中默认创建的主密钥（CMK）进行加密。
 - 使用自定义加密密钥。 

> ! 若使用凭据管理系统表明您已开启 [密钥管理系统](https://intl.cloud.tencent.com/product/kms)，您可以通过以下两种方案创建加密密钥：
>- 选择在 [密钥管理系统](https://intl.cloud.tencent.com/product/kms) 中默认创建的云产品主密钥作为加密密钥，并通过信封加密方案进行加密存储。
>- 选择在 [密钥管理系统](https://intl.cloud.tencent.com/product/kms) 中创建一个用户密钥，将该密钥作为自定义的加密密钥对凭据进行加密存储。
