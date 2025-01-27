## Feature Description

This API (`CreateMediaJobs`) is used to submit a task.

## Request

#### Sample request

```shell
POST /jobs HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>?Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)


#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body
This request requires the following request body:

```shell
<Request>
  <Tag>Concat</Tag>
  <Input>
    <Object></Object>
  </Input>
  <Operation>
    <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
    <Output>
      <Region></Region>
      <Bucket></Bucket>
      <Object></Object>
    </Output>
  </Operation>
  <QueueId></QueueId>
  <CallBack></CallBack>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | ---- |
| Request            | None | Request container | Container | Yes   |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Tag                | Request | Task type: Concat                                   | String    | Yes   |
| Input              | Request | Information about the media to be operated                                         | Container | Yes   |
| Operation          | Request | Operation rule. Up to 6 operation rules are supported.                                                | Container | Yes   |
| QueueId            | Request | ID of the queue where the task is in                                         | String    | Yes   |
| CallBack           | Request | Callback address                 | String    | Yes   |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | --------------- | ------ | ---- |
| Object             | Request.Input | Media filename | String | No   |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | ---- |
| ConcatTemplate               | Request.Operation | Same as `Request.ConcatTemplate` in the concatenation template creation API `CreateMediaTemplate`.    | Container | No   |
| TemplateId                   | Request.Operation | Template ID                                        | String    | No  |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |

>!`TemplateId` is used with priority. If `TemplateId` is unavailable, the corresponding task type parameter is used.

`ConcatTemplate` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------  | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| ConcatFragment      |  Request.Operation.<br/>ConcatTemplate | Concatenation nodes    | Container array    | Yes   | None  | Multiple files are supported and they are concatenated in file order. |
| Audio               |  Request.Operation.<br/>ConcatTemplate | Audio parameter. Same as `Request.ConcatTemplate.Audio` in the concatenation template creation API `CreateMediaTemplate`.  | Container    | No   | None  | None |
| Video               |  Request.Operation.<br/>ConcatTemplate | Video parameter. Same as `Request.ConcatTemplate.Video` in the concatenation template creation API `CreateMediaTemplate`.  | Container    | No   | None  | None |
| Container               |  Request.Operation.<br/>ConcatTemplate | Container format. Same as `Request.ConcatTemplate.Container` in the concatenation template creation API `CreateMediaTemplate`.  | Container    | Yes   | None  | None |
| Index               |  Request.Operation.<br/>ConcatTemplate| Index of the `Input` node in the `ConcatFragment` sequence    | String    | No   | 0  | The number of indexes configured cannot be greater than the number of fragments specified by `ConcatFragment`. |
| DirectConcat | Request.Operation.<br/>ConcatTemplate | Simple concatenation (without transcoding). Other video and audio parameters become invalid. | String | No | false | true, false |

`ConcatFragment` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------  | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Url                 | Request.Operation.<br/>ConcatTemplate.<br/>ConcatFragment | Concatenation object address   | String    | Yes   | None   | Same as the address of the bucket object file. |
| StartTime           | Request.Operation.<br/>ConcatTemplate.<br/>ConcatFragment | Start time   | String    | No   | Video start time   | <li>[0, Video duration] </li><li>Unit: second </li>  |
| EndTime           | Request.Operation.<br/>ConcatTemplate.<br/>ConcatFragment | End time   | String    | No   | Video end time   | <li>[0, Video duration] </li><li>Unit: second </li>  |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------ | ------------------------------------------------------------ | ------ | ---- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Result file name                                             | String | Yes   |



## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
  <JobsDetail>
    <Code></Code>
    <Message></Message>
    <JobId></JobId>
    <State></State>
    <CreationTime></CreationTime>
    <EndTime></EndTime>
    <QueueId></QueueId>
    <Tag>Concat</Tag>
    <Input>
      <Object></Object>
    </Input>
    <Operation>
      <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
      <Output>
        <Region></Region>
        <Bucket></Bucket>
        <Object></Object>
      </Output>
      <MediaInfo>
      </MeidaInfo>
    </Operation>
  </JobsDetail>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Response | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| JobsDetail | Response | Task details |  Container |


`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Code               | Response.JobsDetail | Error code, which is meaningful only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error description, which is meaningful only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Task ID                               | String    |
| Tag                | Response.JobsDetail | Task type: Concat                              | String    |
| State | Response.JobsDetail | Task status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel` |  String |
| CreationTime | Response.JobsDetail | Task creation time |  String |
| StartTime | Response.JobsDetail | Task start time |  String |
| EndTime | Response.JobsDetail | Task end time |  String |
| QueueId            | Response.JobsDetail | ID of the queue where the task is in                       | String    |
| Input              | Response.JobsDetail | Input resource address of the task                   | Container |
| Operation | Response.JobsDetail | Operation rule. Up to 6 operation rules are supported. |  Container |

