伪直播依托于点播的播放控制能力，将点播文件增加“限制观看时间”和“同步观看进度”两种访问控制的功能，使点播文件达成类直播效果，用户可以首先生成点播文件，在指定的直播时间使用点播文件进行类直播分发，有效的降低直播的风险与成本。

## 功能特性
- **开发成本低**：如果选择将点播视频转为标准的直播进行分发，那么用户需要将视频经由 OBS 软件推流到直播平台，并对接整套直播系统，开发成本高。相比之下，伪直播都在云点播内部实现，用户只需要启用转码和防盗链功能即可。
- **违规风险低**：使用伪直播能力，用户可以提前对自己的点播文件进行审核和编辑，有效规避直播过程中可能涉及的违规风险，规避不合规内容，提升直播质量。
- **创建简单灵活**：
	- 没有直播房间的概念，任何视频都可以随时生成伪直播。
	- 没有并发数限制，可以指定好开播时间并预先分发观看链接。

## 应用场景
- 主要应用于视频需要提前录制完毕，按照预定的时间安排让用户同步观看。用户可以提前获取到观看入口，但在预定时间点开始之前无法观看到视频。
- 伪直播进行过程中无法快进，常见于在线教学视频、直播晚会和广电等行业。

## 使用说明

### 使用限制
伪直播本质上是点播，因此并不具备标准直播的一些能力，例如：
- 不支持对“一场”伪直播进行数据统计。
- 无法感知“一场”伪直播的开始和结束。
- 不支持对正在进行的伪直播做暂停/终止等操作。
- 不支持对已分发出去的伪直播链接进行禁用。
- 不支持动态改变视频内容（例如实时转码、打水印等）。

### 名词解释
**限制允许观看的时间**：视频入口可以提前分发给观众，在伪直播开始之前或结束之后，观众都无法观看；只有在伪直播“进行”过程中才能够观看。
**同步观看进度**：在伪直播“进行”过程中，所有观众的观看进度都是同步的（存在分钟级别的偏移）。


