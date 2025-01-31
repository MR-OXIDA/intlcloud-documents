本文的案例是基于实际的加工案例。通过以下案例，用户可以对数据加工有个总体、感性的认识，同时，也可以复制这些案例中的函数，完成自己的数据加工。


## 注意事项

- v 函数的使用：**v("字段A")**，意思是 value of “字段A”，即字段 A 的值。有些函数的参数是**字段**，有些函数的参数是**字段值**，常见错误是：函数参数为字段值，却没有使用**v函数**取字段值，导致函数执行失败。     
- 分发到多个日志主题，需要提前配好**目标日志主题**及其**目标名称**，目标名称用于**分发函数**，详见 [案例1：日志过滤和分发](#case1)。   
- fields_set 函数的使用：通过 fields_set 函数设置字段值，保存数据加工函数处理后的内容。例如 fields_set("A+B",op_add(v("字段A"）,v("字段B")))，意思是将字段 A 的值和字段 B 的值相加，op_add 函数需要借助 fields_set 函数来完成结果的写入和保存。

<span id="case1"></span>
## 案例1：日志过滤和分发

#### 场景描述

小王将日志采集到了 CLS，日志通过双竖线||分割，有日志的时间、日志级别、日志内容、任务 ID、进程名称、主机 IP 等。现在小王想将日志结构化，便于后续索引、仪表盘展示。并按照 **ERROR、WARNING、INFO** 三个级别，把日志**分发**到三个不同的目标日志主题中，便于后续的分析。最后，当日志内容中有 “**team B is working**” 字样时，将该条**日志过滤（丢弃）**。

#### 场景分析

梳理一下小王的加工需求，加工思路如下：  
1. 日志中如有 **team B is working** 字符，将该条日志过滤（丢弃）；并把丢弃日志放在前面，可以减少后续的运算量。  
2. 日志结构化：按照**双竖线**||分割符，对日志进行结构化。  
3. 日志分发：按照按照 **ERROR、WARNING、INFO** 三个级别，把日志分发到三个不同的目标日志主题。  

>! 分发到多个目标日志主题，需要在新建数据加工任务时，定义好日志主题的目标名称。该名称将用在 **log_output("目标名称")** 函数中。
>



#### 原始日志

``` 
[
    {
        "message": "2021-12-09 11:34:28.279||team A is working||INFO||605c643e29e4||BIN--COMPILE||192.168.1.1"
    },
    {
        "message": "2021-12-09 11:35:28.279||team A is working ||WARNING||615c643e22e4||BIN--Java||192.168.1.1"
    },
    {
        "message": "2021-12-09 11:36:28.279||team A is working ||ERROR||635c643e22e4||BIN--Go||192.168.1.1"
    },
    {
        "message": "2021-12-09 11:37:28.279||team B is working||WARNING||665c643e22e4||BIN--Python||192.168.1.1"
    }
]
```

#### DSL 加工函数

``` 
log_drop(regex_match(v("message"),regex="team B is working",full=False))
ext_sepstr("message","time,log,loglevel,taskId,ProcessName,ip",sep="\|\|")
fields_drop("message")
t_switch(regex_match(v("loglevel"),regex="INFO",full=True),log_output("info_log"),regex_match(v("loglevel"),regex="WARNING",full=True),log_output("warning_log"),regex_match(v("loglevel"),regex="ERROR",full=True),log_output("error_log"))
```

#### DSL 加工函数详解 

1. 当日志中含有 **team B is working** 关键字时，丢弃该条日志。因为第四条日志中包含有 **team B is working**，所以第四条日志会被丢弃。
``` 
log_drop(regex_match(v("message"),regex="team B is working",full=False))
```
2. 根据**双竖线**||分隔符来提取结构化数据。
``` 
ext_sepstr("message","time,log,loglevel,taskId,ProcessName,ip",sep="\|\|")
```
3. 丢弃 **message** 字段。
``` 
fields_drop("message")
```
4. 按照 **loglevel** 的字段值，**INFO/WARNING/ERROR**，将日志分发到不同的目标日志主题。
``` 
t_switch(regex_match(v("loglevel"),regex="INFO",full=True),log_output("info_log"),regex_match(v("loglevel"),regex="WARNING",full=True),log_output("warning_log"),regex_match(v("loglevel"),regex="ERROR",full=True),log_output("error_log"))
```

#### 加工结果

>! 必须要提前配置好目标日志主题和目标名称。
>

该日志分发到 **info_log**，即数据加工-目标3，可参看上图中的目标名称和日志主题的对应关系。
``` 
{"ProcessName":"BIN--COMPILE","ip":"192.168.1.1","log":"team A is working","loglevel":"INFO","taskId":"605c643e29e4","time":"2021-12-09 11:34:28.279"}
```
该日志分发到 **warning_log**，即数据加工-目标2。
``` 
{"ProcessName":"BIN--COMPILE","ip":"192.168.1.1","log":"team A is working","loglevel":"INFO","taskId":"605c643e29e4","time":"2021-12-09 11:34:28.279"}
```
该日志分发到 **error_log**，即数据加工-目标1。
``` 
{"ProcessName":"BIN--Go","ip":"192.168.1.1","log":"team A is working ","loglevel":"ERROR","taskId":"635c643e22e4","time":"2021-12-09 11:36:28.279"}
```

## 案例2：单行文本日志结构化

#### 场景描述

小王将日志采集到 CLS，但是没有固定的分割符号，是单行文本格式。现在小王想将日志结构化，从文本中**提取日志时间、日志级别、操作、URL 信息**，便于后续的检索分析。   

#### 场景分析

梳理一下小王的加工需求，加工思路如下：  
1. {...}中的内容是**操作**的详情，可以通过正则提取。  
2. 使用正则提取**日志时间、日志级别、URL**。  

#### 原始日志

``` 
{
    "content": "[2021-11-24 11:11:08,232][328495eb-b562-478f-9d5d-3bf7e][INFO] curl -H 'Host: ' http://abc.com:8080/pc/api -d {\"version\": \"1.0\",\"user\": \"CGW\",\"password\": \"123\",\"interface\": {\"Name\": \"ListDetail\",\"para\": {\"owner\": \"1253\",\"orderField\": \"createTime\"}}}"
}
```

#### DSL 加工函数

```
fields_set("Action",regex_select(v("content"),regex="\{[^\}]+\}",index=0,group=0)) 
fields_set("loglevel",regex_select(v("content"),regex="\[[A-Z]{4}\]",index=0,group=0))。 
fields_set("logtime",regex_select(v("content"),regex="\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2},\d{3}",index=0,group=0))
fields_set("Url",regex_select(v("content"),regex="([a-z]{3}).([a-z]{3}):([0-9]{4})",index=0,group=0))
fields_drop("content")
```

#### DSL 加工函数详解 

1. 新建一个字段 **Action**，使用正则\{[^\}]+\}，匹配**{...}**。  
```
fields_set("Action",regex_select(v("content"),regex="\{[^\}]+\}",index=0,group=0)) 
```
2. 新建一个字段 **loglevel**，使用正则[A-Z]{4}可以匹配 **INFO**。
```
fields_set("loglevel",regex_select(v("content"),regex="\[[A-Z]{4}\]",index=0,group=0))。
```
3. 新建一个字段 **logtime**，使用正则d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2},\d{3}匹配**2021-11-24 11:11:08**。
```  
fields_set("logtime",regex_select(v("content"),regex="\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2},\d{3}",index=0,group=0))
```
4. 新建一个字段 **Url**，使用正则[a-z]{3}.[a-z]{3}匹配 **abc.com**，[0-9]{4}匹配**8080**。  
```
fields_set("Url",regex_select(v("content"),regex="([a-z]{3}).([a-z]{3}):([0-9]{4})",index=0,group=0))
```
5. 丢弃 **content** 字段。 
```
fields_drop("content")
```

