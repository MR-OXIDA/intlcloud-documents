### iOS 平台如何缩减安装包体积？

####  只打包 arm64 架构（荐） 

苹果 iPhone 5s 及以后的手机都可以支持只打包 x64 架构，在 XCode 中的 Build Setting 里将 Build Active Architecture Only 设置为 YES，同时将 Valid Architectures 里只写 arm64 即可，只打包单架构可减少一半的增量。
![](https://main.qcloudimg.com/raw/e8f7a3d2f5ee4c11df8b3fae4cc1ed31.png)

### Android 平台如何缩减安装包体积？

#### 1. 只打包部分 so
如果您的 App 只定位国内使用，可以只打包 `armeabi-v7a` 架构的 so 文件，这样可以将安装包增量压缩到5M以内；如果您的 App 希望上架 Google Play，可以打包  `armeabi-v7a` 和 `arm64-v8a` 两个架构的 so 文件。

具体操作方法是在当前项目的 build.gradle 里添加 `abiFilters "armeabi-v7a"` 来指定打包单架构的 so 文件，或添加 `abiFilters "armeabi-v7a","arm64-v8a"` 来指定打包双架构的 so 文件。

- 如果不打算上架 Google Play：
![](https://main.qcloudimg.com/raw/52cc4e459ce5cb922bfc01cf6f2f08ac.png)
- 如果希望上架到 Google Play：
![](https://main.qcloudimg.com/raw/a03cf098ce88a1b69b91f3920fca1ecb.png)


#### 2. 安装后下载 so（只打包 jar）

Android 版 SDK 的体积主要来自于 so 文件，如果您希望将安装包增量压缩到1M以内，可以考虑采用安装后再下载 so 的方式：

- **Step1：下载指定架构的 so 文件**
在 [Github](https://github.com/tencentyun/TRTCSDK/tree/master/Android) 文件夹下，您可以找到类似 `LiteAVSDK_TRTC_x.x.xxx.zip` 命名的压缩包，将其解压开，并找到指定架构的 so 文件。

- **Step2：将 so 文件上传到服务器**
上传 Step1 中下载到的 so 文件，上传到您的服务器（或腾讯云 [COS](https://intl.cloud.tencent.com/product/cos) 对象存储服务）上，并记录下载地址，例如 `http://xxx.com/so_files.zip`。

- **Step3：首次启动 SDK 前下载 so 文件**
在用户启动 SDK 相关功能前，例如开始播放视频之前，先用 loading 动画提示用户“正在加载相关的功能模块”。

 在用户等待过程中，App 就可以到  `http://xxx.com/so_files.zip` 下载 so 文件，并存入应用目录下（例如应用根目录下的 files 文件夹），为了确保这个过程不受运营商 DNS 劫持的影响，请在文件下载完成后校验 so 文件的完整性，防止 zip 压缩包被运营商篡改。

- **Step4：使用 API 加载 SO 文件**
等待所有 so 文件就位以后，调用 `TXLiveBase` 类（LiteAVSDK 最早的一个基础模块）中的 `setLibraryPath()` 接口，将下载 so 的目标路径设置到 SDK。之后，SDK 会到这些路径下加载需要的 so 文件并启动相关功能。

>! 如果您的 App 希望上架 Google Play，请不要使用该方案，有可能会无法上架。
