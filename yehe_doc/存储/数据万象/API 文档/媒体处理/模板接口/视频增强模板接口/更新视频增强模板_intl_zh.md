## 功能描述
UpdateMediaTemplate 用于更新视频增强模板。

## 请求

#### 请求示例

```shell
PUT /template/<TemplateId> HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>? Authorization: Auth String （详情请参见 [请求签名](https://intl.cloud.tencent.com/document/product/436/7778) 文档）。
>


#### 请求头

此接口仅使用公共请求头部，详情请参见 [公共请求头部](https://intl.cloud.tencent.com/document/product/1045/43609) 文档。

#### 请求体
该请求操作的实现需要有如下请求体：

```shell
<Request>
    <Tag>VideoProcess</Tag>
    <Name>TemplateName</Name>
    <ColorEnhance>
        <Enable>true</Enable>
        <Contrast></Contrast>
        <Correction></Correction>
        <Saturation></Saturation>
    </ColorEnhance>
    <MsSharpen>
        <Enable>true</Enable>
        <SharpenLevel></SharpenLevel>
    </MsSharpen>
</Request>
```

具体数据描述如下：

| 节点名称（关键字） | 父节点 | 描述                                      | 类型      | 是否必选 |
| :----------------- | :----- | :---------------------------------------- | :-------- | ---- |
| Request            | 无     | 保存请求的容器 | Container | 是   |

Container 类型 Request 的具体数据描述如下：

| 节点名称（关键字） | 父节点  | 描述                                                     | 
| ------------------ | ------- | -------------------------------------------------------- | 
| Tag                | Request | 同视频增强模板 CreateMediaTemplate 接口中的 Request.Tag   |
| Name               | Request | 同视频增强模板 CreateMediaTemplate 接口中的 Request.Name  |
| ColorEnhance       | Request | 同视频增强模板 CreateMediaTemplate 接口中的 Request.ColorEnhance |
| MsSharpen          | Request | 同视频增强模板 CreateMediaTemplate 接口中的 Request.MsSharpen |


## 响应

#### 响应头

此接口仅返回公共响应头部，详情请参见 [公共响应头部]( https://intl.cloud.tencent.com/document/product/1045/43610) 文档。

#### 响应体
该响应体返回为 **application/xml** 数据，包含完整节点数据的内容展示如下：

```shell
<Response>
    <Template>
        <Tag>VideoProcess</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <VideoProcess>
            <ColorEnhance>
                <Enable>true</Enable>
                <Contrast></Contrast>
                <Correction></Correction>
                <Saturation></Saturation>
            </ColorEnhance>
            <MsSharpen>
                <Enable>true</Enable>
                <SharpenLevel></SharpenLevel>
            </MsSharpen>
        </VideoProcess>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```

具体的数据内容如下：

| 节点名称（关键字） | 父节点 | 描述                                       | 类型      |
| :----------------- | :----- | :----------------------------------------- | :-------- |
| Response           | 无     | 保存结果的容器，同 CreateMediaTemplate 中的 Response | Container |

#### 错误码

该请求操作无特殊错误信息，常见的错误信息请参见 [错误码](https://intl.cloud.tencent.com/document/product/1045/43611) 文档。

## 实际案例

#### 请求

```shell
PUT /template/<TemplateId> HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml

<Request>
    <Tag>VideoProcess</Tag>
    <Name>TemplateName</Name>
    <ColorEnhance>
        <Enable>true</Enable>
        <Contrast></Contrast>
        <Correction></Correction>
        <Saturation></Saturation>
    </ColorEnhance>
    <MsSharpen>
        <Enable>true</Enable>
        <SharpenLevel></SharpenLevel>
    </MsSharpen>
</Request>
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
    <Template>
        <Tag>VideoProcess</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <VideoProcess>
            <ColorEnhance>
                <Enable>true</Enable>
                <Contrast></Contrast>
                <Correction></Correction>
                <Saturation></Saturation>
            </ColorEnhance>
            <MsSharpen>
                <Enable>true</Enable>
                <SharpenLevel></SharpenLevel>
            </MsSharpen>
        </VideoProcess>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```