`Input` has the following sub-nodes:
Same as the `Request.Input` node in the request.

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| TemplateId | Response.JobsDetail.Operation | Task template ID |  String |
| Output             | Response.JobsDetail.Operation | File output address               | Container |
| MediaInfo          | Response.JobsDetail.Operation | Transcoding output video information. Not returned when there is no output video. | Container |

`Output` has the following sub-nodes:
Same as the `Request.Operation.Output` node in the request.

`MediaInfo` has the following sub-nodes:
Same as the `Response.MediaInfo` node in the `GenerateMediaInfo` API.

#### Error codes
No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Examples

**Using the concatenation template ID**

#### Request

```shell
POST /jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98****-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml



<Request>
  <Tag>Concat</Tag>
  <Input>
    <Object>test.mp4</Object>
  </Input>
  <Operation>
    <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
    <Output>
      <Region>ap-beijing</Region>
      <Bucket>aabc-1250000000</Bucket>
      <Object>concat.mp4</Object>
    </Output>
  </Operation>
  <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
  <CallBack>https://www.callback.com</CallBack>
</Request>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzh****=



<Response>
  <JobsDetail>
    <Code>Success</Code>
    <Message>Success</Message>
    <JobId>je8f65004eb8511eaaed4f377124a303c</JobId>
    <State>Submitted</State>
    <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    <EndTime></EndTime>
    <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
    <Tag>Concat</Tag>
    <Input>
      <Object>test.mp4</Object>
    </Input>
    <Operation>
      <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
      <Output>
        <Region>ap-beijing</Region>
        <Bucket>aabc-1250000000</Bucket>
        <Object>concat.mp4</Object>
      </Output>
    </Operation>
  </JobsDetail>
</Response>
```


**Using the concatenation processing parameter**

#### Request

```shell
POST /jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98****-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml



<Request>
  <Tag>Concat</Tag>
  <Input>
    <Object>test.mp4</Object>
  </Input>
  <Operation>
    <ConcatTemplate>
        <ConcatFragment>
            <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/start.mp4</Url>
        </ConcatFragment>
        <ConcatFragment>
            <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/end.mp4</Url>
        </ConcatFragment>
        <Audio>
            <Codec>mp3</Codec>
            <Samplerate></Samplerate>
            <Bitrate></Bitrate>
            <Channels></Channels>
        </Audio>
        <Video>
            <Codec>H.264</Codec>
            <Bitrate>1000</Bitrate>
            <Width>1280</Width>
            <Height></Height>
            <Fps>30</Fps>
        </Video>
        <Container>
            <Format>mp4</Format>
        </Container>
    </ConcatTemplate>
    <Output>
      <Region>ap-beijing</Region>
      <Bucket>aabc-1250000000</Bucket>
      <Object>concat.mp4</Object>
    </Output>
  </Operation>
  <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
  <CallBack>https://www.callback.com</CallBack>
</Request>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzh****=



<Response>
  <JobsDetail>
    <Code>Success</Code>
    <Message>Success</Message>
    <JobId>jabcxxxxfeipplsdfwe</JobId>
    <State>Submitted</State>
    <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    <EndTime></EndTime>
    <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
    <Tag>Concat</Tag>
    <Input>
      <Object>test.mp4</Object>
    </Input>
    <Operation>
        <ConcatTemplate>
            <ConcatFragment>
                <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/start.mp4</Url>
            </ConcatFragment>
            <ConcatFragment>
                <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/end.mp4</Url>
            </ConcatFragment>
            <Audio>
                <Codec>mp3</Codec>
                <Samplerate></Samplerate>
                <Bitrate></Bitrate>
                <Channels></Channels>
            </Audio>
            <Video>
                <Codec>H.264</Codec>
                <Bitrate>1000</Bitrate>
                <Width>1280</Width>
                <Height></Height>
                <Fps>30</Fps>
            </Video>
            <Container>
                <Format>mp4</Format>
            </Container>
        </ConcatTemplate>
        <Output>
            <Region>ap-beijing</Region>
            <Bucket>aabc-1250000000</Bucket>
            <Object>concat.mp4</Object>
        </Output>
    </Operation>
  </JobsDetail>
</Response>
```