#### 加工结果

```
{"Action":"{\"version\": \"1.0\",\"user\": \"CGW\",\"password\": \"123\",\"interface\": {\"Name\": \"ListDetail\",\"para\": {\"owner\": \"1253\",\"orderField\": \"createTime\"}","Url":"abc.com:8080","loglevel":"[INFO]","logtime":"2021-11-24 11:11:08,232"}
 
```

## 案例3：数据脱敏

#### 场景描述

小王将日志采集到 CLS，日志数据中含有用户 ID（**dev@12345**）、登录的 IP 地址（**11.111.137.225**）、手机号码（**13912345678**），小王想将这些敏感信息脱敏。

#### 场景分析

该日志本身是一个结构化的日志，因此可以直接对字段进行脱敏处理。

#### 原始日志
``` 
    {
        "Id": "dev@12345",
        "Ip": "11.111.137.225",
        "phonenumber": "13912345678"
    }
```

#### DSL 加工函数

```
fields_set("Id",regex_replace(v("Id"),regex="\d{3}", replace="***",count=0))
fields_set("Id",regex_replace(v("Id"),regex="\S{2}", replace="**",count=1))
fields_set("phonenumber",regex_replace(v("phonenumber"),regex="(\d{0,3})\d{4}(\d{4})", replace="$1****$2"))
fields_set("Ip",regex_replace(v("Ip"),regex="(\d+\.)\d+(\.\d+\.\d+)", replace="$1***$2",count=0))
```

