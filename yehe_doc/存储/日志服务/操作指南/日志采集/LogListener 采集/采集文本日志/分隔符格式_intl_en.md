## Overview

In a separator log, the entire log data can be structured according to the specified separator, and each complete log ends with a line break `\n`. When CLS processes separator logs, you need to define a unique key for each separate field.

## Prerequisites

Assume the raw data of a log is as follows:

```plaintext
10.20.20.10 - ::: [Tue Jan 22 14:49:45 CST 2019 +0800] ::: GET /online/sample HTTP/1.1 ::: 127.0.0.1 ::: 200 ::: 647 ::: 35 ::: http://127.0.0.1/
```

If the separator for log parsing is specified as `:::`, the log will be segmented into eight fields, and a unique key will be defined for each of them as shown below:

```plaintext
IP: 10.20.20.10 -
bytes: 35
host: 127.0.0.1
length: 647
referer: http://127.0.0.1/
request: GET /online/sample HTTP/1.1
status: 200
time: [Tue Jan 22 14:49:45 CST 2019 +0800]
```

## Directions

### Logging in to the console

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. In the left sidebar, click **Log Topic** to go to the log topic management page.

### Creating a log topic

1. Click **Create Log Topic**.
2. In the pop-up, enter `test-separator` as **Log Topic Name** and click **OK**.

### Managing the machine group

1. After the log topic is created successfully, click its name to go to the log topic management page.
2. Click the **Collection Configuration** tab and click the format in which you need to collect logs.
3. On the **Machine Group Management** page, select the machine group to which to bind the current log topic and click **Next** to proceed to collection configuration.
For more information, please see [Machine Group Management](https://intl.cloud.tencent.com/document/product/614/17412).



### Configuring collection

On the **Collection Configuration** page, set **Collection Path** according to the log collection path format as shown below:
Log collection path format: `[directory prefix expression]/**/[filename expression]`.

After the log collection path is entered, LogListener will match all common prefix paths that meet the **[directory prefix expression]** rule and listen for all log files in the directories (including subdirectories) that meet the **[filename expression]** rule. The parameters are as detailed below:

| Parameter     | Description       |
| -------- | ------------------------------------------------------------ |
| Directory prefix | Directory structure of the log file prefix. Only wildcards `\*` and `?` are supported.<ul style="margin: 0;"><li>`\*` indicates to match any multiple characters.</li><li>`?` indicates to match any single character.</li></ul> |
| /\*\*/     | Current directory and all its subdirectories.   |
| Filename   | Log filename. Only wildcards `\*` and `?` are supported.<ul style="margin: 0;"><li>`\*` indicates to match any multiple characters.</li><li>`?` indicates to match any single character.</li></ul> |

Common configuration modes are as follows:
- [Common directory prefix]/\*\*/[common filename prefix]\*
- [Common directory prefix]/\*\*/\*[common filename suffix]
- [Common directory prefix]/\*\*/[common filename prefix]\*[common filename suffix]
- [Common directory prefix]/\*\*/\*[common string]\*

Below are examples:

| No. | Directory Prefix Expression | Filename Expression | Description                                                         |
| ---- | -------------- | ------------ | ------------------------------------------------------------ |
| 1.   | /var/log/nginx | access.log   | In this example, the log path is configured as `/var/log/nginx/**/access.log`. LogListener will listen for log files named `access.log` in all subdirectories in the `/var/log/nginx` prefix path. |
| 2.   | /var/log/nginx | \*.log        | In this example, the log path is configured as `/var/log/nginx/**/*.log`. LogListener will listen for log files suffixed with `.log` in all subdirectories in the `/var/log/nginx` prefix path. |
| 3.   | /var/log/nginx | error\*       | In this example, the log path is configured as `/var/log/nginx/**/error*`. LogListener will listen for log files prefixed with `error` in all subdirectories in the `/var/log/nginx` prefix path. |

>!
> - Only LogListener 2.3.9 and above support adding multiple collection paths.
> - The system does not support uploading logs with contents in multiple text formats, which may cause write failures, such as `key:"{"substream":XXX}"`.
> - You are advised to configure the collection path as `log/*.log` and rename the old file after log rotation as `log/*.log.xxxx`.
> - By default, a log file can only be collected by one log topic. If you want to have multiple collection configurations for the same file, please add a soft link to the source file and add it to another collection configuration.
> 

#### Configuring the separator mode

1. Set **Extraction Mode** to **Separator**.
2. Select a separator.
The system segments the sample log according to the selected separator and displays it in the extraction result box. You need to define a unique key for each field. Currently, log collection supports a variety of separators. Common separators include space, tab, comma, semicolon, and vertical bar. If your log data uses other separators such as `:::`, it can also be parsed through custom delimiter.



#### Configuring the collection policy

- Full collection: when LogListener collects a file, it starts reading data from the beginning of the file.
- Incremental collection: when LogListener collects a file, it starts reading data 1 MB ahead of the end of the file (for a file less than 1 MB, incremental collection is equivalent to full collection).


#### Configuring the collection time

>? 
> - The log time is measured in seconds. If the log time is entered in an incorrect format, the collection time is used as the log time.
> - The time attribute of a log is defined in two ways: collection time and original timestamp.
> - Collection time: the time attribute of a log is determined by the time when CLS collects the log.
> - Original timestamp: the time attribute of a log is determined by the timestamp in the raw log.
> 

- **Using the collection time as the time attribute of logs**
Keep **Collection Time** enabled as shown below:

- **Using the original timestamp as the time attribute of logs**
Disable **Collection Time** and enter the time key of the original timestamp and the corresponding time parsing format in **Time Key** and **Time Parsing Format** respectively. For more information on the time parsing format, please see [Configuring Time Format](https://intl.cloud.tencent.com/document/product/614/32942).

Below are examples of how to enter a time parsing format:
Example 1: the parsing format of the original timestamp `10/Dec/2017:08:00:00` is `%d/%b/%Y:%H:%M:%S`.
Example 2: the parsing format of the original timestamp ``2017-12-10 08:00:00`` is `%Y-%m-%d %H:%M:%S`.
Example 3: the parsing format of the original timestamp `12/10/2017, 08:00:00` is `%m/%d/%Y, %H:%M:%S`.

>! Second can be used as the unit of log time. If the time is entered in a wrong format, the collection time is used as the log time.
>

#### Configuring filter rules

Filters are designed to help you extract valuable log data by adding log collection filter rules based on your business needs. If the filter rule is a Perl regular expression, the created filter rule will be used for matching; in other words, only logs that match the regular expression will be collected and reported.

For separator-formatted logs, you need to configure a filter rule according to the defined custom key-value pair. For example, if you want to collect all log data with a `status` field whose value is 400 or 500 after the sample log is parsed in separator mode, you need to configure `key` as `status` and the filter rule as `400|500`.

>! The relationship logic between multiple filter rules is "AND". If multiple filter rules are configured for the same key name, previous rules will be overwritten.
>

## Related Operations

### Log search
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. In the left sidebar, click **Search and Analysis** to enter the search and analysis page.
3. Select the region, logset, and log topic as needed, and click **Search and Analysis** to search for logs according to the set query rules.
