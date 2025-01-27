You can create a cloud disk and attach it to your available CVM instance. The cloud disk can be used as the data disk of the CVM instance after simple initialization procedure. To do this, complete the following steps:
- [Step 1. Creating Cloud Disks](https://intl.cloud.tencent.com/document/product/362/31647)
- [Step 2. Attaching Cloud Disks](https://intl.cloud.tencent.com/document/product/362/39991)
- [Step 3. Initializing Cloud Disks](https://intl.cloud.tencent.com/document/product/362/31645)
- [Step 4. Expanding Cloud Disk (Optional)](https://intl.cloud.tencent.com/document/product/362/31646)

## Overview
This document guides you through how to create a cloud disk `cbs-test` in the Beijing Zone 2 in the console.

## Notes
- Make sure you have an available CVM instance in the availability zone (Beijing Zone 2 in this example) where the cloud disk is to be created.
- For more information about how to purchase and start up a CVM instance, see [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517) and [Customizing Windows CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10516).

## Directions
>?In this example, an elastic premium cloud disk is purchased via the console. For more information on cloud disk creation, see [Creating Cloud Disks](https://intl.cloud.tencent.com/document/product/362/5744).

1. Log in to the CVM console and click [**Cloud Block Storage**](https://console.cloud.tencent.com/cvm/cbs) on the left sidebar.
2. Select **Beijing** at the top of the Cloud Block Storage list page, and click **Create**.
3. Configure the following parameters in the pop-up window:
 - **Availability Zone**: select **Beijing Zone 2**.
 - **Cloud Disk Type**: select **Premium Cloud Storage**.
 - **Capacity**: set to 20 GB.
 - **Disk Name**: enter `cbs-test`.

4. Click **OK**.
5. After confirming the configurations, click **OK** and make the payment.
Return to the Cloud Block Storage list page. You can now view the purchased elastic cloud disk `cbs-test`, whose status is **To be attached**.


## Subsequent Operations
After the cloud disk is created, you need to first attach it to a CVM in the same availability zone as a data disk. For more information about this operation, see [Step 2. Attaching Cloud Disks](https://intl.cloud.tencent.com/document/product/362/39991).
