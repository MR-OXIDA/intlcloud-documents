本文介绍 JSON 函数的基本语法及示例。

<table>
	<tr><th>函数名称</th><th>语句</th><th>含义</th></tr>
	<tr><td><a href="#json_array_contains">json_array_contains 函数</a></td><td>json_array_contain(x，value)</td><td>判断 JSON 数组中是否包含某个值。</td></tr>
	<tr><td><a href="#json_array_get">json_array_get 函数</a></td><td>json_array_get(x，index)</td><td>获取 JSON 数组中某个下标对应的元素。</td></tr>
	<tr><td><a href="#json_array_length">json_array_length 函数</a></td><td>json_array_length(x) </td><td>计算 JSON 数组中元素的数量。 </td></tr>
	<tr><td><a href="#json_extract">json_extract 函数</a></td><td>json_extract(x，json_path)</td><td>从 JSON 对象或 JSON 数组中提取一组 JSON 值（数组或对象）。</td></tr>
	<tr><td><a href="#json_extract_scalar">json_extract_scalar 函数</a></td><td>json_extract_scalar(x，json_path)</td><td>从 JSON 对象或 JSON 数组中提取一组标量值（字符串、整数或布尔值）。类似于 json_extract 函数。</td></tr>
	<tr><td><a href="#json_format">json_format 函数</a></td><td>json_format(x)</td><td>把 JSON 类型转化成字符串类型。</td></tr>
	<tr><td><a href="#json_parse">json_parse 函数</a></td><td>json_parse(x)</td><td>把字符串类型转化成 JSON 类型。</td></tr>
	<tr><td><a href="#json_size">json_size 函数</a></td><td>json_size(x，json_path)</td><td>计算 JSON 对象或数组中元素的数量。</td></tr>
</table>

<span id="json_array_contains"></span>
## json_array_contains 函数

json_array_contains 函数用于判断 JSON 数组中是否包含某个值。

### 语法

```
json_array_contains(x, value)
```

### 参数说明

| 参数  | 说明               |
| ----- | ------------------ |
| x     | 参数值为 JSON 数组。 |
| value | 数值。             |

### 返回值类型

boolean 类型。

### 示例

判断 JSON 字符[1，2，3]中是否包含2。

- 查询和分析语句
```
* | SELECT json_array_contains('[1, 2, 3]', 2)
```
- 查询和分析结果



<span id="json_array_get"></span>
## json_array_get 函数

json_array_get 函数用于获取 JSON 数组中某个下标对应的元素。

### 语法

```
json_array_get(x, index)
```

### 参数说明

| 参数  | 说明                |
| ----- | ------------------- |
| x     | 参数值为 JSON 数组。  |
| index | JSON 下标，从0开始。 |

### 返回值类型

varchar类型。

### 示例

返回 JSON 数组["a", [3, 9], "c"]下标为1的元素。

- 查询和分析语句
```
* | SELECT json_array_get('["a", [3, 9], "c"]', 1)
```
- 查询和分析结果



<span id="json_array_length"></span>
## json_array_length 函数

json_array_length 函数用于计算 JSON 数组中元素的数量。

### 语法

```
json_array_length(x)
```

### 参数说明

| 参数 | 说明               |
| ---- | ------------------ |
| x    | 参数值为 JSON 数组。 |

### 返回值类型

bigint 类型。

### 示例

- 示例1：计算 **apple.message** 字段值中 JSON 元素的数量。
  - 字段样例
```
apple.message:[{"traceName":"StoreMonitor"},{"topicName":"persistent://apache/pulsar/test-partition-17"},{"producerName":"pulsar-mini-338-36"},{"localAddr":"pulsar://pulsar-mini-broker-5.pulsar-mini-broker.pulsar.svc.cluster.local:6650"},{"sequenceId":826},{"storeTime":1635905306062},{"messageId":"19422-24519"},{"status":"SUCCESS"}]
```
- 查询和分析语句
```
* | SELECT json_array_length(apple.message)
```
- 查询和分析结果



<span id="json_extract"></span>
## json_extract 函数

json_extract 函数用于从 JSON 对象或 JSON 数组中提取一组 JSON 值（数组或对象）。

### 语法

```
json_extract(x, json_path)
```

### 参数说明

| 参数      | 说明                                    |
| --------- | --------------------------------------- |
| x         | 参数值为 JSON 对象或 JSON 数组。            |
| json_path | JSON 路径，格式为 $.store.book[0].title。 |

### 返回值类型

JSON 格式的 string 类型。

### 示例

获取 **apple.instant** 字段中 **epochSecond** 的值。

- 字段样例
```
apple.instant:{"epochSecond":1635905306,"nanoOfSecond":63001000}
```
- 查询和分析语句
```
* | SELECT json_extract(apple.instant, '$.epochSecond')
```
- 查询和分析结果



<span id="json_extract_scalar"></span>
## json_extract_scalar 函数

json_extract_scalar 函数用于从 JSON 对象或 JSON 数组中提取一组标量值（字符串、整数或布尔值）。

### 语法

```
json_extract_scalar(x, json_path)
```

### 参数说明

| 参数      | 说明                                    |
| --------- | --------------------------------------- |
| x         | 参数值为 JSON 数组。                      |
| json_path | JSON 路径，格式为 $.store.book[0].title。 |

### 返回值类型

varchar 类型。

### 示例

从 **apple.instant** 字段中获取 **epochSecond** 字段的值，并将该值转换为 bigint 类型进行求和。

- 字段样例
```
apple.instant:{"epochSecond":1635905306,"nanoOfSecond":63001000}
```
- 查询和分析语句
```
* | SELECT sum(cast(json_extract_scalar(apple.instant,'$.epochSecond') AS bigint) )
```
- 查询和分析结果



<span id="json_format"></span>
## json_format 函数

json_format 函数用于将 JSON 类型转化成字符串类型。

### 语法

```
json_format(x)
```

### 参数说明

| 参数 | 说明               |
| ---- | ------------------ |
| x    | 参数值为 JSON 类型。 |

### 返回值类型

varchar 类型。

### 示例

将 JSON 数组[1,2,3]转换为字符串[1, 2, 3]。

- 查询和分析语句
```
* | SELECT json_format(json_parse('[1, 2, 3]'))
```
- 查询和分析结果



<span id="json_parse"></span>
## json_parse 函数

json_parse 函数只用于将字符串类型转化成 JSON 类型，判断是否符合 JSON 格式。

### 语法

```
json_parse(x)
```

### 参数说明

| 参数 | 说明             |
| ---- | ---------------- |
| x    | 参数值为字符串。 |

### 返回值类型

JSON类型。

### 示例

将 JSON 数组[1,2,3]转换为字符串[1, 2, 3]。

- 查询和分析语句
```
* | SELECT json_parse('[1, 2, 3]')
```
- 查询和分析结果



<span id="json_size"></span>
## json_size 函数

json_size 函数用于计算 JSON 对象或 JSON 数组中元素的数量。

### 语法

```
json_size(x, json_path)
```

### 参数说明

| 参数      | 说明                         |
| --------- | ---------------------------- |
| x         | 参数值为 JSON 对象或 JSON 数组。 |
| json_path | JSON 路径，格式为 $.store.book[0].title。            |

### 返回值类型

bigint 类型。

### 示例

将 JSON 数组[1,2,3]转换为字符串[1, 2, 3]。

- 查询和分析语句
```
* | SELECT json_size(json_parse('[1, 2, 3]'))
```
- 查询和分析结果