#### DSL 加工函数详解 

1. 对 **Id** 字段进行脱敏处理，结果为dev@\*\*\*45。
```
fields_set("Id",regex_replace(v("Id"),regex="\d{3}", replace="***",count=0))
```
2. 对 **Id** 字段进行二次脱敏处理，结果为\*\*v@\*\*\*45。
```
fields_set("Id",regex_replace(v("Id"),regex="\S{2}", replace="**",count=1))
```
3. 对 **phonenumber** 字段进行脱敏处理，将中间的4位数替换为\*\*\*\*，结果为139\*\*\*\*5678。
```
fields_set("phonenumber",regex_replace(v("phonenumber"),regex="(\d{0,3})\d{4}(\d{4})", replace="$1****$2"))
```
4. 对 **IP** 字段进行脱敏处理，将第二段替换为\*\*\*，结果为11.\*\*\*137.225。
```
fields_set("Ip",regex_replace(v("Ip"),regex="(\d+\.)\d+(\.\d+\.\d+)", replace="$1***$2",count=0))
```

#### 加工结果

```
{"Id":"**v@***45","Ip":"11.***.137.225","phonenumber":"139****5678"} 
```


## 案例4：嵌套 JSON 的处理

#### 场景描述

小王将日志以 JSON 格式采集到 CLS。JSON 是多层嵌套，小王想提取 **user** 和 **App** 字段。其中 **user** 是二级嵌套字段。

#### 原始日志

``` 
[
    {
        "content": {
            "App": "App-1",
            "start_time": "2021-10-14T02:15:08.221",
            "resonsebody": {
                "method": "GET",
                "user": "Tom"
            },
            "response_code_details": "3000",
            "bytes_sent": 69
        }
    },
    {
        "content": {
            "App": "App-2",
            "start_time": "2222-10-14T02:15:08.221",
            "resonsebody": {
                "method": "POST",
                "user": "Jerry"
            },
            "response_code_details": "2222",
            "bytes_sent": 1
        }
    }
]
```

#### DSL 加工函数

- 方法一：不展开所有的 KV，使用 **jmes** 公式直接提取字段。
```
ext_json_jmes("content", jmes="resonsebody.user", output="user")
ext_json_jmes("content", jmes="App", output="App")
```
- 方法二：平铺所有的 KV，丢弃不需要的字段。
```
ext_json("content")
fields_drop("content")
fields_drop("bytes_sent","method","response_code_details","start_time")
```

#### DSL 加工函数详解 

- 方法一： 
 1. 使用 jmes 公式 **resonsebody.user**，直接指定二级嵌套的 **user** 字段。
```
ext_json_jmes("content", jmes="resonsebody.user", output="user")
```
 2. 使用 jmes 公式 **App**，直接指定 **App** 字段。
```
ext_json_jmes("content", jmes="App", output="App")
```
- 方法二：  
 1. 使用 **ext_json** 函数从 JSON 数据中提取结构化数据，默认会平铺所有的字段。
```
ext_json("content")
```
 2. 丢弃 **content** 字段。
```
fields_drop("content")
```
 3. 丢弃不需要的字段 **bytes_sent,method,response_code_details,start_time**
```
fields_drop("bytes_sent","method","response_code_details","start_time")
```


#### 加工结果

```
[{"App":"App-1","user":"Tom"},
{"App":"App-2","user":"Jerry"}]
```

## 案例5：多格式的日志结构化

#### 场景描述

小王把**用户操作和结果**的日志，以单行文本的格式采集到 CLS，日志的格式和内容**不完全相同**。小王想编写一套语句，对不同格式的日志进行结构化。 
经过梳理查看，日志基本分为三种格式：第一种包含有 **uin、requestid、action、Reqbody** 四个字段，第二种包含 **uin、requestid、action** 三个字段，第三种包含 **requestid、action、TaskId** 三个字段。

#### 场景分析

梳理一下小王的加工需求，加工思路如下：  
1. 由于三种格式的日志都包含 **requestid、action** 字段，因此使用正则提取 **requestid** 和 **action** 字段。  
2. 对 **uin,reqbody,TaskId** 字段进行特殊处理，先判断这个字段是否存在，如果存在，再进行提取。

#### 原始日志

