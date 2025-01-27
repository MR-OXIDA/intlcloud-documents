## 操作场景
本文介绍如何在本地开启日志追踪，以获取更详细的日志，便于自查及协助工单处理。


## 操作步骤
1. 在 CLI 中执行 `terraform apply` 前，可以使用以下命令开启本地日志跟踪：
```bash
export TF_LOG=DEBUG
export TF_LOG_PATH=./terraform.log
```
2. 开启后，再次执行以下命令。
```
terraform apply/destroy
```
执行完毕后，可查看 Terraform 本地文件夹会生成一个 `terraform.log` 的文件。文件记录了 tencentcloud provider 定义的日志输出。


## 示例
以下为执行出错示例，及分析定位问题的过程。


本例中创建了一个 K8S cluster 并挂载一台已经存在的 CVM 作节点。
```text
➜ terraform apply

2021/12/09 17:53:02 [WARN] Log levels other than TRACE are currently unreliable, and are supported only for backward compatibility.
  Use TF_LOG=TRACE to see Terraform's internal logs.
  ----
data.tencentcloud_instance_types.default: Refreshing state...
data.tencentcloud_cbs_storages.storages: Refreshing state...
data.tencentcloud_vpc_subnets.vpc2: Refreshing state...
data.tencentcloud_images.default: Refreshing state...
data.tencentcloud_vpc_subnets.vpc: Refreshing state...
An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # tencentcloud_kubernetes_cluster.managed_cluster will be created
  + resource "tencentcloud_kubernetes_cluster" "managed_cluster" {
      + certification_authority      = (known after apply)
      + claim_expired_seconds        = 300
      + cluster_as_enabled           = false
      + cluster_cidr                 = "10.1.0.0/16"
      + cluster_deploy_type          = "MANAGED_CLUSTER"
      + cluster_desc                 = "test cluster desc"
      + cluster_external_endpoint    = (known after apply)
      + cluster_internet             = false
      + cluster_intranet             = false
      + cluster_ipvs                 = true
      + cluster_max_pod_num          = 32
      + cluster_max_service_num      = 32
      + cluster_name                 = "keep"
      + cluster_node_num             = (known after apply)
      + cluster_os                   = "ubuntu16.04.1 LTSx86_64"
      + cluster_os_type              = "GENERAL"
      + cluster_version              = "1.10.5"
      + container_runtime            = "docker"
      + deletion_protection          = false
      + domain                       = (known after apply)
      + id                           = (known after apply)
      + ignore_cluster_cidr_conflict = false
      + is_non_static_ip_mode        = false
      + kube_config                  = (known after apply)
      + network_type                 = "GR"
      + node_name_type               = "lan-ip"
      + password                     = (known after apply)
      + pgw_endpoint                 = (known after apply)
      + security_policy              = (known after apply)
      + user_name                    = (known after apply)
      + vpc_id                       = "vpc-h70b6b49"
      + worker_instances_list        = (known after apply)

      + worker_config {
          + availability_zone                       = "ap-guangzhou-3"
          + count                                   = 1
          + enhanced_monitor_service                = false
          + enhanced_security_service               = false
          + instance_charge_type                    = "POSTPAID_BY_HOUR"
          + instance_charge_type_prepaid_period     = 1
          + instance_charge_type_prepaid_renew_flag = "NOTIFY_AND_MANUAL_RENEW"
          + instance_name                           = "sub machine of tke"
          + instance_type                           = "S1.SMALL1"
          + internet_charge_type                    = "TRAFFIC_POSTPAID_BY_HOUR"
          + internet_max_bandwidth_out              = 100
          + password                                = (sensitive value)
          + public_ip_assigned                      = true
          + subnet_id                               = "subnet-1uwh63so"
          + system_disk_size                        = 60
          + system_disk_type                        = "CLOUD_SSD"
          + user_data                               = "dGVzdA=="

          + data_disk {
              + disk_size = 50
              + disk_type = "CLOUD_PREMIUM"
            }
        }
    }

  # tencentcloud_kubernetes_cluster_attachment.test_attach will be created
  + resource "tencentcloud_kubernetes_cluster_attachment" "test_attach" {
      + cluster_id      = (known after apply)
      + hostname        = "user"
      + id              = (known after apply)
      + instance_id     = "ins-lmnl6t1g"
      + labels          = {
          + "test1" = "test1"
          + "test2" = "test2"
        }
      + password        = (sensitive value)
      + security_groups = (known after apply)
      + state           = (known after apply)

      + worker_config {
          + docker_graph_path = "/var/lib/docker"
          + is_schedule       = true

          + data_disk {
              + auto_format_and_mount = false
              + disk_size             = 50
              + disk_type             = "CLOUD_PREMIUM"
            }
        }
    }

Plan: 2 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

tencentcloud_kubernetes_cluster.managed_cluster: Creating...

Error: [TencentCloudSDKError] Code=InternalError.CidrConflictWithOtherCluster, Message=DashboardError,Code : -10013 , Msg : CIDR_CONFLICT_WITH_OTHER_CLUSTER[cidr 10.1.0.0/16 is conflict with cluster id: cls-1zc0kpyo], err : CheckCIDRWithVPCClusters failed,CIDR(10.1.0.0/16) conflict with clusterCIDR,ClusterID:cls-1zc0kpyo,clusterCIDR:10.1.0.0/16,err:CIDR1:10.1.0.0/16,firstIP:10.1.0.0,conflict with CIDR2:10.1.0.0/16, RequestId=d7dfb178-f081-480a-9bc3-89efc5fb1db5

  on main.tf line 424, in resource "tencentcloud_kubernetes_cluster" "managed_cluster":
 424: resource "tencentcloud_kubernetes_cluster" "managed_cluster" {
```
CLI 提示错误如下:
```bash
[TencentCloudSDKError] Code=InternalError.CidrConflictWithOtherCluster, Message=DashboardError,Code : -10013 , Msg : CIDR_CONFLICT_WITH_OTHER_CLUSTER[cidr 10.1.0.0/16 is conflict with cluster id: cls-1zc0kpyo], err : CheckCIDRWithVPCClusters failed,CIDR(10.1.0.0/16) conflict with clusterCIDR,ClusterID:cls-1zc0kpyo,clusterCIDR:10.1.0.0/16,err:CIDR1:10.1.0.0/16,firstIP:10.1.0.0,conflict with CIDR2:10.1.0.0/16, RequestId=d7dfb178-f081-480a-9bc3-89efc5fb1db5
```

