## Feature Description
This API (`UpdateMediaTemplate`) is used to update a video montage template.

## Request

#### Sample request

```shell
PUT /template/<TemplateId> HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>? Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)
>


#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body
This request requires the following request body:

```shell
<Request>
    <Tag>VideoMontage</Tag>
    <Name>TemplateName</Name>
    <Duration></Duration>
    <Container>
        <Format>mp4</Format>
    </Container>
    <Video>
        <Codec>H.264</Codec>
        <Bitrate>1000</Bitrate>
        <Width>1280</Width>
        <Height></Height>
        <Fps>30</Fps>
    </Video>
    <Audio>
        <Codec>aac</Codec>
        <Samplerate>44100</Samplerate>
        <Bitrate>128</Bitrate>
        <Channels>4</Channels>
        <Remove>false</Remove>
    </Audio>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :---------------------------------------- | :-------- | ---- |
| Request            | None | Request container | Container | Yes   |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | 
| ------------------ | ------- | -------------------------------------------------------- | 
| Tag                | Request | Same as `Request.Tag` in the video montage template creation API `CreateMediaTemplate`.     |
| Name               | Request | Same as `Request.Name` in the video montage template creation API `CreateMediaTemplate`.    |
| Container          | Request| Same as `Request.Container` in the video montage template creation API `CreateMediaTemplate`. |
| Duration           | Request | Same as `Request.Duration` in the video montage template creation API `CreateMediaTemplate`.  |
| Video              | Request| Same as `Request.Video` in the video montage template creation API `CreateMediaTemplate`. |
| Audio              | Request| Same as `Request.Audio` in the video montage template creation API `CreateMediaTemplate`. |


## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <Tag>VideoMontage</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <VideoMontage>
            <Duration></Duration>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H.264</Codec>
                <Bitrate>1000</Bitrate>
                <Width>1280</Width>
                <Height></Height>
                <Fps>30</Fps>
            </Video>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>128</Bitrate>
                <Channels>4</Channels>
                <Remove>false</Remove>
            </Audio>
        </VideoMontage>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :----------------------------------------- | :-------- |
| Response           | None     | Response container. Same as `Response` in `CreateMediaTemplate`.  | Container |


#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Examples

#### Request

```shell
PUT /template/<TemplateId> HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml



<Request>
    <Tag>VideoMontage</Tag>
    <Name>TemplateName</Name>
    <Duration></Duration>
    <Container>
        <Format>mp4</Format>
    </Container>
    <Video>
        <Codec>H.264</Codec>
        <Bitrate>1000</Bitrate>
        <Width>1280</Width>
        <Height></Height>
        <Fps>30</Fps>
    </Video>
    <Audio>
        <Codec>aac</Codec>
        <Samplerate>44100</Samplerate>
        <Bitrate>128</Bitrate>
        <Channels>4</Channels>
        <Remove>false</Remove>
    </Audio>
</Request>
```

#### Response

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
        <Tag>VideoMontage</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <VideoMontage>
            <Duration></Duration>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H.264</Codec>
                <Bitrate>1000</Bitrate>
                <Width>1280</Width>
                <Height></Height>
                <Fps>30</Fps>
            </Video>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>128</Bitrate>
                <Channels>4</Channels>
                <Remove>false</Remove>
            </Audio>
        </VideoMontage>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```
