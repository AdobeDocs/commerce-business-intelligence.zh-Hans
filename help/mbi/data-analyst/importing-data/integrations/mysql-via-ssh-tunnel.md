---
title: 正在连接 [!DNL MySQL] 通过SSH通道
description: 了解如何连接 [!DNL MySQL] 通过SSH通道。
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# Connect [!DNL MySQL] via [!DNL SSH Tunnel]

* [检索 [!DNL Commerce Intelligence] 公钥](#retrieve)
* [允许访问 [!DNL Commerce Intelligence] IP地址](#allowlist)
* [为创建Linux用户 [!DNL Commerce Intelligence]](#linux)
* [创建 [!DNL MySQL] 用户 [!DNL Commerce Intelligence]](#mysql)
* [将连接和用户信息输入到 [!DNL Commerce Intelligence]](#finish)

## 跳转到

* [[!DNL MySQL] via ](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL] via [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

连接您的 [!DNL MySQL] 数据库至 [!DNL Commerce Intelligence] 通过 `SSH tunnel`，您必须执行以下操作：

1. 检索 [!DNL Commerce Intelligence] `public key`
1. 允许访问 [!DNL Commerce Intelligence] `IP address`
1. 创建 `Linux` 用户 [!DNL Commerce Intelligence]
1. 创建 `MySQL` 用户 [!DNL Commerce Intelligence]
1. 将连接和用户信息输入到 [!DNL Commerce Intelligence]


## 正在检索 [!DNL Commerce Intelligence] 公钥 {#retrieve}

此 `public key` 用于授权 [!DNL Commerce Intelligence] `Linux` 用户。 在下一部分中，您将创建用户并导入密钥。

1. 转到 **[!UICONTROL Manage Data** > **Connections]** 并单击 **[!UICONTROL Add New Data Source]**.
1. 单击 `MySQL` 图标。
1. 在 `MySQL credentials` 页面打开，设置 `Encrypted` 切换到 `Yes`. 这将显示SSH设置表单。
1. 此 `public key` 位于此表单下。

在整个教程中保持此页面处于打开状态 — 您需要在下一部分和结尾处打开此页面。

以下是如何导航浏览的 [!DNL Commerce Intelligence] 要检索密钥，请执行以下操作：

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## 允许访问 [!DNL Commerce Intelligence] IP地址 {#allowlist}

要使连接成功，必须将防火墙配置为允许从IP地址访问。 它们是 `54.88.76.97` 和 `34.250.211.151` 但它们也在 `MySQL credentials` 页面。 请参阅上面GIF中的蓝色方框。

## 创建 [!DNL Linux] 用户 [!DNL Commerce Intelligence] {#linux}

这可以是生产或辅助计算机，只要它包含实时（或经常更新）数据即可。 您可以 [限制此用户](../../../administrator/account-management/restrict-db-access.md) 任何您喜欢的方式，只要它保留连接到 `MySQL` 服务器。

1. 要添加新用户，请以root用户身份在 [!DNL Linux] 服务器：

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. 记住 `public key` 你是在第一节中找回的吗？ 要确保用户有权访问数据库，您需要将密钥导入 `authorized\_keys`.

   将整个密钥复制到 `authorized\_keys` 文件如下所示：

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. 要完成创建用户，请更改以下项的权限： `/home/rjmetric` 允许通过以下方式访问的目录 `SSH`：

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>如果 `sshd\_config` 与服务器关联的文件未设置为默认选项，仅某些用户具有服务器访问权限 — 这会阻止成功连接到 [!DNL Commerce Intelligence]. 在这些情况下，必须运行命令，例如 `AllowUsers` 以允许 `rjmetric` 用户对服务器的访问权限。

## 创建 [!DNL MySQL] 用户 [!DNL Commerce Intelligence] {#mysql}

您的组织可能需要不同的流程，但创建此用户的最简单方法是在登录时执行以下查询 [!DNL MySQL] 作为有权授予权限的用户：

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Replace `secure password here` 安全密码，该密码可以不同于 `SSH` 密码。

要限制此用户访问特定数据库、表或列中的数据，您可以改为运行仅允许访问您允许的数据的GRANT查询。

## 将连接和用户信息输入到 [!DNL Commerce Intelligence] {#finish}

要完成这些操作，您需要将连接和用户信息输入到 [!DNL Commerce Intelligence]. 您是否离开了 `MySQL credentials` 是否打开页面？ 如果不能，请转到 **[!UICONTROL Data** > **Connections]** 并单击 **[!UICONTROL Add New Data Source]**，则 [!DNL MySQL] 图标。 不要忘记设置 `Encrypted` 切换到 `Yes`.

在此页面中输入以下信息，从 `Database Connection` 部分：

* `Username`：的用户名 [!DNL Commerce Intelligence] [!DNL MySQL] 用户
* `Password`：的密码 [!DNL Commerce Intelligence] [!DNL MySQL] 用户
* `Port`： [!DNL MySQL] 服务器上的端口（默认为3306）
* `Host` 默认情况下，这是localhost。 通常，它是的绑定地址值 [!DNL MySQL] 服务器，默认情况下为 `127.0.0.1 (localhost)`，但也可以是某个本地网络地址(例如， `192.168.0.1`)或服务器的公共IP地址。

  该值可在以下位置找到： `my.cnf` 文件(位于 `/etc/my.cnf`)下，代码为 `\[mysqld\]`. 如果bind-address行在该文件中被注释掉，则您的服务器不会受到外部连接尝试的保护。

在 `SSH Connection` 部分：

* `Remote Address`：服务器的IP地址或主机名 [!DNL Commerce Intelligence] 将隧道连接至
* `Username`：的用户名 [!DNL Commerce Intelligence] SSH ([!DNL Linux])用户
* `SSH Port`：服务器上的SSH端口（默认为22）

完成后，单击 **[!UICONTROL Save & Test]** 以完成设置。

## 相关：

* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
