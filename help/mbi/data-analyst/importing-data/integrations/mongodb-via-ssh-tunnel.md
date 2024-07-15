---
title: 通过SSH通道连接 [!DNL MongoDB]
description: 了解如何通过SSH隧道连接 [!DNL MongoDB] 。
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# 通过SSH通道连接[!DNL MongoDB]

要通过SSH通道将[!DNL MongoDB]数据库连接到[!DNL Commerce Intelligence]，您必须执行以下几项操作：

1. [检索 [!DNL Commerce Intelligence] 公钥](#retrieve)
1. [允许访问 [!DNL Commerce Intelligence] IP地址](#allowlist)
1. [创建Commerce Intelligence的Linux用户](#linux)
1. [为Commerce Intelligence创建 [!DNL MongoDB] 用户](#mongodb)
1. [在 [!DNL Commerce Intelligence]中输入连接和用户信息](#finish)

>[!NOTE]
>
>由于此设置的技术性质，Adobe建议您在开发人员中循环，以帮助您解决以前未完成此设置的问题。

## 正在检索[!DNL Commerce Intelligence]公钥 {#retrieve}

`public key`用于授权[!DNL Commerce Intelligence] `Linux`用户。 下一部分将指导您完成创建用户和导入密钥的过程。

1. 转到&#x200B;**[!UICONTROL Data** > **Connections]**&#x200B;并单击&#x200B;**[!UICONTROL Add New Data Source]**。
1. 单击[!DNL MONGODB]图标。
1. 打开[!DNL MongoDB]凭据页面后，将`Encrypted`切换更改为`Yes`。 此时将显示SSH设置表单。
1. `public key`位于此表单下。

在整个教程中保持此页面处于打开状态 — 您将在下一部分和结尾处找到它。

如果您丢失了一点，下面是如何浏览[!DNL Commerce Intelligence]以检索密钥的：

![正在检索RJMetrics公钥](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## 允许访问[!DNL Commerce Intelligence] IP地址 {#allowlist}

要使连接成功，必须将防火墙配置为允许从IP地址访问。 它们是`54.88.76.97`和`34.250.211.151`，但它也位于[!DNL MongoDB]凭据页面上：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 正在为[!DNL Commerce Intelligence]创建`Linux`用户 {#linux}

>[!IMPORTANT]
>
>如果与服务器关联的`sshd_config`文件未设置为默认选项，则只有某些用户具有服务器访问权限 — 这会阻止成功连接到[!DNL Commerce Intelligence]。 在这些情况下，需要运行诸如`AllowUsers`之类的命令以允许`rjmetric`用户访问服务器。

这可以是生产或辅助计算机，只要它包含实时（或经常更新）数据。 您可以按您喜欢的方式限制此用户，只要它保留连接到[!DNL MongoDB]服务器的权利即可。

要添加新用户，请以root用户身份在`Linux`服务器上运行以下命令：

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

是否记得在第一节中检索到的`public key`？ 为确保用户有权访问数据库，您需要将密钥导入`authorized_keys`。 按如下方式将整个密钥复制到`authorized_keys`文件中：

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

要完成创建用户，请更改/home/rjmetric目录上的权限以允许通过SSH进行访问：

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## 创建[!DNL Commerce Intelligence] [!DNL MongoDB]用户 {#mongodb}

[!DNL MongoDB]服务器具有两种运行模式 — [一种使用“auth”选项](#auth) `(mongod -- auth)`，另一种不使用[，这是默认值](#default)。 创建[!DNL MongoDB]用户的步骤因服务器使用的模式而异。 继续之前，请务必验证模式。

### 如果您的服务器使用`Auth`选项： {#auth}

连接到多个数据库时，您可以通过以管理员用户身份登录[!DNL MongoDB]并运行以下命令来添加用户。

>[!NOTE]
>
>要查看所有可用数据库，[!DNL Commerce Intelligence]用户需要运行`listDatabases.`的权限

此命令授予[!DNL Commerce Intelligence]用户访问`to all databases`的权限：

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

使用此命令授予[!DNL Commerce Intelligence]用户访问`to a single database`的权限：

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

这将打印如下响应：

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### 如果您的服务器使用默认选项 {#default}

如果您的服务器不使用`auth`模式，那么即使没有用户名和密码，[!DNL MongoDB]服务器也可以访问。 但是，您应确保`mongodb.conf`文件`(/etc/mongodb.conf)`具有以下行 — 如果不存在，请在添加后重新启动服务器。

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

若要将[!DNL MongoDB]服务器绑定到其他地址，请在下一步中相应地调整数据库主机名。

## 在[!DNL Commerce Intelligence]中输入连接和用户信息 {#finish}

要完成工作，您需要在[!DNL Commerce Intelligence]中输入连接和用户信息。 您是否让[!DNL MongoDB]凭据页面保持打开状态？ 如果没有，请转到&#x200B;**[!UICONTROL Data > Connections]**&#x200B;并单击&#x200B;**[!UICONTROL Add New Data Source]**，然后单击[!DNL MongoDB]图标。 别忘了将`Encrypted`切换更改为`Yes`。

在此页面中输入以下信息，从`Database Connection`部分开始：

* `Host`： `127.0.0.1`
* `Username`： [!DNL Commerce Intelligence] [!DNL MongoDB]用户名（应为`rjmetric`）
* `Password`： [!DNL Commerce Intelligence] [!DNL MongoDB]密码
* `Port`：您的服务器上的MongoDB端口（默认为`27017`）
* `Database Name` （可选）：如果只允许访问一个数据库，请在此处指定该数据库的名称。

在`SSH Connection`部分下：

* `Remote Address`：要通过SSH连接的服务器的IP地址或主机名
* `Username`： [!DNL Commerce Intelligence] Linux (SSH)用户名（应为rjmetric）
* `SSH Port`：服务器上的SSH端口（默认为22）

完成后，单击&#x200B;**[!UICONTROL Save Test]**&#x200B;以完成设置。

### 相关

* [正在重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