问题分析及定位：
1. 找到 `requestId: d7dfb178-f081-480a-9bc3-89efc5fb1db5`。
2. 打开 `terraform.log`，搜索该 requestId，找到上下文如下所示：
```bash
    2021-12-09T17:53:20.222+0800 [DEBUG] plugin.terraform-provider-tencentcloud.exe: 2021/02/25 17:53:20 [DEBUG] setting computed for "worker_instances_list" from ComputedKeys
    
    _CONFLICT_WITH_OTHER_CLUSTER[cidr 10.1.0.0/16 is conflict with cluster id: cls-1zc0kpyo], err : CheckCIDRWithVPCClusters failed,CIDR(10.1.0.0/16) conflict with clusterCIDR,ClusterID:cls-1zc0kpyo,clusterCIDR:10.1.0.0/16,err:CIDR1:10.1.0.0/16,firstIP:10.1.0.0,conflict with CIDR2:10.1.0.0/16"},"RequestId":"d7dfb178-f081-480a-9bc3-89efc5fb1db5"}},cost 370.8109ms
    
    6 is conflict with cluster id: cls-1zc0kpyo], err : CheckCIDRWithVPCClusters failed,CIDR(10.1.0.0/16) conflict with clusterCIDR,ClusterID:cls-1zc0kpyo,clusterCIDR:10.1.0.0/16,err:CIDR1:10.1.0.0/16,firstIP:10.1.0.0,conflict with CIDR2:10.1.0.0/16, RequestId=40d3ee5d-f723-4ef9-8f01-32d725464d51
    
    2021-12-09T17:53:20.593+0800 [DEBUG] plugin.terraform-provider-tencentcloud.exe: 2021/12/09 17:53:20 common.go:79: [DEBUG] [ELAPSED] resource.tencentcloud_kubernetes_cluster.create elapsed 371 ms
```
3. 分析日志，可定位是创建 K8s cluster 过程中出现问题。示例中是因为 cidr 与已存在的其他 K8s cluster 有冲突造成的。
<dx-alert infotype="explain" title="">
若 CLI 提示错误信息不够清晰，或无 requestID 的报错造成定位有困难，可将 **tf 项目文件，CLI 提示错误以及其产生的日志 terraform.log 文件**通过 [提交工单](https://console.cloud.tencent.com/workorder/category) 请求协助。
</dx-alert>


