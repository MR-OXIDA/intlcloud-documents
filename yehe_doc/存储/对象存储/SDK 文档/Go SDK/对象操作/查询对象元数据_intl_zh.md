## 简介

本文档提供关于查询对象元数据操作相关的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | 查询对象元数据 | 查询对象的元数据信息                  |

## 查询对象元数据

#### 功能说明

查询 Object 的 Meta 信息（HEAD Object）。

#### 方法原型

```go
func (s *ObjectService) Head(ctx context.Context, key string, opt *ObjectHeadOptions) (*Response, error)
```

#### 请求示例

[//]: # (.cssg-snippet-head-object)
```go
key := "exampleobject"
_, err := client.Object.Head(context.Background(), key, nil)
if err != nil {
    panic(err)
}
```

#### 参数说明

```go
type ObjectHeadOptions struct {
    IfModifiedSince string 
}
```

| 参数名称        | 参数描述                                                     | 类型   | 是否必填 |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| key             | 对象键（Key）是对象在存储桶中的唯一标识。例如，在对象的访问域名`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`中，对象键为 doc/pic.jpg | string | 是   |
| IfModifiedSince | 在指定时间后被修改才返回                                     | string | 否   |

#### 返回结果说明

```go
{
    'Content-Type': 'application/octet-stream',
    'Content-Length': '16807',
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'X-Cos-Request-Id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```
通过返回结果 Response 获取。
```go
resp, err := client.Object.Head(context.Background(), key, nil)
contentType := resp.Header.Get("Content-Type")
contentLength := resp.Header.Get("Content-Length")
etag := resp.Header.Get("ETag")
reqid := resp.Header.Get("X-Cos-Request-Id")

```

| 参数名称   | 参数描述                                                     | 类型   |
| ---------- | ------------------------------------------------------------ | ------ |
| 文件元信息 | 获取文件的元信息，包括 Etag 和 X-Cos-Request-Id 等信息，也会包含设置的文件元信息 | string |
