本文档将指导您如何验证SaaS 型 WAF 是否生效。

## 操作步骤
1. WAF 通过域名和源站进行绑定，对流量进行防护。验证SaaS型 WAF 是否生效，请先确保本地电脑可以正常访问在 SaaS不同实例下添加的域名。
2. 在浏览器中输入网址 `http://wow.qcloudwaf.com/?test=alert(123) `并访问，浏览器返回阻断页面，说明 Web 应用防火墙防护功能正常。
>!`wow.qcloudwaf.com` 为本案例中域名，此处需要将域名替换为实际添加的域名。

![](https://main.qcloudimg.com/raw/253fdfbae2d6529f2b1e64c1f599c8cc.png)



