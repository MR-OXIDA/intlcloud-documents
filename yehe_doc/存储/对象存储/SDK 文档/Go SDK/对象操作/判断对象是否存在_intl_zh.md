## 简介

本文档提供快捷查询存储桶中某个对象是否存在的示例代码。

示例代码实际调用了 COS API [HeadObject](https://intl.cloud.tencent.com/document/product/436/7745)，是该接口的简化版。

HeadObject 除了检查对象是否存在，主要功能为返回对象元数据。包含了 HeadObject 完整功能的 SDK 接口，可参见 [查询对象元数据](https://intl.cloud.tencent.com/document/product/436/37688)。


## 查询对象元数据

#### 功能说明

您可以通过 SDK 提供的快捷接口来判断对象是否存在。

#### 方法原型
```go
func (s *ObjectService) IsExist(ctx context.Context, key string, id ...string) (isExist bool, err error)
```
#### 示例代码

```go
key := "exampleobject"
ok, err := c.Object.IsExist(context.Background(), name)
if err == nil && ok {
	fmt.Printf("object exists\n")
} else if err != nil {
	fmt.Printf("head object failed: %v\n", err)
} else {
	fmt.Printf("object does not exist\n")
}
```
#### 参数说明

| 参数名称 | 描述                                                         | 类型   |      |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key      | 对象键（Key）是对象在存储桶中的唯一标识。例如，在对象的访问域名`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`中，对象键为 doc/pic.jpg | string | 是   |
| id       | 对象 VersionId。                                             | string | 否   |

#### 返回结果说明

| 参数名称               | 描述                                                         | 类型   |
| ---------------------- | ------------------------------------------------------------ | ------ |
| isExist | 对象是否存在                    | bool |
| err |  请求是否成功 | struct |