## Overview

This document provides an overview of APIs and SDK code samples related to how to create a bucket.


| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under a specified account |


## Creating a Bucket

#### Description

This API is used to create a bucket under the specified account. You can create multiple buckets under the same user account. The maximum number is 200 (regardless of region). There is no limit to the number of objects in the bucket. Bucket creation is a low-frequency operation. We recommended you create a bucket in the console and perform object operations in the SDK.

#### Method prototype

```php
public Guzzle\Service\Resource\Model createBucket(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket)

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
            
try {
    $result = $cosClient->createBucket(array(
        'Bucket' => 'examplebucket-125000000' // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Parent Node | Description | Type | 
| -------- | ------ | ---------------------------------- | ------ |
| Bucket | None | Bucket name in the format of `BucketName-APPID` | String |