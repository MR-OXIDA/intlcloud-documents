### 视频播放失败时，如何定位问题？
视频播放失败有多种原因，定位问题的基本思路是：

1. 配置网络抓包，查看网络请求情况。
2. 查看浏览器控制台报错情况。
3. 检查视频格式，使用的浏览器是否支持播放。


### 视频同时在线观看人数是否有限制？

理论上没有，我们的系统目前不做任何限制，因此理论上可支持无限用户数量的同时在线观看。


### 如何解决视频播放会有卡顿现象的问题？

在排除视频文件本身问题的情况下，视频卡顿有可能是因为播放视频的电脑配置过低或局部网络条件欠佳（包括带宽和时延）引起的，可以通过改变播放视频的硬件设备或网络环境来尝试分析。如果问题仍然存在，请 [联系我们](https://intl.cloud.tencent.com/document/product/266/19905)。

### 如何解决在 HTTPS 协议的页面播放 HTTP 协议的视频，被浏览器拦截的问题？
浏览器会处于安全考虑进行拦截。因此，在 HTTP 协议的页面播放 HTTP 的视频，HTTPS 协议的页面播放 HTTPS 的视频。

### 如何解决 CDN 无视频，访问视频地址返回404的问题？
请 [联系我们](https://intl.cloud.tencent.com/document/product/266/19905) 定位并修复 CDN 资源。

### 如何解决访问视频地址返回403，无法加载视频的问题？
需确认是否开启 referer 防盗链或者 key 防盗链，视频播放时是否具备校验参数。


### 如何解决 PC 端无法播放视频，浏览器控制台报跨域相关错误的问题？
在 PC 端使用 Flash 播放视频时，视频存储服务器需要部署`crossdomain.xml`文件并配置正确的访问策略，以及开启 CORS 支持。

**crossdomain.xml 的作用**
- 位于`www.a.com`域中的 SWF 文件要访问`www.b.com`的文件时，SWF 首先会检查`www.b.com`服务器根目录下是否有`crossdomain.xml`文件，如果没有，则访问不成功；如果`crossdomain.xml`文件存在，且文件内设置了允许`www.a.com`域访问，则通信正常。
- `crossdomain.xml`中配置的是 SWF 文件的域名。

在 PC 端的现代浏览器使用 HTML5 播放 HLS 和 FLV 时，视频服务器需要配置跨域资源共享 [CORS](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS)。
正常情况下，腾讯云服务会自动配置这两项跨域策略，如遇到异常情况请 [联系我们](https://intl.cloud.tencent.com/document/product/266/19905)。

### 如何解决播放器提示视频未转码的问题？
对视频进行转码操作，具体操作请参见 [处理视频](https://intl.cloud.tencent.com/document/product/266/33892)，确保视频编码格式为 H.264，视频封装格式为 MP4 或者 HLS。

### 能否为不同的视频观看者打不同的水印？
云点播仅支持在转码时指定固定的图片或文字水印，不支持随观看者的不同打动态水印。

### 能否对视频做配音、混音、亮度调节、画面旋转、画中画等编辑？
可以，请参见云点播视频处理功能中的 [视频合成](https://intl.cloud.tencent.com/document/product/266/33936) 功能。

### 如何解决转码后的视频出现花屏、黑屏、卡顿和无法播放等现象的问题？
需要定位原始视频是否有问题，如果是转码问题请 [联系我们](https://intl.cloud.tencent.com/document/product/266/19905)。

### 浏览器环境不支持播放时会有什么提示？
通常情况下在 Web 端播放视频依赖浏览器自带的解码器，或者 Flash 解码器，不支持播放会出现 error code 为3或4的错误。

### 如何解决无法播放 RTMP 和 FLV 格式的视频，或者无法在 IE 浏览器中播放视频的问题？
播放 RTMP、FLV 格式的视频以及在 IE 中播放视频都依赖 Flash 插件，请安装并启用 Flash 插件。

### 如何解决在 PC 浏览器不支持 Flash 的情况下，使用 H5 方式无法播放 HLS、FLV 格式视频的问题？
不支持 Flash 的情况下，播放器将使用 MSE 播放 HLS、FLV 格式的视频，如浏览器不支持，只能更换或升级浏览器，目前支持通过 MSE 播放 HLS、FLV  格式视频的浏览器有 Edge、Chrome、Firefox 和 Safari11+。

### 如何解决浏览器不支持解码 H.264 或者不支持播放 MP4、HLS 格式视频的问题？
通常出现在部分 PC 软件或者 App 集成精简版本的浏览器内核中，没有对应的视频解码器。在 PC 软件或 App 中升级浏览器内核，或者集成 Flash 插件，并允许调用 Flash 插件。

### 如何防止视频被其他人下载并播放？
网络上视频播放的原理，就是下载后播放，因此不能防止他人下载视频。如果您希望自己的视频被他人下载后不能被随意播放，请参见云点播的 [视频加密](https://intl.cloud.tencent.com/document/product/266/33968)。

### 如何解决 HLS 加密视频播放失败的问题？
HLS 加密视频的播放流程有别于常规视频，通常需要确保获取 key 这个步骤是正常的，解决步骤如下：
1. 检查 M3U8 文件格式是否符合规范，获取密钥的地址是否正确，密钥接口服务端鉴权是否正常，密钥接口是否正常返回。
2. 检查密钥长度，确保密钥长度为16字节，并且是能正确解密的密钥。

### 如何解决拖拽到某个时间点无法播放，或者跳到片头的问题？
避免使用原始视频进行播放，请使用腾讯云转码后的视频进行播放。避免使用 Flash 进行播放，请切换 HTML5 播放模式。如果视频时长过短，关键帧通常只有1个，不支持拖拽播放。

### 如何解决自动播放失败的问题？
在许多浏览器中，都禁止了多媒体文件自动播放，特别是移动端浏览器。部分浏览器允许静音视频或者无音轨视频自动播放，因此可以尝试将播放器设置为静音。对于静音也无法播放的浏览器，暂无解决办法。

### 如何解决在 Hybrid App 的 WebView 中自动播放失败的问题？
需要设置 WebView 关于多媒体自动播放的属性：
- iOS：mediaPlaybackRequiresUserAction = NO
- Android：webView.getSettings().setMediaPlaybackRequiresUserGesture(false)

### 如何解决播放器初始化后看不到视频画面的问题？
Web 播放器是否显示视频的首帧画面取决于该浏览器是否支持，目前并非所有浏览器都支持首帧画面，解决方案为设置视频的封面。

### 如何解决播放器没有变速播放按钮或者变速功能不可用的问题？
目前只有部分现代浏览支持 HTML5 播放模式的变速播放功能，且 Flash 播放模式不支持变速播放，因此不支持 HTML5 模式播放的浏览器也不支持变速播放。
可以优先使用 HTML5 模式播放，如果没有出现变速播放按钮，说明当前播放模式不支持变速播放；如果出现变速播放按钮，但切换没有效果，说明播放器检测到当前浏览器支持设置变速播放接口，但实际设置后没有效果，建议在此浏览器下隐藏变速播放按钮。


### 如何解决视频无法被其他元素覆盖的问题？
播放器控件为浏览器自带控件，需要浏览器厂商提供方法解除视频置顶，暂无通用解决方案。

### 如何解决播放器出现多余图标的问题？
可以尝试隐藏 video 标签，当监听到视频开始播放的事件时，再将 video 标签显示。

### 如何解决播放器出现广告、下载、推荐视频等内容的问题？
广告投放（如微信播放视频出现广告）属于浏览器厂商劫持行为，需要浏览器厂商提供关闭方法，暂无通用解决方案。

### 如何解决 Android 端播放视频不会随着页面滑动的问题？
经测试发现，通过前端方法无法有效解决此类问题，浏览器劫持视频播放后，没有做好优化体验，可以尝试直接使用 video 标签播放（不通过播放器生成）或者尝试使用 Canvas 绘制视频，如果仍无法解决，只能通过升级浏览器来解决。

### 如何解决播放器播放视频时出现黑边的问题？
设置播放器的尺寸比率与视频实际的尺寸比率一致。
例如，视频的分辨率为1280 x 720，播放器的尺寸可以设置为640 x 360或者1280 x 720等，只要满足16:9（1280:720）的宽高比，就能完全显示视频，播放器不会出现黑边。如果视频自带黑边，则需要在转码的时候切掉视频的黑边内容，改变视频的分辨率。

### 如何解决推流端切换横竖屏，播放端不切换的问题？
Web 播放器目前无法检测到推流端进行了横竖屏切换，只能通过其他途径进行处理。
例如，推流开始时是竖屏模式，上行视频宽高比为9:16，Web 播放端播放也是9:16，这时推流设备不断流（是否断流需要推流 SDK 支持）且变成横屏模式，上行视频宽高比变为16:9，如果下行视频也变成16:9，需要将 Web 播放端重新链接才能播放宽高比切换后的视频，这个操作需要外部的接口通知 Web 播放器。 如果下行视频还是9:16，视频将继续按9:16播放。


### 云点播播放地址是否支持 HTTP 的 DNS 协议？
云点播播放地址目前暂不支持 HTTP 的 DNS 协议。

### 使用云点播在电脑端不能播放视频，而手机端却可以播放？
您需要在 PC 浏览器中启用 Flash 插件。

### 点播业务支持植入广告吗？
广告功能还没上线。您可以使用播放器的贴片功能做广告，或者定制 Web 播放器，自行实现广告功能，相关文档请参见 [TCPlayerLite](https://www.qcloud.com/document/product/267/5706)。

### 云点播上传的视频是否需要转码后才能播放？
云点播不强制用户进行转码，**但是非转码的文件在第三方平台播放可能会有播放问题，建议转码后播放**。

### 两个相同分辨率、码率的视频，编辑合并之后码率下降了，应该如何保持码率？

指定目标码率和原始码率一致，编码环节也会根据情况分配码率，可能出现实际转码码率「不需要那么高指定的码率」的情况，通常导致视频码率降低，但是视频画面质量不会有明显的降低。如果有明显降低请 [提交工单](https://console.cloud.tencent.com/workorder/category)。

### 加密后的视频是否可以缓存播放 ？

不可以，视频解密以后可以进行播放和缓存。


