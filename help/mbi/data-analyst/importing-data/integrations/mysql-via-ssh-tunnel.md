---
title: 通过SSH隧道连接MySQL
description: 了解如何通过SSH隧道连接MySQL。
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# 连接 `MySQL` 通过 `SSH Tunnel`

* [检索 [!DNL MBI] 公钥](#retrieve)
* [允许访问 [!DNL MBI] IP地址](#allowlist)
* [为创建Linux用户 [!DNL MBI]](#linux)
* [为 [!DNL MBI]](#mysql)
* [在 [!DNL MBI]](#finish)

## 跳到

* `MySQL via SSH tunnel`
* [“MySQL”](../integrations/mysql-via-a-direct-connection.md)
* [“MySQL”](../integrations/mysql-via-cpanel.md)

连接 `MySQL` 数据库到 [!DNL MBI] 通过 `SSH tunnel`，则您（或您的团队，如果您不是技术人员）将需要执行以下操作：

1. 检索 [!DNL MBI] `public key`
1. 允许访问 [!DNL MBI] `IP address`
1. 创建 `Linux` 用户 [!DNL MBI]
1. 创建 `MySQL` 用户 [!DNL MBI]
1. 在 [!DNL MBI]

它不像听起来那么复杂。 让我们开始吧。

## 检索 [!DNL MBI] 公钥 {#retrieve}

的 `public key` 用于授权 [!DNL MBI] `Linux` 用户。 在下一部分中，我们将创建用户并导入密钥。

1. 转到 **[!UICONTROL Manage Data** > **Connections]** 单击 **[!UICONTROL Add New Data Source]**.
1. 单击 `MySQL` 图标。
1. 在 `MySQL credentials` 页面打开，设置 `Encrypted` 切换至 `Yes`. 此时将显示SSH设置表单。
1. 的 `public key` 位于此表单下方。

在整个教程中，请保持此页面处于打开状态 — 您将在下一部分和最后需要该页面。

如果你迷路了，请看下面是如何浏览 [!DNL MBI] 要检索密钥，请执行以下操作：

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## 允许访问 [!DNL MBI] IP地址 {#allowlist}

要使连接成功，您必须配置防火墙以允许从我们的IP地址访问。 是 `54.88.76.97` 和 `34.250.211.151` 但也在 `MySQL credentials` 页面。 看到上面GIF的蓝色方框？ 就这样！

## 创建 `Linux` 用户 [!DNL MBI] {#linux}

这可以是生产计算机或辅助计算机，但前提是它包含实时（或经常更新）数据。 您可以 [限制此用户](../../../administrator/account-management/restrict-db-access.md) 任何您喜欢的方式，只要它保留连接到 `MySQL` 服务器。

1. 要添加新用户，请在 `Linux` 服务器：

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. 记住 `public key` 我们在第一部分找到了？ 为确保用户有权访问数据库，我们需要将密钥导入 `authorized\_keys`.

   将整个密钥复制到 `authorized\_keys` 文件如下：

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. 要完成用户的创建，请更改 `/home/rjmetric` 允许通过访问的目录 `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>如果 `sshd\_config` 与服务器关联的文件未设置为默认选项，只有某些用户具有服务器访问权限 — 这将阻止成功连接到 [!DNL MBI]. 在这些情况下，必须运行类似 `AllowUsers` 允许 `rjmetric` 用户对服务器的访问权限。

## 创建 `MySQL` 用户 [!DNL MBI] {#mysql}

贵组织可能需要不同的流程，但创建此用户的最简单方法是，在登录后执行以下查询 `MySQL` 作为有权授予权限的用户：

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

替换 `secure password here` 具有安全密码，该密码可能与 `SSH` 密码。

要限制此用户访问特定数据库、表或列中的数据，您可以改为运行仅允许访问您允许的数据的GRANT查询。

## 在中输入连接和用户信息 [!DNL MBI] {#finish}

总结一下，我们需要在 [!DNL MBI]. 你离开 `MySQL credentials` 页面打开？ 如果没有，请转到 **[!UICONTROL Data** > **Connections]** 单击 **[!UICONTROL Add New Data Source]**，然后显示MySQL图标。 不要忘记设置 `Encrypted` 切换至 `Yes`.

在此页中输入以下信息（从数据库连接部分开始）：

* `Username`:的用户名 [!DNL MBI] MySQL用户
* `Password`:的密码 [!DNL MBI] MySQL用户
* `Port`:您服务器上的MySQL端口（默认为3306）
* `Host` 默认情况下，这将为localhost。 通常，它将是MySQL服务器的绑定地址值，默认情况下为 `127.0.0.1 (localhost)`，但也可能是一些本地网络地址(例如， `192.168.0.1`)或您服务器的公共IP地址。

   值可在 `my.cnf` 文件(通常位于 `/etc/my.cnf`) `\[mysqld\]`. 如果绑定地址行在该文件中被注释掉，则服务器将受到外部连接尝试的保护。

在 `SSH Connection` 部分：

* `Remote Address`:服务器的IP地址或主机名 [!DNL MBI] 会穿隧
* `Username`:的用户名 [!DNL MBI] SSH(Linux)用户
* `SSH Port`:服务器上的SSH端口（默认为22个）

就这样！ 完成后，单击 **[!UICONTROL Save & Test]** 以完成设置。

## 相关：

* [重新验证集成](https://support.magento.com/hc/en-us/articles/360016733151)
