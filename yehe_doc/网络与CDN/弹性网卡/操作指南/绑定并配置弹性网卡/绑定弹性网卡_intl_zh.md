本文指导您绑定弹性网卡到云服务器上。
>?
>+ 如您云服务器镜像类型为 CentOS 8.0、7.8、7.6、7.5、7.4，可直接参考 [Linux云服务器配置弹性网卡](https://intl.cloud.tencent.com/document/product/576/41744) 中的“工具配置”，即先安装工具，再执行本操作绑定弹性网卡，弹性网卡信息将自动配置到云服务器的网卡文件中，路由策略也将自动下发。
>+ 如您是其他镜像类型的云服务器，请先参考本节绑定弹性网卡到云服务器，然后再参考 [Linux云服务器配置弹性网卡](https://intl.cloud.tencent.com/document/product/576/41744) 中的“手动配置”，或 [Windows云服务器配置弹性网卡](https://intl.cloud.tencent.com/document/product/576/41745) 进行弹性网卡的配置。

## 绑定云服务器
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc) 。
2. 单击左侧目录中的【IP 与网卡】>【弹性网卡】。
3. 在弹性网卡列表页，找到需要绑定和配置的弹性网卡所在行，单击操作栏中的【绑定云服务器】。
![](https://main.qcloudimg.com/raw/bce45aabdb1e1b26df31d3ff40211bce.png)
>?
>- 仅支持绑定和弹性网卡在相同可用区的云服务器。
>- 不支持绑定黑石2.0（裸金属）服务器。
>
4. 在弹框中，选择需要绑定的云服务器，单击【确定】完成绑定。
    ![](https://main.qcloudimg.com/raw/7bbcb3850eae4b56ccd6d2f918f04682.png)

