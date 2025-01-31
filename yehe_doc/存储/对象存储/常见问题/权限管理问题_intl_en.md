## Keys

### How can I view the key information such as `APPID`, `SecretId`, and `SecretKey`?

The second half of a bucket name is the `APPID`. You can view it by logging in to the [COS console](https://console.cloud.tencent.com/cos5/bucket). To view information such as `SecretId` and `SecretKey`, log in to the CAM console and go to [Manage API Key](https://console.cloud.tencent.com/cam/capi).

### How long will a temporary key be valid?

Currently, a temporary key can be valid for up to 2 hours (i.e., 7,200 seconds) for the root account, and 36 hours (i.e., 129,600 seconds) for a sub-account. The default validity period is 30 minutes (i.e., 1,800 seconds). Requests carrying an expired temporary key will be denied. For more information, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).

### What do I do if my key information such as `SecretId` and `SecretKey` is compromised?

You can delete the compromised key and create a new one. For more information, please see [Access Key](https://intl.cloud.tencent.com/document/product/598/34227).

### How can I generate a time-bound access URL for a Private Read/Write file?

You can set a validity period for your key by referring to [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).

## Permissions

### How can I grant a sub-account permission to access a specific folder?

You can grant such permission by referring to [Setting Folder Permissions](https://intl.cloud.tencent.com/document/product/436/35261). To grant more advanced permissions to a sub-account, please see [Cases of Permission Setting](https://intl.cloud.tencent.com/document/product/436/12514).



### What do I do if “AccessDenied” is reported?

In most cases, this error is reported due to unauthorized access or insufficient permissions. You can troubleshoot as follows:

1. Check whether the configuration of `BucketName`, `APPID`, `Region`, `SecretId`, and `SecretKey` is correct. Note that you should also check whether spaces are carried.
2. If the configuration above is correct, check whether a sub-account is used for the operation. If yes, check whether the sub-account has been authorized by the root account. If it has not yet been authorized, log in using the root account to authorize the sub-account. For more information about authorization, please see [Cases of Permission Settings](https://intl.cloud.tencent.com/document/product/436/12514).
3. If a temporary key is used, check whether the current operation is in the policy set when the temporary key is obtained; if not, modify the relevant policy settings. For more information, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).


### What do I do if the number of bucket permissions has reached the upper limit?

Each root account (i.e., each `APPID`) can have up to 1,000 bucket ACLs. If more bucket ACLs have been configured, an error will be reported. Therefore, you are advised to delete unnecessary ACLs.

>?You are not advised to use file-level ACLs or policies. When calling APIs or SDKs, if you do not need ACL control over a file, we recommend leaving the ACL-related parameters (such as x-cos-acl and ACL) empty to inherit the bucket permissions.

### What should I do if an incorrect permission error is reported when I am creating a bucket?

This is because your bucket is set to public read/private write, or public read/write. These permissions occupy the number of ACLs your root account is allowed to use. This error is reported because the root account has used up the number of ACLs allowed, which cannot be adjusted.

The following two solutions are provided for your reference:

Solution 1: Set the access permission of the bucket to private read/write. For more information, please see [Setting Access Permission](https://intl.cloud.tencent.com/document/product/436/13315).
Solution 2: In **Permission Policy Settings**, click **Add Policy** and configure access permissions as needed. For more information, please see [Adding Bucket Policies](https://intl.cloud.tencent.com/document/product/436/30927).


### Can I access a public-read file using a signed URL whose signature has expired?

If you use an expired signed URL to access a public-read file, COS will first verify the permissions. If the URL has expired, the access will be denied.

### What do I do if "403 Forbidden" or “permission rejected” is reported during uploads, downloads, or other operations?

You can troubleshoot as follows:

1. Check whether the configuration of `BucketName`, `APPID`, `Region`, `SecretId`, and `SecretKey` is correct.
2. If the configuration above is correct, check whether a sub-account is used for the operation. If yes, check whether the sub-account has been authorized by the root account. If it has not yet been authorized, log in using the root account to authorize the sub-account. For more information about authorization, please see [Cases of Permission Settings](https://intl.cloud.tencent.com/document/product/436/12514).
3. If a temporary key is used, check whether the current operation is in the policy set when the temporary key is obtained; if not, modify the relevant policy settings. For more information, please see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).


### How can I prevent users from downloading COS data?

You can prevent users from downloading data based on your use case as follows:

1. To prevent sub-accounts from downloading data, please see [Granting Sub-accounts Access to COS](https://intl.cloud.tencent.com/document/product/436/11714).
2. To prevent anonymous users from downloading data, you can set your bucket to private-read/write, or set `deny anyone Get Object` in the bucket policy.

### How can I grant permissions to a sub-account under another root account?

Assume that you (root account A) need to grant bucket permissions to the sub-account B0 that is under the root account B. You need to first grant the root account B permissions to operate your bucket. Then, root account B should grant the permissions to its sub-account B0. For detailed directions, please see [Granting Sub-account Under One Root Account Permission to Manipulate Buckets Under Another Root Account](https://intl.cloud.tencent.com/document/product/436/32971).

### How can I only allow sub-accounts/collaborators to upload but not delete files?

You can log in to the [CAM console](https://console.cloud.tencent.com/cam/policy) to create a custom policy that grants specified permissions to sub-accounts. For detailed directions, please see [Creating Custom Policies](https://intl.cloud.tencent.com/document/product/598/35596).

>? When creating the custom policy, you need to grant read permissions, set upload only for write operations, and **do not grant delete permissions**.
>
![](https://main.qcloudimg.com/raw/578ae1960f7f8b182503cef5653dc829.png)

### When I access a public-read bucket using its default domain name, how can I hide the returned file list?

You can set a permission to deny anyone's Get Bucket operation for the bucket by following the steps below:

Log in to the [COS console](https://console.cloud.tencent.com/cos5), click **Bucket List**, click the desired bucket, and select **Permission Management**.

#### Method 1:

1. Click **Permission Policy Settings**. Then, click **Add Policy** under **Visual Editor**.
2. Configure the permissions as shown below and then click **OK**.
   ![Policy Visual Editor](https://main.qcloudimg.com/raw/60e17e3473bfb309376a6e54327a41b0.png)

#### Method 2:

Click **Permission Policy Settings**. Then, click **JSON** > **Edit** and enter the following code:

```
{
 "Statement": [
   {
     "Action": [
       "name/cos:GetBucket",
       "name/cos:GetBucketObjectVersions"
     ],
     "Effect": "Deny",
     "Principal": {
       "qcs": [
         "qcs::cam::anyone:anyone"
       ]
     },
     "Resource": [
       "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*"
     ]
   }
 ],
 "version": "2.0"
}
```

>!
> Replace values in `qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*` with the actual information as follows:
>
> - “ap-beijing”: Replace it with the region where your bucket resides.
> - “1250000000”: Replace it with your `APPID`.
> - “examplebucket-1250000000”: Replace it with your bucket name.
>
> The second half of the bucket name is the `APPID`. You can view it by logging in to the [COS console](https://console.cloud.tencent.com/cos5/bucket).

### Are COS's ACLs bucket-specific or account-specific? Can I specify permissions when uploading files?

ACLs are account-specific. You are not advised to use file-level ACLs or policies. When calling APIs or SDKs, if you do not need ACL control over a file, we recommend leaving the ACL-related parameters (such as x-cos-acl and ACL) empty to inherit the bucket permissions.

### How do I authorize a collaborator to access a specified bucket?

A collaborator is a special sub-account. For more information, please see [Access Policy Language Overview](https://intl.cloud.tencent.com/document/product/436/18023).

### Can I isolate permissions by buckets or other dimensions if I have multiple services that need to work with buckets?

You can log in to the [CAM console](https://console.cloud.tencent.com/cam/overview) to go to the **User Management** page, where you can create sub-accounts for different services and grant different permissions for them.

### How can I create sub-accounts for subsidiaries or employees and grant them permissions to access specific buckets?

You can create sub-accounts and grant them permissions by referring to [Granting Sub-accounts Access to COS](https://intl.cloud.tencent.com/document/product/436/11714).

### How can I allow specific sub-accounts to only operate a certain bucket?

To grant a sub-account access to a specific bucket, you can add access paths for the sub-account. For more information, see [Accessing Bucket List Using a Sub-account](https://intl.cloud.tencent.com/document/product/436/17061).

## Other

### What do I do if I cannot access COS resources normally?

You can troubleshoot by referring to [Resource Access Error](https://intl.cloud.tencent.com/document/product/436/40167).

### What do I do if “HTTP ERROR 403” is returned when I access COS using a CDN domain?

This is usually because the CDN acceleration domain is disabled. You can troubleshoot by referring to [“HTTP ERROR 403” is Returned When I Access COS Using a CDN Domain](https://intl.cloud.tencent.com/document/product/436/40175).

### What do I do if I use a CDN domain name to access COS but only access the old version of the file?

This is usually because of the existing cache. You can troubleshoot by referring to [A URL Points to a Wrong File](https://intl.cloud.tencent.com/document/product/436/40170).

### Can the front-end access COS using CDN and a temporary key?

If you need authentication when CDN pulls from COS with files set to private read/write, please see [CDN Origin-Pull Authentication](https://intl.cloud.tencent.com/document/product/436/18670).
