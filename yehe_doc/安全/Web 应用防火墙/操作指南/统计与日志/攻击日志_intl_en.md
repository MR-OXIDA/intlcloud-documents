This guide describes how to search and analyze attack logs.

## Background
WAF supports logging to get attack information including the attack time, attacker IP and attack type. You can query or export the data for the last 30 days, search data with full-text search, fuzzy search, and search by filter, and download data and even million of logs based on your search filters.

## Operation Guide

3. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/attack). On the left sidebar, choose **Log Services** > **Attack Logs** to go to the attack log search tab.
2. On the log search tab, select a domain name, attack type, action and attack time to view the attack log.
![](https://main.qcloudimg.com/raw/b0f782b0ce530ec81cc0106b74366a40.png)

**Field description:**
 - **Domain Name**: supports multiple domain names. All domain names will be displayed by default.
 - **Attack Type**: supports multiple attack types. All attack types will be displayed by default. Attack types involve observation and blocking logs generated by various security modules.
 - **Action Type**: supports `Observe` or `Block`. Default: `All`.
 - **Risk Grade**: supports `Major` (high-risk level), `Medium` (medium-risk level) or `Minor` (low-risk level).
 - **Time Period**: supports selecting a time period you want. By default, a time period of one hour is selected.
 - **Auto Refresh**: supports automatic refresh, which is disabled by default. If it is enabled, you can select a time period for auto refresh and obtain the latest attack log data.
 - **Advanced Search (recommended)**:
   - By default, this feature is enabled and supports Lucene syntax for full-text search (recommended), key value search and fuzzy search.

>?It is recommended to use full-text search for searching. You only need to enter key log fields, such as IP, URL, and one of fields in a request.

    - If you disable the switch, you can use the search box provided, by simply typing in the attacker IP, RUI, UUID and request method. For more search syntaxes, see [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/30439).


3. Specify the search filters prior to clicking **Search Analysis** to view search results.
4. On the left of the raw data page, click a specific statistical field to quickly check each field value as a percentage of the attack log based on your search filters.
- **Custom Field List**: At the top right of the log list, click <img src="https://main.qcloudimg.com/raw/9ebb9fa1652d9154137fa1d934329043.png" style="margin:0;"> to select fields to be displayed, and then click **OK**. To know more about the log fields, refer to [Log field description](#Log).
- **Download**:
	1. At the top right of the log list, click <img src="https://main.qcloudimg.com/raw/ac6451a8dab74a5cf57770ff8af30954.png" style="margin:0;"> to create a download task.
>?
>- You cannot create more than one download task simultaneously.
>- One download task can contain up to 1 million logs. If you need to download more, it is recommended to create a task to start after another task completes, or [contact us](https://intl.cloud.tencent.com/contact- us) for support.
>- If you select a wildcard domain name (for example, *.abc.com), log entries of all associated subdomain names such as those suffixed with .abc.com will also be downloaded.

	2. At the top of the [Attack Logs](https://console.cloud.tencent.com/guanjia/attack) page, click **Download** to view the downloading status.
	3. For logs in **Completed** status, download them locally by clicking **Download**. For field details, see [Log field description](#log2).
5. On the right of the raw data page, click the unfold button to display log details. To view the information in JSON format, click **JSON**.
6. On the log details page, select a specific parameter value as a search filter. Multiple field combinations are also supported for searching.

## Appendix

[](id:Log)
### Log field description

**Basic Information**

|Field|Description|
|----|---|
|host|Domain name accessed by the client|
|attack_type|All attack types|
|attack_category |Unavailable currently|
|count|Number of attacks of the same type from the same attacker IP every 10 seconds|
|attack_ip|Attacker IP, the source IP used by the client to launch an attack|
|rule_id|ID of the hit protection rule. ID of the rule taken by the AI engine is 0.|
|rule_name|Name of the hit protection rule. Names of the rules taken by the rule engine and AI engine are left empty.|
|method|Request method used by the client to launch an attack|
|risk_level|Risk level of the attack|
|attack_time|Time that the attack is launched|
|attack_place|Attack location in the HTTP request|
|action|Action triggered by the attack|
|uri|Content of the request URI
|attack_content|Content of the attack triggered by the client|
|http_log|Other information of the request, including the request protocol and protocol version.|
|user_agent|Information about the browser type and operating system used by the attacker IP|
|headers|Header information, including custom headers.|
|UUID|Unique identifier of the log|

**Attacker IP Attribute**

|Field|Description|
|----|---|
|ipinfo_province|Province of the attacker IP|
|ipinfo_state |Country abbreviation of the attacker IP|
|pinfo_nation|Country name of the attacker IP|
|ipinfo_city |City of the attacker IP|
|ipinfo_isp|ISP of the attacker IP|
|ipinfo_dimensionality |Latitude of the attacker IP|
|ipinfo_longitude |Longitude of the attacker IP|


### Log field description

|Field|Description|
|----|---|
|uuid|Unique identifier of the log|
|attack_time|Time that the attack is launched by the client|
|rule_id|ID of the protection rule triggered by the attack|
|count|Number of attacks of the same type from the same attacker IP every 10 seconds|
|status|Status of the action. `0`: observe; `1`: block.|
|domain|Domain name attacked by the client|
|attack_ip|IP address used by the client to launch an attack|
|attack_type|Attack type|
|args_name|Attacked object in a client request, such as request parameters, URI, and IP|
|attack_content|Content of the attack triggered by the client|
|uri|URI of the attack triggered by the client|
|method|Method of the attack request sent by the client|
|user_agent|User-Agent information of the client|
