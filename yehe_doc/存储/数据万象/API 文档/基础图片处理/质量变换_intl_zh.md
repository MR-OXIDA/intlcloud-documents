## 功能概述

腾讯云数据万象通过 **imageMogr2** 接口对图片质量进行调节。

>该接口仅适用于 **jpg** 和 **webp** 格式的图片。

## 接口形式

```shell
download_url?imageMogr2/quality/<Quality>
                       /rquality/<quality>
                       /lquality/<quality>						
```

## 参数说明

操作名称：quality。

| 参数                | 含义                                                         |
| ------------------- | ------------------------------------------------------------ |
| download_url | 文件的访问链接，具体构成为`<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`，<br>例如`examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`。 |
| /quality/&lt;Quality>  | 图片质量，取值范围0 - 100 ，默认值为原图质量；取原图质量和指定质量的最小值；&lt;Quality&gt;后面加“!”表示强制使用指定值，例如：`90!`。 |
| /rquality/&lt;quality> | 图片的相对质量，取值范围0 - 100 ，数值以原图质量为标准。例如原图质量为80，将 rquality 设置为80后，得到处理结果图的图片质量为64（80x80%）。 |
| /lquality/&lt;quality> | 图片的最低质量，取值范围0 - 100 ，设置结果图的质量参数最小值。<br><li>例如原图质量为85，将 lquality 设置为80后，处理结果图的图片质量为85。<br><li>例如原图质量为60，将 lquality 设置为80后，处理结果图的图片质量会被提升至80。 |


## 示例

假设设置**绝对质量**为60，示例如下：
```
http://examples-1251000004.picsh.myqcloud.com/sample.jpeg?imageMogr2/quality/60
```

效果如下：
![](https://main.qcloudimg.com/raw/499501182b2989899116d958f94368a5.jpeg)

假设设置**相对质量**为60，示例如下：

```
http://examples-1251000004.cos.ap-shanghai..myqcloud.com/sample.jpeg?imageMogr2/rquality/60
```

效果如下：
![](https://main.qcloudimg.com/raw/7b111c90aca02d94d0f11991d92e64cb.jpeg)