``` 
[
    {
        "__CONTENT__": "2021-11-29 15:51:33.201 INFO request 7143a51d-caa4-4a6d-bbf3-771b4ac9e135 action: Describe uin: 15432829 reqbody {\"Key\": \"config\",\"Values\": \"appisrunnning\",\"Action\": \"Describe\",\"RequestId\": \"7143a51d-caa4-4a6d-bbf3-771b4ac9e135\",\"AppId\": 1302953499,\"Uin\": \"100015432829\"}"
    },
    {
        "__CONTENT__": "2021-11-2915: 51: 33.272 ERROR request 2ade9fc4-2db2-49d8-b3e0-a6ea78ce8d96 has error action DataETL uin 15432829"
    },
    {
        "__CONTENT__": "2021-11-2915: 51: 33.200 INFO request 6059b946-25b3-4164-ae93-9178c9e73d75 action: UploadData hUWZSs69yGc5HxgQ TaskId 51d-caa-a6d-bf3-7ac9e"
    }
]
```

#### DSL 加工函数

```
fields_set("requestid",regex_select(v("__CONTENT__"),regex="request [A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+",index=0,group=0))
fields_set("action",regex_select(v("__CONTENT__"),regex="action: \S+|action \S+",index=0,group=0))
t_if(regex_match(v("__CONTENT__"),regex="uin", full=False),fields_set("uin",regex_select(v("__CONTENT__"),regex="uin: \d+|uin \d+",index=0,group=0)))
t_if(regex_match(v("__CONTENT__"),regex="TaskId", full=False),fields_set("TaskId",regex_select(v("__CONTENT__"),regex="TaskId [A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+",index=0,group=0)))
t_if(regex_match(v("__CONTENT__"),regex="reqbody", full=False),fields_set("requestbody",regex_select(v("__CONTENT__"),regex="reqbody \{[^\}]+\}")))
t_if(has_field("requestbody"),fields_set("requestbody",str_replace(v("requestbody"),old="reqbody",new="")))
fields_drop("__CONTENT__")
fields_set("requestid",str_replace(v("requestid"),old="request",new=""))
t_if(has_field("action"),fields_set("action",str_replace(v("action"),old="action:|action",new="")))
t_if(has_field("uin"),fields_set("uin",str_replace(v("uin"),old="uin:|uin",new="")))
t_if(has_field("TaskId"),fields_set("TaskId",str_replace(v("TaskId"),old="TaskId",new="")))
```

#### DSL 加工函数详解 

1. 新建一个字段 **requestid**，使用正则公式匹配 “**request 7143a51d-caa4-4a6d-bbf3-771b4ac9e135**”。
```
fields_set("requestid",regex_select(v("__CONTENT__"),regex="request [A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+",index=0,group=0))
```
2. 新建一个字段 **action**，使用正则公式匹配 “**action: UploadData**” 或者 “**action DataETL**”。因为原始日志中两种格式都有。
```
fields_set("action",regex_select(v("__CONTENT__"),regex="action: \S+|action \S+",index=0,group=0))
```
 - 如果 **\_\_CONTENT\_\_** 字段中有 **uin** 这个字符，新建 **uin** 字段，使用正则"**uin: \d+|uin \d+**"来匹配**uin: 15432829**或者**uin 15432829**。
```
t_if(regex_match(v("__CONTENT__"),regex="uin", full=False),fields_set("uin",regex_select(v("__CONTENT__"),regex="uin: \d+|uin \d+",index=0,group=0)))
```
 - 如果有 **TaskId** 这个字符，新建 **TaskId** 字段，使用正则来匹配 “**TaskId 51d-caa-a6d-bf3-7ac9e**“，。
```
t_if(regex_match(v("__CONTENT__"),regex="TaskId", full=False),fields_set("TaskId",regex_select(v("__CONTENT__"),regex="TaskId [A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+",index=0,group=0)))
```
 - 如果有 **reqbody** 这个字符，新建 **requestbody** 字段，使用正则来匹配 **reqbody{...}**。
```
t_if(regex_match(v("__CONTENT__"),regex="reqbody", full=False),fields_set("requestbody",regex_select(v("__CONTENT__"),regex="reqbody \{[^\}]+\}")))
```
3. 丢弃**\_\_CONTENT\_\_**字段。
```
fields_drop("__CONTENT__")
```

以上我们已经提取出了我们需要的字段，但是由于在正则匹配过程中，产生了多余的字符 action、uin、requestbody、requestid、TaskId。所以需要使用 **str_replace()** 函数将多余的字符去掉，并且使用 **fields_set()** 函数对字段值进行重置。

