## 功能描述
DescribeMediaTemplates 用于搜索转码模板。

## 请求

#### 请求示例

```shell
GET /template HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

```

>?Authorization: Auth String （详情请参见 [请求签名](https://intl.cloud.tencent.com/document/product/436/7778) 文档）。


#### 请求头

此接口仅使用公共请求头部，详情请参见 [公共请求头部](https://intl.cloud.tencent.com/document/product/1045/43609) 文档。

#### 请求体
该请求的请求体为空。

#### 请求参数
参数的具体内容如下：

|节点名称（关键字）|父节点     |描述                    |   类型    |   必选    |
|:---           |:--       |:--                    |   :--     |   :--    |
| tag           | 无        | 模板Tag：Transcode       | String    |是|
| category      | 无   | Official，Custom，默认值: Custom | String    |是|
| ids           | 无        | 模板 ID，以`,`符号分割字符串  | String     |否|
| name          | 无        | 模板名称前缀              | String     |否|
| pageNumber    | 无        | 第几页                   | Integer     |否|
| pageSize      | 无        | 每页个数                 | Integer     |否|


## 响应

#### 响应头

此接口仅返回公共响应头部，详情请参见 [公共响应头部]( https://intl.cloud.tencent.com/document/product/1045/43610) 文档。

#### 响应体
该响应体返回为 **application/xml** 数据，包含完整节点数据的内容展示如下：

``` shell
<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhfMjc=</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <TemplateList>
        <TemplateId>A</TemplateId>
        <Name>TemplateName</Name>
        <Tag>Transcode</Tag>
        <TransTpl>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H.264</Codec>
                <Profile>high</Profile>
                <Bitrate>1000</Bitrate>
                <Crf></Crf>
                <Width>1280</Width>
                <Height></Height>
                <Fps>30</Fps>
                <Gop></Gop>
                <Preset>medium</Preset>
                <ScanMode></ScanMode>
                <Bufsize>0</Bufsize>
                <Maxrate>0</Maxrate>

            </Video>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>128</Bitrate>
                <Channels>4</Channels>
            </Audio>
            <TransConfig>
                <AdjDarMethod>scale</AdjDarMethod>
                <IsCheckReso>false</IsCheckReso>
                <ResoAdjMethod>1</ResoAdjMethod>
            </TransConfig>
            <TimeInterval>
                <Start>0</Start>
                <Duration>60</Duration>
            </TimeInterval>
        </TransTpl>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </TemplateList>
</Response>
```

具体的数据内容如下：

| 节点名称（关键字） | 父节点 | 描述           | 类型      |
| :----------------- | :----- | :------------- | :-------- |
| Response           | 无     | 保存结果的容器 | Container |

Container 节点 Response 的内容：

| 节点名称（关键字） | 父节点   | 描述                           | 类型      |
| :----------------- | :------- | :----------------------------- | :-------- |
| RequestId          | Response | 请求的唯一 ID                   | String    |
| TotalCount         | Response | 模板总数                       | Int       |
| PageNumber         | Response | 当前页数，同请求中的 pageNumber | Int       |
| PageSize           | Response | 每页个数，同请求中的 pageSize   | Int       |
| TemplateList       | Response | 模板数组                       | Container |

Container节点 TemplateList 的内容：

| 节点名称（关键字） | 父节点                | 描述                                                         | 类型      |
| :----------------- | :-------------------- | :----------------------------------------------------------- | :-------- |
| TemplateId         | Response.TemplateList | 模板 ID                                                      | String    |
| Name               | Response.TemplateList | 模板名字                                                     | String    |
| BucketId           | Response.TemplateList | 模板所属存储桶                                                | String    |
| Category           | Response.TemplateList | 模板属性，Custom 或者 Official                                | String    |
| Tag                | Response.TemplateList | 模板类型，Transcode                                          | String    |
| UpdateTime         | Response.TemplateList | 更新时间                                                     | String    |
| CreateTime         | Response.TemplateList | 创建时间                                                     | String    |
| TransTpl           | Response.TemplateList | 详细的模板参数                                                | Container |

Container节点 TransTpl 的内容：

| 节点名称（关键字） | 父节点                         | 描述     | 类型      |
| :----------------- | :----------------------------- | :------- | :-------- |
| TimeInterval       | Response.TemplateList.TransTpl | 时间区间 | Container |
| Container          | Response.TemplateList.TransTpl | 容器格式 | Container |
| Video              | Response.TemplateList.TransTpl | 视频信息 | Container |
| Audio              | Response.TemplateList.TransTpl | 音频信息 | Container |
| TransConfig        | Response.TemplateList.TransTpl | 转码配置 | Container |

TransTpl 节点 Container 的具体数据描述如下：

| 节点名称（关键字） | 父节点  | 描述                                                     | 类型      | 必选 |
| ------------------ | ------- | ---------------------------------------------------- | --------- | ---- |
| Format                | Request.Container | 容器格式：mp4，flv，hls，ts               | String    | 是   |

TransTpl 节点 Video 的具体数据描述如下：

| 节点名称（关键字）         | 父节点        | 描述                  | 类型   | 必选 | 默认值       | 限制                                                         |
| -------------------------- | ------------- | --------------------- | ------ | ---- | ------------ | ------------------------------------------------------------ |
| Codec                      | Response.TemplateList.<br/>TransTpl.Video | 编解码<br/>格式            | String | 否   |   视频原<br/>始编码 | H.264                                          |
| Width                      | Response.TemplateList.<br/>TransTpl.Video | 宽                    | String | 否   | 视频原<br/>始宽度 | <li>值范围：[128，4096]<br/><li>单位：px<br/><li> 若只设置 Width 时，按照视频原始比例计算 Height |
| Height                     | Response.TemplateList.<br/>TransTpl.Video | 高                    | String | 否   | 视频原<br/>始高度 | <li>值范围：[128，4096]<br/><li>单位：px<br/><li> 若只设置 Height 时，按照视频原始比例计算 Width |
| Fps                        | Response.TemplateList.<br/>TransTpl.Video | 帧率                  | String | 否   | 视频原<br/>始帧率 | <li>值范围：(0，60]<br><li>单位：fps<br><li>帧率超过60时，设置为60<br/>用户可以设置 fps，如果不设置，那么播放速度按照<br/>原来的时间戳。这里设置 fps 为动图的播放帧率。 |
| Remove                     | Response.TemplateList.<br/>TransTpl.Video | 是否删<br/>除视频流        | String | 否   | false        | true、false                                               |
| Profile                    | Response.TemplateList.<br/>TransTpl.Video | 编码级别              | String | 否   | high         | <li>支持 baseline、main、high<br/><li>baseline：适合移动设备；<br/><li>main：适合标准分辨率设备；<br/><li>high：适合高分辨率设备;<br/><li>仅H.264支持此参数。 |
| Bitrate                    | Response.TemplateList.<br/>TransTpl.Video | 视频输出<br/>文件的码率    | String | 否   |  视频原始码率          | <li>值范围：[10，50000]<br/><li>单位：Kbps                     |
| Crf                        | Response.TemplateList.<br/>TransTpl.Video | 码率-质量<br/>控制因子     | String | 否   | 空           | <li>值范围：[0，51]<br/><li>如果设置了 Crf，则 Bitrate 的设置失效<br/><li>默认为不设置 Crf |
| Gop                        | Response.TemplateList.<br/>TransTpl.Video | 关键帧间<br/>最大帧数      | String | 否   |  空            | 值范围：<li>[0，100000] <br/><li>默认不设置 Gop                                       |
| Preset                     | Response.TemplateList.<br/>TransTpl.Video | 视频算法<br/>器预置        | String | 否   | medium       | <li>仅H.264支持该参数<br/><li>取值 veryfast、fast、medium、slow、slower |
| Bufsize                    | Response.TemplateList.<br/>TransTpl.Video | 缓冲区<br/>大小            | String | 否   | 0            | <li>值范围：[1000，128000]<br/><li>单位：Kb<br/><li>默认值为0，表示不使用缓冲区 |
| Maxrate                    | Response.TemplateList.<br/>TransTpl.Video | 视频码率<br/>峰值          | String | 否   | 0            | <li>值范围：[10，50000]<br/><li>单位：Kbps<br/><li>默认值为0，表示不使用此参数 |
| HlsTsTime                  | Response.TemplateList.<br/>TransTpl.Video | hls 分片时间          | String | 否   | 5            | <li>值范围：(0 视频时长] <br/> <li>单位为秒 |
| Pixfmt                     | Response.TemplateList.<br/>TransTpl.Video | 视频颜色格式          | String | 否   |     yuv420p       | 支持 yuv420p、yuv422p、yuv444p、yuvj420p、yuvj422p、yuvj444p |
| LongShortMode              | Response.TemplateList.<br/>TransTpl.Video | 长短边自适应          | String | 否   | false        | true、false

TransTpl 节点 TimeInterval 的具体数据描述如下：

| 节点名称（关键字） | 父节点  | 描述                                                     | 类型      | 必选 | 默认值       | 限制  |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Start                | Response.TemplateList.<br/>TransTpl.TimeInterval | 开始时间 | String    | 否   | 0 | <li>[0 视频时长] <br/><li>单位为秒 <br/><li>支持 float 格式，执行精度精确到毫秒 |
| Duration             | Response.TemplateList.<br/>TransTpl.TimeInterval | 持续时间 | String    | 否   | 视频时长 | <li>[0 视频时长] <br/><li>单位为秒 <br/><li>支持 float 格式，执行精度精确到毫秒 |

TransTpl 节点 Audio 的具体数据描述如下：

| 节点名称（关键字） | 父节点        | 描述           | 类型   | 必选 | 默认值 | 限制                                                         |
| ------------------ | ------------- | -------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| Codec              | Response.TemplateList.<br/>TransTpl.Audio | 编解码格式     | String | 否   | aac    | 取值 aac、mp3                                                |
| Samplerate         | Response.TemplateList.<br/>TransTpl.Audio | 采样率         | String | 否   | 44100  | <li>单位：Hz<br/><li>44100、32000、44100、48000、96000<br/><li> 若视频容器格式为 flv，音频编解码格式选择为 mp3时，采样率不<br/>支持32000、48000、96000；音频编解码格式为 mp3时，采样率不支持96000 |
| Bitrate            | Response.TemplateList.<br/>TransTpl.Audio | 原始音频码率   | String | 否   | 128    | <li>单位：Kbps<br/><li>值范围：[8，1000]                       |
| Channels           | Response.TemplateList.<br/>TransTpl.Audio | 声道数         | String | 否   |  无      | <li>当 Codec 设置为 aac，支持1、2、4、5、6、8<br/><li>当 Codec 设置为 mp3，支持1、2 |
| Remove             | Response.TemplateList.<br/>TransTpl.Audio | 是否删除音频流 | String | 否   |   无    | 取值 true、false                                             |

TransTpl 节点 TransConfig 的具体数据描述如下：

| 节点名称（关键字）    | 父节点              | 描述             | 类型   | 必选 | 默认值 | 限制                                                         |
| --------------------- | ------------------- | ---------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| AdjDarMethod          | Response.TemplateList.<br/>TransTpl.TransConfig | 分辨率调整方式   | String | 否   | none   | <li>取值 scale、crop、pad、none。<br/><li>当输出视频的宽高比与原视频不等时，根据此参数做分辨率的相应调整 |
| IsCheckReso           | Response.TemplateList.<br/>TransTpl.TransConfig | 是否检查分辨率   | String | 否   | false  | <li>true、false <br/><li>当为 false 时，按照配置参数转码 |
| ResoAdjMethod         | Response.TemplateList.<br/>TransTpl.TransConfig | 分辨率调整方式   | String | 否   | 0      | <li>取值0、1；0 表示使用原视频分辨率；1表示返回转码失败<br/><li>当 IsCheckReso 为 true 时生效 |
| IsCheckVideoBitrate   | Response.TemplateList.<br/>TransTpl.TransConfig | 是否检查视频码率 | String | 否   | false  | <li>true、false <br/><li>当为 false 时，按照配置参数转码 |
| VideoBitrateAdjMethod | Response.TemplateList.<br/>TransTpl.TransConfig | 视频码率调整方式 | String | 否   | 0      | <li>取值0、1；0 表示使用原视频码率；1表示返回转码失败<br/><li>当 IsCheckVideoBitrate 为 true 时生效 |
| IsCheckAudioBitrate   | Response.TemplateList.<br/>TransTpl.TransConfig | 是否检查音频码率 | String | 否   | false  | <li>true、false <br/><li>当为 false 时，按照配置参数转码<br/> |
| AudioBitrateAdjMethod | Response.TemplateList.<br/>TransTpl.TransConfig | 音频码率调整方式 | String | 否   | 0      | <li>取值0、1；0 表示使用原音频码率；1表示返回转码失败<br/><li>当 IsCheckAudioBitrate 为 true 时生效 |

AdjDarMethod 参数图示：

![](https://qcloudimg.tencent-cloud.cn/raw/0bc73f058dcfc8ba34572fd1bcadb997.png)


#### 错误码

该请求操作无特殊错误信息，常见的错误信息请参见 [错误码](https://intl.cloud.tencent.com/document/product/1045/43609) 文档。

## 实际案例
**案例一：按照模板 ID 维度查询**
#### 请求

```shell
GET /template?ids=A,B,C HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 0
Content-Type: application/xml
```

#### 响应

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
    <TemplateList>
        <TemplateId>A</TemplateId>
        <Name>TemplateName</Name>
        <Tag>Transcode</Tag>
        <TransTpl>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H.264</Codec>
                <Profile>high</Profile>
                <Bitrate>1000</Bitrate>
                <Crf></Crf>
                <Width>1280</Width>
                <Height></Height>
                <Fps>30</Fps>
                <Gop></Gop>
                <Preset>medium</Preset>
                <ScanMode></ScanMode>
                <Bufsize>0</Bufsize>
                <Maxrate>0</Maxrate>

            </Video>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>128</Bitrate>
                <Channels>4</Channels>
            </Audio>
            <TransConfig>
                <AdjDarMethod>scale</AdjDarMethod>
                <IsCheckReso>false</IsCheckReso>
                <ResoAdjMethod>1</ResoAdjMethod>
            </TransConfig>
            <TimeInterval>
                <Start>0</Start>
                <Duration>60</Duration>
            </TimeInterval>
        </TransTpl>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </TemplateList>
    <NonExistTIDs>
        <TemplateId>B</TemplateId>
        <TemplateId>C</TemplateId>
    </NonExistTIDs>
</Response>
```

**案例二：按照分页列表维度查询**

#### 请求

```shell
GET /template?pageSize=10&pageNumber=1 HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 0
Content-Type: application/xml
```

#### 响应

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <TemplateList>
        <TemplateId>A</TemplateId>
        <Name>TemplateName</Name>
        <Tag>Transcode</Tag>
        <TransTpl>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H.264</Codec>
                <Profile>high</Profile>
                <Bitrate>1000</Bitrate>
                <Crf></Crf>
                <Width>1280</Width>
                <Height></Height>
                <Fps>30</Fps>
                <Gop></Gop>
                <Preset>medium</Preset>
                <ScanMode></ScanMode>
                <Bufsize>0</Bufsize>
                <Maxrate>0</Maxrate>
            </Video>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>128</Bitrate>
                <Channels>4</Channels>
            </Audio>
            <TransConfig>
                <AdjDarMethod>scale</AdjDarMethod>
                <IsCheckReso>false</IsCheckReso>
                <ResoAdjMethod>1</ResoAdjMethod>
            </TransConfig>
            <TimeInterval>
                <Start>0</Start>
                <Duration>60</Duration>
            </TimeInterval>
        </TransTpl>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </TemplateList>
</Response>
```
