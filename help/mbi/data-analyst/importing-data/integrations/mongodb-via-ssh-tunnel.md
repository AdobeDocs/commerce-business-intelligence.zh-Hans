---
title: 连接 [!DNL MongoDB] 通过SSH隧道
description: 了解如何连接 [!DNL MongoDB] 通过SSH隧道。
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# 连接 [!DNL MongoDB] 通过SSH隧道


连接 [!DNL MongoDB] 数据库到 [!DNL MBI] 通过SSH隧道，您（或您的团队，如果您不是技术人员）将需要执行以下操作：

1. [检索 [!DNL MBI] 公钥](#retrieve)
1. [允许访问 [!DNL MBI] IP地址](#allowlist)
1. [为MBI创建Linux用户](#linux)
1. [创建 [!DNL MongoDB] MBI用户](#mongodb)
1. [在 [!DNL MBI]](#finish)

>[!NOTE]
>
>由于此设置的技术性质，我们建议您在开发人员中循环使用，以在您之前未执行此操作时提供帮助。

## 检索 [!DNL MBI] 公钥 {#retrieve}

的 `public key` 用于授权 [!DNL MBI] `Linux` 用户。 在下一部分中，我们将创建用户并导入密钥。

1. 转到 **[!UICONTROL Data** > **Connections]** 单击 **[!UICONTROL Add New Data Source]**.
1. 单击 [!DNL MONGODB] 图标。
1. 在 [!DNL MongoDB] “凭据”页面打开，请更改 `Encrypted` 切换至 `Yes`. 此时将显示SSH设置表单。
1. 的 `public key` 位于此表单下方。

在整个教程中，请保持此页面处于打开状态 — 您将在下一部分和最后需要该页面。

如果你有点迷路，请看下面是如何浏览 [!DNL MBI] 要检索密钥，请执行以下操作：

![检索RJMetrics公钥](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## 允许访问 [!DNL MBI] IP地址 {#allowlist}

要使连接成功，您必须配置防火墙以允许从我们的IP地址访问。 是 `54.88.76.97` 和 `34.250.211.151`，但也在 [!DNL MongoDB] 凭据页：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 创建 `Linux` 用户 [!DNL MBI] {#linux}

>[!IMPORTANT]
>
>如果 `sshd_config` 与服务器关联的文件未设置为默认选项，只有某些用户具有服务器访问权限 — 这将阻止成功连接到 [!DNL MBI]. 在这些情况下，必须运行类似 `AllowUsers` 允许 `rjmetric` 用户对服务器的访问权限。

这可以是生产计算机或辅助计算机，但前提是它包含实时（或经常更新）数据。 只要此用户保留连接到的权限，您就可以按您喜欢的任何方式限制此用户 [!DNL MongoDB] 服务器。

要添加新用户，请在 `Linux` 服务器：

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

记住 `public key` 我们在第一部分找到了？ 为确保用户有权访问数据库，我们需要将密钥导入 `authorized_keys`. 将整个密钥复制到 `authorized_keys` 文件如下：

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

要完成用户的创建，请更改/home/rjmetric目录上的权限以允许通过SSH访问：

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## 创建 [!DNL MBI] [!DNL MongoDB] 用户 {#mongodb}

[!DNL MongoDB] 服务器有两种运行模式 —  [带有“auth”选项的](#auth) `(mongod -- auth)` 一个没有， [默认值](#default). 创建 [!DNL MongoDB] 用户将因服务器所使用的模式而有所不同，因此请务必先验证该模式，然后再继续。

### 如果您的服务器使用 `Auth` 选项： {#auth}

连接到多个数据库时，您可以通过登录来添加用户 [!DNL MongoDB] 作为管理员用户并运行以下命令。

>[!NOTE]
>
>要查看所有可用的数据库，请 [!DNL MBI] 用户需要运行权限 `listDatabases.`

此命令将授予 [!DNL MBI] 用户访问 `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

使用此命令可授予 [!DNL MBI] 用户访问 `to a single database`:

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

这将打印如下所示的响应：

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### 如果您的服务器使用默认选项 {#default}

如果您的服务器未使用 `auth` 模式， [!DNL MongoDB] 即使没有用户名和密码，服务器仍可访问。 但是，您应确保 `mongodb.conf` 文件 `(/etc/mongodb.conf)` 具有以下行 — 如果没有，则在添加服务器后重新启动服务器。

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

绑定 [!DNL MongoDB] 服务器到其他地址，在下一步中相应地调整数据库主机名。

## 在中输入连接和用户信息 [!DNL MBI] {#finish}

总结一下，我们需要在 [!DNL MBI]. 你离开 [!DNL MongoDB] 凭据页面打开？ 如果没有，请转到 **[!UICONTROL Data > Connections]** 单击 **[!UICONTROL Add New Data Source]**，则 [!DNL MongoDB] 图标。 不要忘记改变 `Encrypted` 切换至 `Yes`.

在此页面中输入以下信息(从 `Database Connection` 部分：

* `Host`: `127.0.0.1`
* `Username`:的 [!DNL MBI] [!DNL MongoDB] 用户名(应 `rjmetric`)
* `Password`:的 [!DNL MBI] [!DNL MongoDB] 密码
* `Port`:服务器上的MongoDB端口(`27017` 默认)
* `Database Name` （可选）：如果只允许访问一个数据库，请在此处指定该数据库的名称。

在 `SSH Connection` 部分：

* `Remote Address`:我们要SSH到的服务器的IP地址或主机名
* `Username`:的 [!DNL MBI] Linux(SSH)用户名（应为rjmetric）
* `SSH Port`:服务器上的SSH端口（默认为22个）

就这样！ 完成后，单击 **[!UICONTROL Save Test]** 以完成设置。

### 相关

* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
