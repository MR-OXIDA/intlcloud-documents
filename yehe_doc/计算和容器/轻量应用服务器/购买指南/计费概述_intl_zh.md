轻量应用服务器计费分为 **[基础套餐](#basis)**、**[套餐外超额流量](#additional)** 及 **[自定义镜像](#customizeOS)** 三部分。


## [基础套餐概述](id:basis)
轻量应用服务器提供服务器套餐售卖模式，套餐包含了 CPU、内存、SSD 云硬盘、网络流量包等云服务器资源，并以优惠价格售卖。如若套餐包含的云服务器资源无法满足用户的需求，用户还可以通过购买超出流量等形式申请额外的云服务资源。



### 计费模式
基础套餐目前仅支持包年包月模式售卖。包年包月是一种预付费模式，需提前一次性支付一个月或多个月甚至多年的费用。其中，包月时长计算周期为自然月。例如：
2020年2月10日0点购买轻量应用服务器，时长为1个月，则包月时长计算周期为 2月10日 00:00:00 - 3月10日 23:59:59。
2020年5月1日0点购买轻量应用服务器，时长为1个月，则包月时长计算周期为 5月1日 00:00:00 - 5月31日 23:59:59。

### 欠费停服
实例到期后将处于“待回收”状态，7天内用户可以通过续费恢复实例可用状态。
若在实例处于“待回收”期间内不进行续费操作，则将释放实例，释放后实例中的数据将被清除且不可恢复，详情请参见 [回收机制](https://intl.cloud.tencent.com/document/product/1103/41405)。请关注实例状态，及时续费或转移数据。

### 流量包
轻量应用服务器的套餐采用流量包模式，流量包仅统计实例的出流量。当实例当月使用的流量属于下列情况时：
 - **未超出当月流量包限制**：以购买时间起，按月进行流量包重置。
 - **超出当月流量包限制**：超出部分的流量将按照使用量进行计费。




## [基础套餐定价](id:basisPrice)
>? 
>- **Linux 实例套餐**：实例使用的镜像为 Linux 类型的系统镜像或者基于 Linux 系统的应用镜像。
>- **Windows 实例套餐**：实例使用的镜像为 Windows Server 系统镜像或者 ASP.NET 应用镜像。
>- 已下线套餐已不再售卖，建议使用已下线套餐的用户进行实例套餐升级。详情请参见 [升级实例套餐](https://intl.cloud.tencent.com/document/product/1103/41407)。
>

### 中国内地地域
中国内地地域根据套餐配置的不同，分为**通用型**及**存储型**两种类型，请根据您的业务情况进行选择。创建实例时，一次性购买半年及以上将享受优惠价格。

<table>
	<tr><th>套餐类型</th><th>CPU（核）</th><th>内存（GB）</th><th>系统盘-SSD（GB） </th><th>带宽（Mbps）</th><th>每月流量包（GB）</th><th>价格（元/月）</th></tr>
	<tr><td rowspan=7>通用型</td></tr>
	<tr><td>1</td><td>1</td><td>40</td><td>4</td><td>300</td><td><b>40</b></td></tr>
	<tr><td>1</td><td>2</td><td>50</td><td>5</td><td>500</td><td><b>50</b></td></tr>
	<tr><td>1</td><td>2</td><td>60</td><td>6</td><td>1000</td><td><b>90</b></td></tr>
	<tr><td>2</td><td>4</td><td>80</td><td>8</td><td>1200</td><td><b>140</b></td></tr>
	<tr><td>4</td><td>8</td><td>100</td><td>10</td><td>1500</td><td><b>255</b></td></tr>
	<tr><td>4</td><td>16</td><td>120</td><td>12</td><td>2000</td><td><b>350</b></td></tr>
	<tr><td rowspan=4>存储型</td><td>1</td><td>2</td><td>200</td><td>3</td><td>200</td><td><b>70</b></td></tr>
	<tr><td>2</td><td>4</td><td>350</td><td>4</td><td>300</td><td><b>105</b></td></tr>
	<tr><td>2</td><td>8</td><td>500</td><td>5</td><td>500</td><td><b>150</b></td></tr>
	<tr><td>4</td><td>8</td><td>1000</td><td>8</td><td>1000</td><td><b>300</b></td></tr>
</table>

下表为已下线套餐（建议升级为新套餐）：
<table>
	<tr><th>套餐类型</th><th>CPU（核）</th><th>内存（GB）</th><th>系统盘-SSD（GB） </th><th>带宽（Mbps）</th><th>每月流量包（GB）</th><th>价格（元/月）</th></tr>
	<tr><td rowspan=6>通用型</td><td>1</td><td>1</td><td>20</td><td>3</td><td>200</td><td><b>40</b></td></tr>
	<tr><td>1</td><td>1</td><td>40</td><td>3</td><td>300</td><td><b>50</b></td></tr>
	<tr><td>1</td><td>1</td><td>40</td><td>3</td><td>500</td><td><b>90</b></td></tr>
	<tr><td>1</td><td>2</td><td>40</td><td>5</td><td>1000</td><td><b>140</b></td></tr>
	<tr><td>2</td><td>4</td><td>60</td><td>8</td><td>1500</td><td><b>255</b></td></tr>
	<tr><td>2</td><td>8</td><td>80</td><td>10</td><td>2000</td><td><b>350</b></td></tr>
</table>




### 中国内地地域时长折扣

| 1 - 5个月 | 6 - 11个月 | 12个月及以上 |
|---------|---------|---------|
| 无 | 88折 | 85折 |

>?新购及续费实例均可享受时长折扣。

### 中国港澳台地区和其他国家地域

<dx-tabs>
::: Linux\s实例套餐
<table>
<thead>
<tr>
<th>CPU（核）</th><th>内存（GB）</th><th>系统盘-SSD（GB）</th><th>峰值带宽（Mbps）</th>
<th>每月流量包（GB）</th><th>价格（元/月）</th>
</tr>
</thead>
<tbody>
<tr>
<tr>
<tr>
<td>1</td><td>1</td><td>25</td><td>30</td><td>1024</td><td><strong>24</strong></td>
</tr>
<tr>
<td>1</td><td>2</td><td>50</td><td>30</td><td>2048</td><td><strong>34</strong></td>
</tr>
<td>2</td><td>4</td><td>80</td><td>30</td><td>3072</td><td><strong>67</strong></td>
</tr>
<tr>
<td>2</td><td>8</td><td>100</td><td>30</td><td>4096</td><td><strong>133</strong><sup>1</sup></td>
</tr>
<tr>
<td>4</td><td>8</td><td>200</td><td>30</td><td>5120</td><td><strong>266</strong><sup>1</sup></td>
</tr>
<tr>
<td>4</td><td>16</td><td>400</td><td>30</td><td>6144</td><td><strong>532</strong><sup>1</sup></td>
</tr>
</tbody></table>

<dx-alert infotype="explain" title="">
<sup>1</sup> 该套餐可享受时长折扣。
</dx-alert>

下表为已下线套餐（建议升级为新套餐）：
<table>
<thead>
<tr>
<th>CPU（核）</th><th>内存（GB）</th><th>系统盘-SSD（GB）</th><th>峰值带宽（Mbps）</th>
<th>每月流量包（GB）</th><th>价格（元/月）</th>
</tr>
</thead>
<tbody>
<tr>
<td>2</td><td>2</td><td>80</td><td>30</td><td>3072</td><td><strong>67</strong></td>
</tr>
<tr>
<td>2</td><td>4</td><td>100</td><td>30</td><td>4096</td><td><strong>133</strong></td>
</tr>
<tr>
<td>2</td><td>8</td><td>200</td><td>30</td><td>5120</td><td><strong>266</strong></td>
</tr>
</tbody></table>

:::
::: Windows\s实例套餐
<table>
<thead>
<tr>
<th>CPU（核）</th><th>内存（GB）</th><th>系统盘-SSD（GB）</th><th>峰值带宽（Mbps）</th>
<th>每月流量包（GB）</th><th>价格（元/月）</th>
</tr>
</thead>
<tbody><tr>
<td>1</td><td>1</td><td>40</td><td>30</td><td>1024</td><td><strong>48</strong></td>
</tr>
<tr>
<td>1</td><td>2</td><td>50</td><td>30</td><td>2048</td><td><strong>68</strong></td>
</tr>
<tr>
<td>2</td><td>4</td><td>80</td><td>30</td><td>3072</td><td><strong>121</strong></td>
</tr>
<tr>
<td>2</td><td>8</td><td>100</td><td>30</td><td>4096</td><td><strong>239</strong><sup>1</sup></td>
</tr>
<tr>
<td>4</td><td>8</td><td>200</td><td>30</td><td>5120</td><td><strong>465</strong><sup>1</sup></td>
</tr>
<tr>
<td>4</td><td>16</td><td>400</td><td>30</td><td>6144</td><td><strong>788</strong><sup>1</sup></td>
</tr>
</tbody></table>

<dx-alert infotype="explain" title="">
<sup>1</sup> 该套餐可享受时长折扣。
</dx-alert>

下表为已下线套餐（建议升级为新套餐）：
<table>
<thead>
<tr>
<th>CPU（核）</th><th>内存（GB）</th><th>系统盘-SSD（GB）</th><th>峰值带宽（Mbps）</th>
<th>每月流量包（GB）</th><th>价格（元/月）</th>
</tr>
</thead>
<tbody>
<tr>
<tr>
<td>2</td><td>2</td><td>80</td><td>30</td><td>3072</td><td><strong>132</strong></td>
</tr>
<tr>
<td>2</td><td>4</td><td>100</td><td>30</td><td>4096</td><td><strong>265</strong></td>
</tr>
<tr>
<td>2</td><td>8</td><td>200</td><td>30</td><td>5120</td><td><strong>465</strong></td>
</tr>
</tbody></table>

:::
</dx-tabs>



### 中国港澳台地区和其他国家地域时长折扣
| 1 - 5个月 | 6 - 11个月 | 12个月及以上 |
|---------|---------|---------|
| 无 | 88折 | 85折 |

>?新购及续费实例均可享受时长折扣。


## [套餐外超额流量概述](id:additional)
当实际使用流量超出基础套餐的月流量包限额，轻量应用服务器将按流量计费（仅统计服务器的出流量），即按公网传输的数据总量（单位为GB）计费。

### 计费模式
超出月流量包限额的部分将按照套餐外超额流量定价每小时结算费用。

### 欠费停服
当用户账号处于欠费状态，所有超出月流量包限额的实例将进入停服状态，没有超出月流量包限额的实例不受影响。如需恢复实例至可用状态，请将账户充值到余额大于0，或等待流量包按月重置后再进行使用。


## [套餐外超额流量定价](id:OverRatedPrice)
| 地域 | 价格（元/GB） |
|---------|---------|
| 中国内地、新加坡、莫斯科、东京 | 0.8 |
| 中国香港 | 	1.0 |
| 硅谷	 | 	0.5 |

## [自定义镜像计费概述](id:customizeOS)
### 计费模式
按地域内**超出免费配额的自定义镜像个数**进行统计，按小时进行结算（删除自定义镜像时，使用时长中不足一小时的部分将按一小时结算）。
>! 每个地域提供5个免费自定义镜像配额。


### 定价信息
超出免费配额的每个自定义镜像计费单价为0.01元/小时。

### 欠费说明
当您的账号处于欠费状态时：
- 自定义镜像功能将被停止，无法制作新的自定义镜像。
- 账号下已有的自定义镜像（包含免费配额内的镜像）都将进入“待回收”状态。若自定义镜像进入“待回收”状态后7天内（包括第7天），账号未进行充值，则自定义镜像将会自动释放。

### 相关操作
您可前往轻量应用服务器控制台，创建自定义镜像。