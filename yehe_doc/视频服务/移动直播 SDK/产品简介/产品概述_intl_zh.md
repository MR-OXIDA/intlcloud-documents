移动直播（Mobile Live Video Broadcasting，MLVB）SDK 是云直播服务（LVB）在移动场景的延伸。相比于主要面向云对接的直播（LVB） 服务，移动直播既提供了基于 RTMP SDK 的“快速集成方案”，也提供了集标准直播（LVB）、快直播（LEB）、云点播（VOD）、即时通信（IM） 和对象存储（COS） 等多云端服务的“一体化解决方案”。


## 方案与架构

### 移动端直播功能快速集成
使用移动直播 SDK 的 RTMP 推流功能配合标准直播（LVB）和快直播（LEB）在现有 App 中快速实现直播推流，获得更佳的推流质量和更好的推流速度。同时支持 RTMP、FLV、HLS 协议及 WebRTC 协议进行直播播放，提升当前直播流的观看体验，降低全局卡顿率，能够适用于多种平台下的多种直播场景。

开通云直播服务后，只需要简单了解腾讯云直播地址的生成规则，就可以自定义自己的推流和播放地址，再配合移动直播提供的基于 RTMP SDK 的**快速集成方案**，一对推流和播放 URL + RTMP SDK 就可以为您的 App 快速添加直播能力。

![](https://qcloudimg.tencent-cloud.cn/raw/5f2d64aeb329299c775d50efe51ce7ac.png)

### 一体化集成方案

若想要为您的 App 集成一套完整且闭环的直播能力，可以通过参考 [小直播源码集](https://intl.cloud.tencent.com/document/product/1071/38147) 快速实现您的目标。

小直播综合运用了腾讯云直播 LVB、云点播 VOD、即时通信 IM 和对象存储 COS 等几项基础服务，提供了包括文字互动、弹幕消息、飘星点赞、美颜增白、动效蒙皮、连麦互动、身份认证等一系列常见的直播相关功能，并且所有功能在设计上遵循积木式堆叠原则，您可以根据自己产品的需求随意定制组合，最快一天就能搭建出一款直播类产品的原型。
![](https://main.qcloudimg.com/raw/8f8232368b4cf0aa728c268cb4fa2f43.png)

