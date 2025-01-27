### 如果云服务器在购买时没有分配公网 IP ，应该如何申请？
如果您在购买云服务器时没有分配公网 IP，那么无法为该云服务器再申请普通公网 IP，但可以通过 [弹性公网 IP](https://intl.cloud.tencent.com/document/product/213/5733) 来实现相同功能，操作详情请参见 [申请 EIP](https://intl.cloud.tencent.com/document/product/213/16586)。
- 弹性公网 IP 是公网 IP 的一种，是某地域下一个固定不变的公网 IP 地址。与普通公网 IP 不同的是，它是与您的账户绑定，即：您可以将一个弹性公网 IP 根据需要与不同的云服务器绑定、解绑（一次仅能绑定一个）。
- 由于弹性公网 IP 的特殊性，如果您申请了弹性公网 IP 但并未绑定实例，需要收取一定的 IP 资源费用，详情请参见 [弹性公网 IP 计费说明](https://intl.cloud.tencent.com/zh/document/product/213/17156)。

### 没有公网 IP 地址的实例（云服务器、数据库）如何访问公网？
没有公网 IP 的实例可以申请弹性公网 IP（请参见上一个问题），或者通过 NAT 网关访问公网。
[NAT 网关](https://intl.cloud.tencent.com/document/product/1015) 能够为私有网络内的云服务器提供 SNAT 和 DNAT 功能，如果您有多台云服务器需要通过一个公网 IP 访问公网，可以使用 NAT 网关。

### 能否为云服务器更换公网 IP？
可以。
- 如果您的云服务器是在购买时分配的普通公网 IP，请参见 [更换公网 IP 地址](https://intl.cloud.tencent.com/document/product/213/16642)。
- 如果您的云服务器绑定的是弹性公网 IP，您需要 [解绑该弹性公网 IP](https://intl.intl.cloud.tencent.com/document/product/213/16586)，重新 [申请一个弹性公网 IP](https://intl.intl.cloud.tencent.com/document/product/213/16586) 或为其绑定已有弹性公网 IP。
> ! 普通公网 IP 转换成弹性公网 IP 后，建议您立即释放，否则，未绑定实例的弹性公网 IP 将会收取一定 [IP 资源费用](https://intl.cloud.tencent.com/document/product/213/17156)。 

### 能否找回之前使用的公网 IP？能否申请指定的弹性公网 IP？
支持找回您使用过、且当前未分配给其他用户的公网 IP，找回后的公网 IP 均为 EIP，详情请参见 [找回公网 IP 地址](https://intl.cloud.tencent.com/document/product/213/32719)。

### 弹性公网 IP 数量达到上限后能否申请增加配额？
由于弹性公网 IP 资源的有限性，每个账号每个地域仅能申请20个，不能申请增加配额。对于无公网 IP 的云服务器，您可以使用 NAT 网关等方式访问公网。

### 如果云服务器有公网 IP 或弹性公网 IP，所在子网又关联了 NAT 网关，将如何实现公网的访问?

如果一台云服务器有公网 IP 或弹性公网 IP，同时，子网又关联了 NAT 网关，即路由表中设置了该子网访问公网流量的下一跳是 NAT 网关，那么，默认该云服务器访问公网的流量会全部通过 NAT 网关实现。

如果您需要修改优先级，使得云服务器访问公网的流量通过公网IP实现，请参见 [调整 NAT 网关和公网 IP 的优先级](https://intl.cloud.tencent.com/document/product/1015/32734)。

### 当云服务器通过公网网关或 NAT 网关访问公网时，网络费用是否会收取双份？

不会，网络费用只收取一份。通过公网网关或 NAT 网关访问公网，收取的是公网网关或 NAT 网关的网络费用。 

