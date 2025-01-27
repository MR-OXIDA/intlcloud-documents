## Introduction to LVM
Logical Volume Manager (LVM) creates a logical layer over your disks or partitions to divide them into physical extent (PE) units with the same size. This categorizes disks or partitions into a volume group (VG), on which you can create a logical volume (LV), and then create file systems on the LV.
Different from direct disk partitioning, LVM allows elastic scaling of file system.
- The file system is not limited by the size of a physical disk. Instead, it can be distributed among multiple disks:
For example, you can purchase three 4-TB elastic cloud disks, and use LVM to create a massive file system nearly 12 TB.
- You can resize the LVs dynamically instead of repartitioning your disks.
When the LVM VG capacity cannot meet your needs, you can purchase a elastic cloud disk, attach it to your CVM instance, and add it to the LVM VG to expand capacity.

## Building LVM
>?The following example uses three elastic cloud disks to create a dynamically resizable file system through LVM.
![](https://main.qcloudimg.com/raw/81086e80477ff7e374e7c3f0fe9d2788.png)

### Step 1: create a physical volume (PV)
1. [Log in to the Linux CVM instance](https://intl.cloud.tencent.com/document/product/213/5436) as the root user.
2. Run the following command to create a PV.
```plaintext
pvcreate <disk path 1> ... <disk path N>
``` Taking `/dev/vdc`, `/dev/vdd` and `/dev/vde` disks as an example, run the following command.
```plaintext
pvcreate /dev/vdc /dev/vdd /dev/vde
``` The result of a successful creation is shown below:
![](https://main.qcloudimg.com/raw/5b92a6c7878e22906599af48bfa09d95.png)
3. Run the following command to view physical volumes of the system.
```plaintext
lvmdiskscan | grep LVM
``` ![](https://main.qcloudimg.com/raw/1de75af4a49c2deea689a2576eb075d9.png)

### Step 2: create a volume group (VG)
1. Run the following command to create a VG.
```plaintext
vgcreate [-s <specified PE size>] <VG name> <PV path>.
``` Take creating a VG named `lvm_demo0` as an example, run the following command:
```plaintext
vgcreate lvm_demo0 /dev/vdc /dev/vdd
``` The result of a successful creation is shown below:
![](https://main.qcloudimg.com/raw/3b8dba3329f62e85d2075fad10898632.png)
 When **Volume group" <VG name> "successfully created** is displayed, the VG has been created.
 - Then you can run the following commands to add a new PV to the VG.
```plaintext
vgextend [VG name] [Path of the new PV]
``` The result of a successful addition is shown below:
![](https://main.qcloudimg.com/raw/105e5a77472f173ffd4a58624f20a863.png)
 - After the VG is created, you can run `vgs`, `vgdisplay` or other commands to query information about VGs of the system, as shown below:
![](https://main.qcloudimg.com/raw/309c991d32cf4b801ddbe8d898f1bfbb.png)

### Step 3: create a logical volume (LV)
1. Run the following command to create a LV.
```plaintext
lvcreate [-L <LV size>][-n <LV name>] <VG name>.
``` Take creating an 8 GB logical volume named `lv_0` as an example, run the following command:
```plaintext
lvcreate -L 8G -n lv_0 lvm_demo0
``` The result of a successful creation is shown below:
![](https://main.qcloudimg.com/raw/ed6d2f827ae7c4a4630bf17e24d90df2.png)
>?Run the `pvs` command. You can see that only the capacity of the `/dev/vdc` disk is reduced by 8 GB, as shown below:
>![](https://main.qcloudimg.com/raw/2718d08f7c74b7b469a23473a1398dfe.png)

### Step 4: create and mount a file system
1. Run the following command to create a file system on an existing LV.
```plaintext
mkfs.ext3 /dev/lvm_demo0/lv_0
```
2. Run the following command to create the mount point `/vg0`.
```plaintext
mkdir /vg0
```
3. Run the following command to mount the file system.
```plaintext
mount /dev/lvm_demo0/lv_0 /vg0
``` The result of a successful mount is shown below:
![](https://main.qcloudimg.com/raw/34af8440192a1fa74f85ea44b6354194.png)

### Step 5: resize the logical volume and file system dynamically
>!LVs can be extended dynamically only when the VG capacity is not used up. After increasing the LV capacity, you need to extend the file system created on this LV.
>
1. Run the following command to extend the LV.
```plaintext
lvextend [-L +/- <scale capacity>] <LV path>
``` Take extending the LV named `lv_0` by 4 GB as an example, run the following command:
```plaintext
lvextend -L +4G /dev/lvm_demo0/lv_0
``` The result of a successful extension is shown below:
![](https://main.qcloudimg.com/raw/eccd7d6aec587eb90ec655a384367595.png)
>?Run the `pvs` command. You can find that the `/dev/vdc` disk capacity has been fully used, and the `/dev/vdd` disk capacity has been used by 2 GB, as shown below:
>![](https://main.qcloudimg.com/raw/189155ca377ef9550c4587ca78ab5b27.png)
2. Run the following command to extend the file system.
```plaintext
resize2fs /dev/lvm_demo0/lv_0
``` The result of a successful extension is shown below:
![](https://main.qcloudimg.com/raw/2e37f35678014ab1ca398fe5470a754b.png)
After the extension, run the following command to check whether the LV capacity is 12 GB.
```plaintext
df -h
```




