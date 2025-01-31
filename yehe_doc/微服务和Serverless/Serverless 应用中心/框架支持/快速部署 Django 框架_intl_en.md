## Overview


This document describes how to quickly deploy a local Django project to the cloud through a web function.

>?This document mainly describes how to deploy in the console. You can also complete the deployment on the command line. For more information, please see [Deploying Framework on Command Line](https://intl.cloud.tencent.com/document/product/1040/41597).


## Prerequisites
Before using SCF, you need to sign up for a [Tencent Cloud account](https://Intl.cloud.tencent.com/register) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629) first.

## Directions

### Template deployment - quick deployment of Django project

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and click **Function Service** on the left sidebar.
2. Select the region where to create a function at the top of the page and click **Create** to enter the function creation process.
3. Select **Template** for **Creation Method**, enter `Django` in the search box, select **Django Framework Template**, and click **Next** as shown below:
![](https://main.qcloudimg.com/raw/e0a04cd3cb345c6c9c8c2f229528a013.png)
4. On the **Configuration** page, you can view and modify the specific configuration information of the template project.
5. Click **Complete**. After creating the web function, you can view its basic information on the **Function Management** page.
6. You can access the deployed Django project at the access path URL generated by API Gateway. Click **Trigger Management** on the left to view the access path as shown below:
![](https://main.qcloudimg.com/raw/e3b1e5cd072c81b14e2555468f4c9499.png)
7. Click the access path URL to access the Django project.



### Custom deployment - quick migration of local project to cloud

#### Local development

1. Run the following command to confirm that Django has been installed in your local environment.
```shell
python -m pip install Django
```
2. Create the `Hello World` sample project locally.
```sh
django-admin startproject helloworld && cd helloworld
```
 The directory structure is as follows:
```
$ tree
. manage.py   Manager
|--*** 
|   |-- __init__.py   Package
|   |-- settings.py   Settings file
|   |-- urls.py   Route
|   `-- wsgi.py   Deployment
```
3. Run the `python manage.py runserver` command locally to start the bootstrap file. Below is the sample code:
<dx-codeblock>
:::  python
$ python manage.py runserver
July 27, 2021 - 11:52:20
Django version 3.2.5, using settings 'helloworld.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
:::
</dx-codeblock>
4. Visit `http://127.0.0.1:8000` in a browser, and you can access the sample Django project locally as shown below:
![](https://main.qcloudimg.com/raw/a09696d7d24c719ecb2f276c4bba93ce.png)


#### Deployment in cloud

Next, perform the following steps to make simple modifications to the locally created project, so that it can be quickly deployed through a web function. The steps of project transformation for Django are as follows:


1. **Install dependencies**
 1. As the Django dependency library is not provided in the standard cloud environment of SCF, you must install the dependencies and upload them together with the project code. Please create the `requirements.txt` file first with the following content:
```txt
Django==3.1.3
```
 2. Run the following command to install:
```shell
pip install -r requirements.txt -t .
```
>?As the initialized default project imports the `db.sqlite3` library, please install this dependency synchronously or configure comments for the `DATABASES` field in the `setting.py` file of the project.
>
2. **Add the `scf_bootstrap` bootstrap file**
The listening port in the web function must be **9000**, so you need to change the listening address and port in the following way: create the `scf_bootstrap` bootstrap file in the project root directory and add the following content to it (which is used to configure environment variables, specify service bootstrap commands, and make sure that your service can be started normally through this file):
```
#!/bin/bash
/var/lang/python3/bin/python3 manage.py runserver 9000
```

3. After the creation is completed, you need to run the following command to modify the executable permission of the file. By default, the permission `777` or `755` is required for it to start normally. Below is the sample code:
```shell
chmod 777 scf_bootstrap
```
>!
>- In the SCF environment, only files in the `/tmp` directory are readable/writable. We recommend you select `/tmp` when outputting files. If you select other directories, write will fail due to the lack of permissions.
>- If you want to output environment variables in the log, you need to add the `-u` parameter before the bootstrap command, such as `python -u app.py`.
>
4. After the local configuration is completed, run the following command to start the service (with execution in the `scf_bootstrap` directory as an example) and make sure that your service can be normally started locally.
>! Be sure to change the `python` path to the local path during local testing.
```shell
./scf_bootstrap
```

5. Log in to the [SCF console](https://console.cloud.tencent.com/scf/index?rid=1) and click **Function Service** on the left sidebar.
6. Select the region where to create a function at the top of the page and click **Create** to enter the function creation process.
7. Select **Custom Creation** for **Creation Method** and configure the options as prompted as shown below:
![](https://main.qcloudimg.com/raw/10dce3203472b93e65e66119e47135d8.png)
	- **Function Type**: select **Web function**.
	- **Function Name**: enter the name of your function.
	- **Region**: enter your function deployment region, such as Chengdu.
	- **Deployment Method**: select **Code deployment** and upload your local project.
	- **Runtime Environment**: select **Python 3.6**.
8. Click **Complete**.


#### Development management
After the deployment is completed, you can quickly access and test your web service in the SCF console and try out various features of SCF, such as layer binding and log management. In this way, you can enjoy the advantages of low cost and flexible scaling brought by the serverless architecture as shown below:
![](https://main.qcloudimg.com/raw/c87151ecbb2f7c7e7f2c6877a043eda6.png)