## 前提条件
- [注册](https://intl.cloud.tencent.com/register) 并 [登录](https://intl.cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fcloud.tencent.com) 腾讯云账号，并且完成账号实名认证，未进行实名认证的用户无法购买中国大陆的伪直播实例。
- 已开通腾讯云直播和云点播服务。若未开通，请前往开通 [云直播服务](https://console.cloud.tencent.com/live/livestat) 和 [云点播服务](https://console.cloud.tencent.com/vod/overview)。
- 进行直播录制，详情请参见 [直播录制转点播](https://intl.cloud.tencent.com/document/product/266/39562)。

## 实践步骤
### 步骤1：上传视频到云点播
在 [云点播控制台](https://console.cloud.tencent.com/vod/media) （非管理员）左侧导航栏，选择【媒资管理】>【视频管理】，单击【上传视频】。
![](https://qcloudimg.tencent-cloud.cn/raw/fae7f0c7f7a7fba65da7a947903b58ad.png)
您也可根据业务情况选择合适的方法将视频文件上传到云点播，更多上传方式可参见 [媒体上传综述](https://intl.cloud.tencent.com/document/product/266/9760) 和 [直播录制转点播](https://intl.cloud.tencent.com/document/product/266/39562)。

### 步骤2：将视频转码为 HLS[](id:HLS)
1. 使用伪直播必须基于 HLS 格式，您可以按照 [转码任务发起](https://intl.cloud.tencent.com/document/product/266/33938) 的说明将已上传的视频转码为 HLS（具体的 [转码模版](https://intl.cloud.tencent.com/document/product/266/14059) 请根据业务进行选择）。
2. 转码完成后，在控制台 [媒资管理](https://intl.cloud.tencent.com/document/product/266/33895) 中查看 HLS 的 URL，或者通过接收 [事件通知](https://intl.cloud.tencent.com/document/product/266/33938) 的方式获取 HLS 的 URL。
![](https://qcloudimg.tencent-cloud.cn/raw/ca003d8a162fb814938888b5678e6f33.png)

### 步骤3：开启 Key 防盗链
1. 使用伪直播必须开启防盗链，请登录 [云点播控制台](https://console.cloud.tencent.com/vod)，选择左侧导航栏的【分发播放设置】>【域名管理】，单击目标域名所在行的【设置】，进入域名相关设置页面。
![](https://qcloudimg.tencent-cloud.cn/raw/f21443e506aab6c9020d4a98575c1e7b.png)
2. 单击【编辑】去开启 Referer 防盗链。
![](https://qcloudimg.tencent-cloud.cn/raw/e4fecb5f16b4157959b86acbc9d33ee0.png)
2. 开启 Referer 防盗链、Key 防盗链。
![](https://qcloudimg.tencent-cloud.cn/raw/7f13f03767df78e476012158fb44eebd.png)
更多选项说明，请参见 [设置防盗链](https://intl.cloud.tencent.com/document/product/266/14060)。完成设置后，请保存防盗链 KEY 的内容用于以下的防盗链签名计算。

### 步骤4：计算防盗链签名
#### 签名计算公式[](id:function)
```plaintext
sign = md5(KEY + Dir + t + plive + exper + rlimit + us)
```
>!伪直播的防盗链参数比 [标准的 Key 防盗链](https://intl.cloud.tencent.com/document/product/266/33986) 多一个参数：`plive`。在计算防盗链签名时，`plive` 需要参与计算。

| 参数名 | 取值                   | 说明                                               |
| ------ | ---------------------- | -------------------------------------------------- |
| KEY    | 11111111| 开发者开通 Key 防盗链时选择的密钥。                  |
| Dir    | /dir1/dir2/          | 原始播放 URL 的 PATH 中除去 myVideo.mp4 的剩余部分。 |
| t      | 5a71afc0             | 过期时间戳1517400000的十六进制表示结果。             |
|plive|5e344f00|表示该场伪直播的开始时间（北京时间），以 UNIX 时间戳的形式表示。例如1577808000表示2020-01-01 00:00:00这个时间点。|
|exper|0|试看时长，0 表示不限制。|
|rlimit|0|观看 IP 数限制，0 表示不限制。|
| us     | test| 生成的随机字符串。                                   |


例如某个开发者在云点播有一视频，其 HLS URL （而非原始视频的 URL）播放地址：`http://1250000000.vod2.myqcloud.com/vodtranscq125000000/12345678/v.f240.m3u8；`现有如下需求：
- HLS URL 防盗链 KEY 为 `11111111`。
- 有效截止时间 t 为 `5e5a8a80`（即2020-03-01 00:00:00）。
- 伪直播开始时间 plive 为 `5e344f00`（即2020-02-01 00:00:00）。
- 试看时长 exper 为 `0`（即不限制）。
- 观看 IP 数限制 rlimit 为 `0`（即不限制）。
- 随机字符串 us 为 `test`。


1. 根据 [签名计算公式](#function) 来计算签名：
```plaintext
sign = md5(11111111/vodtranscq125000000/12345678/5e5a8a805e344f0000test) = 0af5018df88c00e6629e0fb8939277dd
```
2. 将计算后的签名拼接到 HLS URL 的 QueryString 中，最终生成的防盗链链接：
```plaintext
http://1250000000.vod2.myqcloud.com/vodtranscq125000000/12345678/v.f240.m3u8?t=5e5a8a80&plive=5e344f00&exper=0&rlimit=0&us=test&sign=0af5018df88c00e6629e0fb8939277dd
```

>?
>- 防盗链链接 QueryString 中参数顺序需要和计算 `sign` 时一样，即：`t-plive-exper-rlimit-us-sign`。
>- 为了方便开发者调试，我们提供了 [防盗链签名生成工具页面](https://vods.cloud.tencent.com/referer/gen_video_url.html)。按页面内容填写参数后即可查看签名计算的中间结果和最终防盗链链接。

## 体验伪直播
在支持 HLS 播放的播放器中（例如 Safari 浏览器、VLC、PotPlayer 等。）访问上述防盗链链接，即可直接体验。
>!Chrome 浏览器默认不支持 HLS，需要安装插件。