1. 如果有 **requestbody** 字段，将字段值中多余的 **reqbody** 字符去掉。
```
t_if(has_field("requestbody"),fields_set("requestbody",str_replace(v("requestbody"),old="reqbody",new="")))
```
2. 将字段值v("**requestid**")中多余的 **requestid** 去掉。因为每条日志中都有 **requestid**，所以没有判断这个字段是否存在。
```
fields_set("requestid",str_replace(v("requestid"),old="request",new=""))
```
3. 如果有 **action** 字段，那么字段值中多余的 **action:** 或 **action** 字符去掉。
```
t_if(has_field("action"),fields_set("action",str_replace(v("action"),old="action:|action",new="")))
```
4. 如果有 **uin** 字段，那么字段值中多余的 **uin:** 或者 **uin** 去掉。
```
t_if(has_field("uin"),fields_set("uin",str_replace(v("uin"),old="uin:|uin",new="")))
```
5. 如果有 **TaskId** 字段，那么字段值中多余的 **TaskId** 字符去掉。
```
t_if(has_field("tTaskId"),fields_set("TaskId",str_replace(v("TaskId"),old="TaskId",new="")))
```

#### 加工结果

```
[
{"action":" Describe","requestid":" 7143a51d-caa4-4a6d-bbf3-771b4ac9e135","requestbody":" {\"Key\": \"config\",\"Values\": \"appisrunnning\",\"Action\": \"Describe\",\"RequestId\": \"7143a51d-caa4-4a6d-bbf3-771b4ac9e135\",\"AppId\": 1302953499,\"Uin\": \"100015432829\"}","uin":" 15432829"},
{"action":" DataETL","requestid":" 2ade9fc4-2db2-49d8-b3e0-a6ea78ce8d96","uin":" 15432829"},
{"action":" UploadData","requestid":" 6059b946-25b3-4164-ae93-9178c9e73d75","TaskId":" 51d-caa-a6d-bf3-7ac9e"}
]
```

## 案例6：利用分割符提取日志中的指定内容

#### 场景描述

小王将 **Flink 任务运行的日志**，以单行文本采集到 CLS。日志内容里面包含了**逗号","** ,**冒号"："**，这些分割符将日志分割成了几小段。其中有一段是转义 JSON，它里面是 Flink 任务执行的详情，小王想将任务详情提取出来，然后对其进行结构化。  

#### 场景分析

梳理一下小王的加工需求，加工思路如下：  
1. 将转义 JSON 提取出来。  
2. 从 JSON 中提取结构化数据。


#### 原始日志

``` 
{
    "regex": "2021-12-02 14:33:35.022 [1] INFO  org.apache.Load - Response:status: 200, resp msg: OK, resp content: {    \"TxnId\": 58322,    \"Label\": \"flink_connector_20211202_1de749d8c80015a8\",    \"Status\": \"Success\",    \"Message\": \"OK\",    \"TotalRows\": 1,    \"LoadedRows\": 1,    \"FilteredRows\": 0,  \"CommitAndPublishTimeMs\": 16}"
}
```

#### DSL 加工函数

```
ext_sepstr("regex", "f1, f2, f3", sep=",")
fields_drop("regex")
fields_drop("f1")
fields_drop("f2")
ext_sepstr("f3", "f1,resp_content", sep=":")
fields_drop("f1")
fields_drop("f3")
ext_json("resp_content", prefix="")
fields_drop("resp_content")
```

#### DSL 加工函数详解 

1. 使用逗号将该条日志截成3段，第三段**f3**是 **resp content:{JSON}**。
```
ext_sepstr("regex", "f1, f2, f3", sep=",")
```
2. 将不需要的字段丢弃。
```
fields_drop("regex")
fields_drop("f1")
fields_drop("f2")
```
3. 使用冒号将**f3**字段截成两段。
```
ext_sepstr("f3", "f1,resp_content", sep=":")
```
4. 丢弃无用的字段。
```
fields_drop("f1")
fields_drop("f3")
```
5. 使用 **ext_json** 函数，从 **resp_content** 字段中，提取结构化数据。
```
ext_json("resp_content", prefix="")
```
6. 丢弃 **resp_content** 字段。
```
fields_drop("resp_content")
```

#### 加工结果

```
{"CommitAndPublishTimeMs":"16","FilteredRows":"0","Label":"flink_connector_20211202_1de749d8c80015a8","LoadedRows":"1","Message":"OK","Status":"Success","TotalRows":"1","TxnId":"58322"}
```
