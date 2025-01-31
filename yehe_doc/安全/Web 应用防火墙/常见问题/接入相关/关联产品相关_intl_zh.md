### WAF 如何同 CDN 或 DDoS 高防包 一起接入？
- WAF 可直接将 DDoS 高防包叠加，CDN 的源站指向WAF 实例的 IP 即可。最佳部署架构：客户端 > CDN > WAF+高防包 > 负载均衡 > 源站。
- 在客户需要 CDN 和高防能力时，只要将网站管家接入后提供的 CNAME 配置为 CDN 的源站即可，同时可以将 DDoS 高防包叠加到 WAF 实例上。即可实现用户流量经过 CDN 之后，被转发至 WAF，同时具备大流量 DDoS 的清洗能力，最终转发至源站，对源站进行全面的安全防护。

### 若已经接入 CDN 域名在 WAF 如何接入？
若已经接入 CDN 域名，将 WAF 为域名分配的 CNAME 地址作为 CDN 的源站即可，流量按照用户 > CDN > WAF > 负载均衡 > 源站的架构回源。同时您可以登录 WAF 控制台，在 [添加域名页面](https://console.cloud.tencent.com/guanjia/waf/config/add)，将代理情况勾选为是，此时 WAF 会根据 HTTP 头部中的 XFF 字段，获取客户端的真实 IP，保证 WAF 正常防护。

