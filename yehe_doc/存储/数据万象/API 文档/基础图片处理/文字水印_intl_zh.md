## 功能概述
腾讯云数据万象通过 **watermark** 接口提供实时文字水印处理功能。目前支持大小在20M以内、长宽小于9999像素的图片处理。

## 接口形式

```http
download_url?watermark/2/text/<encodedText>
                        /font/<encodedFont>
                        /fontsize/<fontSize>
                        /fill/<encodedColor>
                        /dissolve/<dissolve>
                        /gravity/<gravity>
                        /dx/<dx>
                        /dy/<dy>
                        /batch/<type>
                        /degree/<degree>
```

>请忽略上面的空格与换行符。


## 参数说明

**操作名称**：watermark，数字2，表示水印类型为文字水印。

| 参数         | 含义                                                         |
| ------------ | ------------------------------------------------------------ |
| download_url | 文件的访问链接，具体构成为`<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`，<br>例如 `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`。 |
| /text/       | 水印内容，需要经过 URL 安全的 Base64 编码                    |
| /font/       | 水印字体，需要经过 URL 安全的 Base64 编码，默认值 tahoma.ttf 。|
| /fontsize/   | 水印文字字体大小，单位为磅，缺省值13                       |
| /fill/       | 字体颜色，缺省为灰色，需设置为十六进制 RGB 格式（如 #FF0000），详情参考 [RGB 编码表](https://www.rapidtables.com/web/color/RGB_Color.html)，需经过 URL 安全的 Base64 编码，默认值为 #3D3D3D |
| /dissolve/   | 文字透明度，取值1 - 100 ，默认90（完全不透明）                |
| /gravity/    | 文字水印位置，九宫格位置（[参见九宫格方位图](#1)），默认值 SouthEast |
| /dx/         | 水平（横轴）边距，单位为像素，缺省值为0                      |
| /dy/         | 垂直（纵轴）边距，单位为像素，默认值为0                      |
| /batch/      | 平铺水印功能，可将文字水印平铺至整张图片。当 batch 设置为1时，开启平铺水印功能 |
| /degree/     | 文字水印的旋转角度设置，取值范围为0 - 360，默认0               |

<span id="1"></span>
## 九宫格方位图

九宫格方位图可为图片的多种操作提供位置参考。红点为各区域位置的原点（通过 gravity 参数选定各区域后位移操作会以相应远点为参照）。
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)

>
- 当 gravity 参数设置为 center 时，dx、dy 参数无效。
- 当 gravity 参数设置为 north 或 south 时，dx 参数无效（水印会水平居中）。
- 当 gravity 参数设置为 west 或 east 时，dy 参数无效（水印会垂直居中）。

## 示例
**添加文字水印**

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?watermark/2/text/6IW-6K6v5LqRwrfkuIfosaHkvJjlm74/fill/IzNEM0QzRA/fontsize/20/dissolve/50/gravity/northeast/dx/20/dy/20/batch/1/degree/45
```

添加文字水印后，效果如下：
![](https://main.qcloudimg.com/raw/7e72e46d082e36dfc5ec319e0ccd1664.jpg)

