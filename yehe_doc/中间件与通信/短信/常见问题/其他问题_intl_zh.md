### 用户没有收到短信怎么处理？
登录 [短信控制台](https://console.cloud.tencent.com/smsv2) ，选择【统计分析】>【国内短信】（或【国际/港澳台短信】）>【短信记录】，查看对应号码的短信【发送状态】和【备注】。
- 如果【发送状态】为失败，可结合【备注】中的失败原因说明进一步排查，常见原因有请求命中了频率控制策略、短信内容格式不正确或手机号已因退订加入黑名单中等。
- 如果【发送状态】为成功，但【备注】中提示错误码，请根据具体 [错误码](https://intl.cloud.tencent.com/document/product/382/34861) 信息进一步排查。
- 如果【发送状态】为成功且【备注】中提示“用户短信接收成功”，但是用户实际并未收到短信，可以从以下几个方面进行排查：
 - 手机关机、欠费或停机：检查手机状态，例如拨打手机确认。
 - 手机号处于黑名单状态：确认机主是否投诉过运营商或退订过业务。
 - 手机长时间未关机引起无法正常接收短信：可以尝试重启手机。
 - 手机信号异常引起无法正常接收短信：检查手机信号，必要时可尝试重启手机。
 - 手机收件箱满：可尝试删除多余短信。
 - 手机设置异常或硬件异常引起无法正常接收短信：可尝试修改相关设置或将 SIM 卡换到其他手机上进行测试（双卡手机可交换卡槽测试）。
 - 短信被用户手机中的系统/软件拦截屏蔽：检查屏蔽列表。

如仍然无法解决，请[提交工单](https://console.cloud.tencent.com/workorder/category)。

### 调用接口耗时比较长怎么办？[](id:jump)
如果发现访问腾讯云短信接口时请求耗时较长，可参考以下方法进行定位：
1. 执行`dig yun.tim.qq.com`命令，确认是否使用内网 DNS。若是使用内网 DNS，则选择一个就近的同运营商的腾讯云短信 IP 配置 host，排查问题是否解决。
  - 如果问题已解决，则说明可能是 DNS 解析卡住或者 DNS 解析跨地域运营商访问引起的时延，建议使用 DNS 代理或配置公网 DNS server。
  - 如果问题未解决，请执行 [步骤2](#Q2step2)。
2. 检查业务使用哪种连接模式以及是否使用连接池。[](id:Q2step2)
 - 如果业务使用单条长连接，根据 HTTP 一应一答的模式，前面的请求卡住会影响该连接上的后续请求。建议优化成“长连接 + 连接池”模式。
 - 如果业务使用短连接，用 netstat 确认本机连接数是否已满。如果连接数已满，建议优化成“长连接 + 连接池”模式。
 - 用 netstat 确认或用 tcpdump 抓包确认连接的 Recv-Q 和 Send-Q 是否存在积压。如果存在积压，建议优化成“长连接 + 连接池”模式。
 - 如果某条连接长时间（90s）没有请求时，为了防止中间网络设备回收该连接，建议请求方先关闭该连接，等下次发起请求且连接池中连接不够用时再新建连接。

### 为什么用户很久才收到短信？

1. 查看本地记录的请求发送时间和控制台上记录的该短信发送时间，计算两者之间的时间差。
 - 如果时间差较大（例如接近甚至超过10分钟），则可能是因为调用接口有时延，请参考 [调用接口耗时比较长](#jump) 解决。
 - 如果时间差较小，请执行 [步骤2](#Q3step2)。
2. 在控制台查询该短信【发送时间】与【状态上报时间】，计算两者之间的时间差。[](id:Q3step2)
 - 如果时间差较大（例如普通短信超过数10秒，营销短信超过5分钟），可能原因有短信内容有敏感词进入人工审核、手机信号不佳或手机处于异常状态（例如欠费或停机）等。
 - 如果时间差较小，可能原因有手机信号不佳或手机处于异常状态（例如关机）等。
3. 如果以上场景都不满足，请[提交工单](https://console.cloud.tencent.com/workorder/category)。

### 手机黑名单是什么？

目前黑名单有以下类型：
- 退订用户名单，用户主动对短信内容进行退订回复，例如回复“T”、“N”、“TD”、“退订”、“T退订”、“QX”或“0000”等（不区分大小写），系统收到回复后会将其手机号加入黑名单中。再次下发短信时会返回发送失败并备注“1015手机号在黑名单库中”，且用户无法成功接收短信。
 您可以登录 [短信控制台](https://console.cloud.tencent.com/smsv2) ，选择【通用管理】>【退订用户管理】页面提交解除退订状态申请，审核通过后生效。
- 运营商黑名单，该类用户因不同原因被运营商定为黑名单。下发短信时会返回发送成功，但是可能会因为被运营商网关拦截或其他原因导致用户无法成功接收短信。

### 返回1004错误如何处理？
调用腾讯云短信接口发送短信时，如果应答包返回1004错误，可通过以下方式定位解决：
1. 检查发送的请求是否为标准的 JSON 格式，建议您到网上搜索 JSON 格式检查工具进行排查校验。例如，误将单引号当做双引号使用，而标准的 JSON 格式应该是使用双引号。
2. 检查参数名称是否正确。
3. 检查请求的字段类型是否与 [API 文档](https://intl.cloud.tencent.com/document/product/382/34689) 中描述的字段类型一致。 例如，将 JSON 字符串和 JSON 整型混淆使用（`{"姓名":"小明", "年龄":23}`，"姓名"应为 JSON 字符串，"年龄"应为 JSON 整型）。
4. 检查请求的字段的取值是否在 API 文档中描述的取值范围内。 例如，international 字段只能取0或1。
5. 检查对 API 的调用是否与 API 文档描述的一致。 例如，调用群发短信的 API 时，包体的格式不能是单发短信的。
6. 如果仍旧无法解决，请[提交工单](https://console.cloud.tencent.com/workorder/category)。

### 返回1014错误如何处理？
调用腾讯云短信接口发送短信时，如果应答包返回1014错误，可通过以下方式定位解决：
1. 确认申请的内容模版格式是否正确。例如内容模版中的“{}”为英文的括号，括号中的数字需从1开始连续编号，即{1}，{2}等。
2. 确认模板中是否含变量值，若模板中含变量值，则发送短信时需传入变量进行发送，若模板中设置了多个变量值，则发送短信时也应该传入多个变量进行发送。
3. 确认请求内容对应的模版是否审批通过。
4. 确认请求包中 type 参数的值（0表示普通短信，1表示营销短信）与申请的内容模版类型是否一致。
5. 确认请求的内容与申请的内容模版格式是否一致，例如**因空格等不可见字符导致不匹配。**
6. 如果内容中含有中文，请确认中文需使用 UTF-8 编码。
7. 国内文本短信模板只能发中国大陆手机号，国际/港澳台短信模板只能发境外手机号。
8. 如果仍旧无法解决，请[提交工单](https://console.cloud.tencent.com/workorder/category)。

### 返回1016错误如何处理？
调用腾讯云短信接口发送短信时，如果应答包返回1016错误，可通过以下方式定位解决：
1. 确认 AppID 和 AppKey 是否正确。
2. 确认手机号码格式是否正确。**手机号码正确格式为连续数字，无需输入空格。**
3. 确认字段名称是否正确。


### 返回60008错误如何处理？
调用腾讯云短信接口发送短信时，如果应答包返回60008错误，可通过以下方式定位解决：
1. 如果请求在1s内响应60008错误码，请确认请求格式是否是标准 HTTP 格式。
2. 确认请求的 URL 及 Body 格式是否与 API 相符。
3. 确认请求 Content-Type 是否与包体相符（短信服务应该是`Content-Type: application/json;charset=utf-8`）。
4. 确认 DNS 配置是否正常，确保使用的是公网 DNS server。
5. 推荐业务使用 HTTP 长连接并使用连接池，以提升网络质量。
6. 如果仍旧无法解决，请[提交工单](https://console.cloud.tencent.com/workorder/category)。

### 返回1001（sig 校验失败）错误如何处理？
调用腾讯云短信接口发送短信时，如果应答包返回1001错误，可通过以下方式定位解决：
1. 确认 sig 生成的随机数与 URL 中的随机数是否一致。
2. 确认代码中的 SDK AppID/App Key（SDK AppID 以1400开头）是否填写正确。
3. 确认使用的代码是否跟示例代码一致，检查带入参数生成的 sig 伪代码是否一致。

### 如何获取短信 API SecretId 和SecretKey？
1. 登录腾讯云管理中心控制台。
2. 前往 [云API密钥](https://console.cloud.tencent.com/cam/capi) 的控制台页面。
3. 在云API密钥页面，单击【新建密钥】即可以创建一对密钥。

**SecretId**：用于标识 API 调用者身份，可以简单类比为用户名。
**SecretKey**：用于验证 API 调用者的身份，可以简单类比为密码。

>?
>- 用户必须严格保管安全凭证，避免泄露，否则将危及财产安全。如已泄漏，请立刻禁用该安全凭证。
>- 短信 SecretId 与 AccessKey ID 是一样的。


### 如何获取短信 SDK AppID 和 AppKey？
SDK AppID 和 AppKey 是开发者在申请开发新应用时获得的由腾讯云授予的应用程序接入账户和密钥，当您创建应用成功之后即可看到。
- **SDK AppID**：是腾讯云短信应用的唯一标识码，SDK AppID 如下图所示：
![](https://main.qcloudimg.com/raw/eee1084a4e88defd26f69061906d7a44.png)
- **AppKey**：是用来校验短信发送请求合法性的密码，该密钥在一定技术条件下可保证应用来源的可靠性。



### 为什么使用小程序转短链后，点击短链，无法跳转到指定页？
请在短链管理页 path 栏输入通过 scheme 码进入的小程序页面路径，必须是已经发布的小程序存在的页面，path 为空时会跳转小程序主页。可通过【小程序】>【统计】>【使用分析】>【页面分析】查找 path。

### 腾讯云短信发送后，对方收到信息是否可以回复，回复是否有时间限制？
对方需要在72小时内回复才有效，回复信息支持查看。

### 是否支持查看或者接收用户回复的信息？
短信支持用户上行回复，且回复短信不收取额外费用。回复内容可在控制台 [短信回复记录](https://console.cloud.tencent.com/smsv2/statistics-csms/record) 中查看，或设置回调地址获取回复内容。

### 开通腾讯云短信后，发送消息的号码是什么？
- 国内短信：发送消息的号码13 - 20位，1069开头，尾数是运营商的随机号码。
- 国际/港澳台短信：发送消息不显示号码，统一显示 Qsms 或 Qcloud。

### 不同的手机在同一时间，是否可以发送不同的短信内容？
可以多进程调用单发接口，实现对不同手机号发送不同短信内容。

### 发送短信报错，自己排查不出来该怎么办？
您可以[提交工单](https://console.cloud.tencent.com/workorder/category)。

### 短信发送失败，记录提示含有敏感词，但是申请时已通过审核，是什么情况？
敏感词库是由运营商反馈的，可以[提交工单](https://console.cloud.tencent.com/workorder/category)并提供发送失败的手机号码，人工客服将与运营商沟通确认能否解除。

### 短信签名和正文已审核通过，是否每发送一次短信都需要进行审核？
个人认证用户使用控制台的发送功能是需先经过审核后才可以发送的，建议升级为企业认证用户。


### 给某个号码发送了短信，但是该号码未收到短信且控制台短信发送记录查询不到该号码，该怎么处理？
- 若是通过控制台发送的，建议检查发送文件里号码是否有其他字符，需要删除多余字符。
- 若是通过接口发送的，建议查看数据是否有正常请求给腾讯云，是否有响应返回。


### 境外的服务器是否可以正常发送短信？
境外服务器可以调用接口发送短信，域名就近解析，您可以先用 curl 接口测试。

### 是否支持短信群发？
支持短信群发，调用 [发送短信 API](https://intl.cloud.tencent.com/document/product/382/34859) 时一次最多不要超过200个手机号，通过控制台群发时单次最多上传10万个手机号。

### 是否支持号码去重？
从控制台导入号码，平台会针对相同属性的一批号码自动做去重处理。
在一次发送短信的请求中，平台会校验同一短信内容的接收号码是否存在重复，针对重复号码只会正常发送一条。

### 是否可以开发票？
如果您需要开具发票，可以进入控制台，在【[发票管理](https://console.cloud.tencent.com/expense/invoice)】页面申请。

### 为什么预览短信内容时，数字会出现星号？例如`尊敬的客户，您充值的1**2元已到账，请在系统查看！`
控制台会对数字进行加密入库，所以预览时数字会出现星号，但用户接收到的短信是正常显示的。

### 国家（或地区）码分别是多少？
国家（或地区）码详情请参阅 [国际/港澳台短信日结后付费价格表](https://intl.cloud.tencent.com/document/product/382/8414)。

### 地域是什么？
地域（Region）是指物理的数据中心的地理区域。腾讯云短信国际站目前包括新加坡和欧洲法兰克福，不同地域之间完全隔离，数据只存在本地域，不跨区域存储，建议您根据各地区数据存储要求选择地域。各地域之间产品功能和刊例价无差异，但是各地域数据不互通，仅支持不同地域间已审核通过的签名和模板相互复制。

### 我该怎么选择地域？
各地域之间产品功能和刊例价无差异，不同地域之间完全隔离，数据只存在本地域，不跨区域存储，建议您根据各地区数据存储要求选择地域。如果您的用户为欧盟用户，建议选择欧洲法兰克福地域。您可在控制台标题栏切换选择不同“地域”，或者通过API接入的时候明确region字段。查看[地域列表](https://intl.cloud.tencent.com/document/api/382/40466?lang=en#region-list)
