## 什么是封堵
当目标 IP 受到的攻击流量超过其封堵阈值时，腾讯云将通过运营商的服务屏蔽该 IP 的所有外网访问，保护云平台其他用户免受影响。简而言之，当您的某个 IP 受到的攻击流量超过您所购买的高防 IP 最大防护能力时，腾讯云将屏蔽该 IP 的所有外网访问。当您的高防 IP 被封堵时，您可以登录 [DDoS 高防 IP 控制台](https://console.cloud.tencent.com/ddos/antiddos-advanced/overview/ddos) 进行自助解封。

## 封堵时长
默认为2小时，实际封堵时长与当日封堵触发次数和攻击峰值相关，最长可达24小时。
封堵时长主要受以下因素影响：
- 攻击是否持续：若攻击一直持续，封堵时间会延长，封堵时间从延长时刻开始重新计算。
- 攻击是否频繁：被频繁攻击的用户被持续攻击的概率较大，封堵时间会自动延长。
- 攻击流量大小：被超大型流量攻击的用户，封堵时间会自动延长。
>!针对个别封堵过于频繁的用户，腾讯云保留延长封堵时长和降低封堵阈值的权利。

## 为什么不能立即解除封堵？
通常 DDoS 攻击会持续一段时间，不会在封堵后立即停止，具体持续时间不定，腾讯云安全团队会根据大数据分析的结果，设定默认封堵时长。

由于封堵是在运营商网络部分生效，被攻击外网 IP 进入封堵后，腾讯云无法监控到攻击流量是否停止。如果在攻击未停止的情况下解除封堵，被攻击外网 IP 将再次进入封堵，同时在解除封堵至再次封堵生效的这段时间内，攻击流量将直接进入腾讯云的基础网络，可能会影响到云内其它用户。另外，封堵是腾讯云向运营商购买的服务，解封次数、频率都有限制。

## 如何解除封堵？
封堵是腾讯云向运营商购买的服务，解封次数、频率都有限制。
>?DDoS 高防 IP 的用户每天将拥有三次自助解封机会，当天超过三次后将无法进行解封操作。系统将在每天零点时重置自助解封次数，当天未使用的解封次数不会累计到次日。

 具体解封操作，请参见 [解除封堵](https://intl.cloud.tencent.com/document/product/297/43395)。
