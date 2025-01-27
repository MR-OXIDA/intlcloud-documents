## 操作场景

本文将为您指导如何通过 Web Function，将您的本地 Express 项目快速部署到云端。


>?本文档主要介绍控制台部署方案，您也可以通过命令行完成部署，详情请参见 [通过命令行完成框架部署](https://intl.cloud.tencent.com/document/product/583/41586)。



## 前提条件

在使用腾讯云云函数服务之前，您需要 [注册腾讯云账号](https://intl.cloud.tencent.com/register) 并完成 [实名认证](https://intl.cloud.tencent.com/document/product/378/3629)。

## 操作步骤


### 模版部署 -- 一键部署 Express 项目


1. 登录 [Serverless 控制台](https://console.cloud.tencent.com/scf/index?rid=1)，单击左侧导航栏的【函数服务】。
2. 在主界面上方选择期望创建函数的地域，并单击【新建】，进入函数创建流程。
3. 选择使用【模版创建】来新建函数，在搜索框里输入 `WebFunc` 筛选所有 Web 函数模版，选择【Express 框架模版】并单击【下一步】。如下图所示：
![](https://main.qcloudimg.com/raw/e0a04cd3cb345c6c9c8c2f229528a013.png)
4. 在“配置”页面，您可以查看模版项目的具体配置信息并进行修改。
5. 单击【完成】即可创建函数。函数创建完成后，您可在“函数管理”页面，查看 Web 函数的基本信息。
6. 您可以通过 API 网关生成的访问路径 URL，访问您部署的 Express 项目。单击左侧菜单栏中的【触发管理】，查看访问路径。如下图所示：
![](https://main.qcloudimg.com/raw/e3b1e5cd072c81b14e2555468f4c9499.png)
7. 单击访问路径 URL，即可访问服务 Express 项目。




### 自定义部署 -- 快速迁移本地项目上云


#### 前提条件

本地已安装 Node.js 运行环境。

#### 本地开发

1. 执行以下命令安装 Express 框架和 express-generator 脚手架，并初始化 Express 示例项目。
```shell
npm install express --save
npm install express-generator --save
express WebApp
```
2. 执行以下命令，进入项目目录并安装依赖包。
```shell
cd WebApp
npm install
```
3. 安装完成后，执行以下命令在本地直接启动服务。
```shell
npm start
```
4. 打开浏览器访问 `http://localhost:3000`，即可在本地完成 Express 示例项目的访问。



#### 部署上云

接下来执行以下步骤，对已初始化的项目进行简单修改，使其可以通过 Web Function 快速部署，此处项目改造通常分为以下两步：

- 修改监听地址与端口为 `0.0.0.0:9000`。
- 新增 `scf_bootstrap` 启动文件。

具体步骤如下：
1. 在 Express 示例项目中，可通过 `./bin/www` 设置监听地址与端口，打开该文件可以发现，通过环境变量可以设置指定监听端口，否则将自动监听**3000**端口。如下图所示：
![](https://main.qcloudimg.com/raw/a32fd560e9a6e58e6a1f6a46356324e6.png)
2. 在项目根目录下新建 `scf_bootstrap` 启动文件，在该文件添加如下内容（用于配置环境变量和启动服务）：
<dx-codeblock>
:::  shell
#!/bin/bash
export PORT=9000
npm run start
:::
</dx-codeblock>
3. 新建完成后，还需执行以下命令修改文件可执行权限，默认需要 `777` 或 `755` 权限才可正常启动。示例如下：
<dx-codeblock>
:::  shell
chmod 777 scf_bootstrap
:::
</dx-codeblock>
4. 本地配置完成后，执行以下命令启动文件（如下命令为在该文件 `scf_bootstrap` 目录下执行时示例），确保您的服务在本地可以正常启动。
<dx-codeblock>
:::  shell
./scf_bootstrap
:::
</dx-codeblock>
5. 登录 [Serverless 控制台](https://console.cloud.tencent.com/scf/index?rid=1)，单击左侧导航栏的【函数服务】。
6. 在主界面上方选择期望创建函数的地域，并单击【新建】，进入函数创建流程。
7. 选择【自定义创建】新建函数，根据页面提示配置相关选项。如下图所示：
![](https://main.qcloudimg.com/raw/563fa4d0a8a3e8d098d1d2505f785e1a.png)
	- **函数类型**：选择 “Web 函数”。
	- **函数名称**：填写您自己的函数名称。
	- **地域**：填写您的函数部署地域，默认为广州。
	- **运行环境**：选择 “Nodejs 12.16”。
	- **部署方式**：选择“代码部署”，上传您的本地项目。
	- **提交方法**：选择“本地上传文件夹”。
	- **函数代码**：选择函数代码在本地的具体文件夹。
8. 单击【完成】完成 Express 项目的部署。





#### 开发管理
部署完成后，即可在 SCF 控制台快速访问并测试您的 Web 服务，并且体验云函数多项特色功能，例如层绑定、日志管理等，享受 Serverless 架构带来的低成本、弹性扩缩容等优势。
