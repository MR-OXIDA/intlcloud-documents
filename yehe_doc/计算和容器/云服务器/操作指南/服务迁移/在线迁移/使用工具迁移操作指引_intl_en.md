This document describes how to use the go2tencentcloud migration tool to perform online server migration.


## Migration Process
The migration process of the tool is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/89072a07336ffe9574dfc8d0bc96de65.png)

## Preparations

- You already have a Tencent Cloud account and a destination CVM.
- Stop applications on the source server to prevent existing applications from being affected by the migration.
[Click here](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) to download the compressed migration tool package.
- Create and copy `SecretId` and `SecretKey` on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page.
- Check that both source servers and destination CVM meet the migration requirements. For example, the cloud disks of the destination CVM should have sufficient capacity to save data migrated from source servers.
- We recommend you back up your data in the following ways before migrating:
 - Source server: you can use the source server's snapshot feature or other methods to back up data.
 - Destination CVM: you can [create a snapshot](https://intl.cloud.tencent.com/document/product/362/5755) or use other methods to back up the data of the destination CVM.

## Migration Directions


### Modifying configuration file[](id:modifyConfiguration)

1. Download or upload `go2tencentcloud.zip` to the source server and run the following command to enter the corresponding directory.
    1. Run the following commands in sequence to decompress `go2tencentcloud.zip` and enter the directory.
```sh
unzip go2tencentcloud.zip
```
```sh
cd go2tencentcloud
```
    2. Run the following commands in sequence to decompress `go2tencentcloud_tool.zip` and enter the directory.
```sh
unzip go2tencentcloud_tool.zip
```
```sh
cd go2tencentcloud_tool
```
<dx-alert infotype="explain" title="">
The files in the `go2tencentcloud` directory will not be migrated. Do not place the files to be migrated in this directory.
</dx-alert>
2. In the `user.json` file, configure the destination CVM for the migration.
Follow the [descriptions of parameters in the `user.json` file](https://intl.cloud.tencent.com/document/product/213/44340) to configure the required parameters and their values. Replace the corresponding parameter values with your actual parameter values. Below are examples:
 - Example 1: to migrate a Linux source server to a CVM located in Guangzhou, configure the `user.json` file as follows:
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id"
} 
```
 - Example 2: a Linux source server has one data disk, the mount point is `/mnt/disk1`, and the size of the data disk is `10 GB`. To migrate this server to a CVM (with at least one data disk mounted) located in the Guangzhou region, configure the `user.json` file as follows:
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id",
	"DataDisks": [
		{
			"Index": 1,
			"Size": 10,
			"MountPoint": "/mnt/disk1"
		}
	]
}
```
 - Example 3: a Linux source server has two data disks. The mount point for disk 1 is `/mnt/disk1`, and the size is `10 GB`. The mount point for disk 2 is `/mnt/disk2`, and the size is `20 GB`. To migrate this server to a CVM (with at least two data disks mounted) located in Guangzhou, with disk 1 and disk 2 of the source server to be migrated to the first and second data disks of the destination CVM respectively, configure the `user.json` file as follows:
```json
{  
	"SecretId": "your secretId",
	"SecretKey": "your secretKey",  
	"Region": "ap-guangzhou",  
	"InstanceId": "your instance id",
	"DataDisks": [
		{
			"Index": 1,
			"Size": 10,
			"MountPoint": "/mnt/disk1"
		},
		{
			"Index": 2,
			"Size": 20,
			"MountPoint": "/mnt/disk2"
		}
	]
}  
```
2. (Optional) Configure the migration mode and other items in the `client.json` file.
Follow the [descriptions of parameters in the `client.json` file](https://intl.cloud.tencent.com/document/product/213/44340) for configuration. If either the source server or the destination CVM cannot directly access the public network, you can choose to establish a connection through [Peering Connection](https://intl.cloud.tencent.com/zh/document/product/553), [VPN Connections](https://intl.cloud.tencent.com/zh/document/product/1037), [Cloud Connect Network](https://intl.cloud.tencent.com/zh/document/product/1003), or [Direct Connect](https://intl.cloud.tencent.com/zh/document/product/216), and then perform migration in the private network mode. For more information, see [Private Network Migration](https://intl.cloud.tencent.com/document/product/213/44341).
3. (Optional) Exclude files or directories that do not need to be migrated on the source server.
If there are files or directories on the Linux source server that do not need to be migrated, you can add them to the [rsync\_excludes\_linux.txt](https://intl.cloud.tencent.com/document/product/213/44340) file.

### Checking before migration

Before migration, you need to check the source server and destination CVM separately as detailed below:

<table>
  <tr>
	<th style="width: 15%;">Destination CVM</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		Storage space: the cloud disks of the destination CVM (including system and data disks) should have sufficient capacity to save data migrated from the source server.</li>
		<li>Security group: port 443 and port 80 cannot be restricted in the security group.</li>
		<li>
		Bandwidth settings: we recommend you maximize bandwidths at the two ends to speed up the migration. During the process, the traffic consumed is approximately the amount of data migrated. Adjust the billing mode before the migration if necessary.</li>
		<li>
		OS consistency: if the operating systems of the source server and destination CVM are different, the created image may be inconsistent with the actual operating system. We recommend you use the same operating system for the source server and destination CVM.
		For example, to migrate a CentOS 7 source server, select a CentOS 7 CVM as the destination.</li>
	  </ol>
	</td>
  </tr>
  <tr>
	<th>Linux source server</th>
	<td>
	  <ol style="margin: 0;">
		<li>Check and install Virtio. For more information, see: 
		<a href="https://intl.cloud.tencent.com/document/product/213/9929">Checking Virtio Drivers in Linux</a>.</li>
		<li>Run 
		the <code>which rsync</code> command to check whether Rsync is installed, and if not, install it as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/32395#installRsync">How do I install Rsync?</a>.</li>
		<li>Check whether SELinux is enabled, and if yes, disable it as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/32395#closeSELinux">How do I disable SELinux?</a>.</li>
		<li>After a migration request is made to the TencentCloud API, the API will use the current UNIX time to check the generated
		token. You need to make sure that the current system time is correct.</li>
	  </ol>
	</td>
  </tr>
</table>
<dx-alert infotype="explain" title="">
- You can use tool commands such as `sudo ./go2tencentcloud_x64 --check` to automatically check the source server.
- By default, the go2tencentcloud migration tool automatically starts checking upon launch. To skip checks and perform forced migration, configure `Client.Extra.IgnoreCheck` to `true` in the `client.json` file.
</dx-alert>



### Initiating migration

Run the following command to run the tool.
This document takes a 64-bit Linux source server as an example. Go to the `go2tencentcloud_tool` directory and run the following command as the root user to run the tool.
```sh
sudo ./go2tencentcloud_x64
```

### Waiting for migration to end

If you use go2tencentcloud provided by Tencent Cloud for migration, the migration process supports checkpoint restart and includes the following three stages. You can intuitively view the migration progress when the tool is running.

- **Stage 1**: the destination CVM enters the migration mode, and is ready for migration
- **Stage 2**: the destination CVM is in the migration mode, and receives data migrated
- **Stage 3**: the destination CVM exits the migration mode, and the migration completes

Each stage will generate some subtasks to perform related operations, and some time-consuming subtasks may have maximum timeout periods by default. The time required for data transfer depends on the size of the data on the source server, network bandwidth, etc. Please wait for the migration process to complete.

<dx-alert infotype="notice" title="">
The destination CVM enters migration mode after the migration starts. Do not reinstall the system, shut down, terminate, or reset passwords of the destination CVM until the migration is completed and the destination CVM exits the migration mode. 
</dx-alert>

If the migration in public network migration mode succeeds, the console output is as follows:
![](https://main.qcloudimg.com/raw/b056d6b1d5ac457ff43e48883848af01.png)

### Checking after migration

- If the migration fails, check the error information in log files (under the migration tool directory by default), operation guides, or [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) for troubleshooting methods.
- If the migration succeeds, check whether the destination CVM can be started normally, whether data on the destination CVM is consistent with that on the source server, whether the network is normal, and whether other system services run normally.

If you have any questions or the migration has an exception, see [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) or [contact us](https://intl.cloud.tencent.com/document/product/213/34837).
