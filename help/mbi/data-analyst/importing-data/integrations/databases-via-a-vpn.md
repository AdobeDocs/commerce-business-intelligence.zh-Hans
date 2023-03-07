---
title: 通过VPN连接数据库
description: 了解如何通过VPN而不是SSH通道连接数据库。
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 通过VPN连接数据库

虽然Adobe建议使用SSH通道连接数据库，但也可以使用加密的VPN连接来确保安全。 A `VPN` 可用于任何数据库集成，而且为了简化操作，此过程与设置 `SSH tunnel`：

1. [创建 [!DNL MBI] 数据库用户](#database)
1. [创建 [!DNL MBI] VPN用户](#vpn)
1. [允许访问 [!DNL MBI] IP地址](#allowlist)
1. [在MBI中输入连接和VPN用户信息](#finish)

除了数据库身份证明之外，还必须输入VPN用户的身份证明才能总结。 任何VPN用户均可工作，但Adobe建议您创建 [!DNL MBI] user — 使您能够更轻松地跟踪帐户中的用户。

## 创建数据库用户 [!DNL MBI] {#database}

创建数据库用户的过程因您连接的数据库类型而异。 要查看每种数据库类型的说明，请单击下面的链接。

* [Microsoft](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## 创建 `VPN` 用户 [!DNL MBI] {#vpn}

如前所述，任何有效 `VPN` 用户有效 — 但Adobe建议您仅为 [!DNL MBI] use.

## 允许访问 [!DNL MBI] IP地址 {#allowlist}

要使连接成功，必须将防火墙配置为允许从IP地址访问。 它们是 `54.88.76.97` 和 `34.250.211.151`，但它也位于 `credentials` 任何数据库集成的页面：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 输入连接和 `VPN` 用户信息进入 [!DNL MBI] {#finish}

要完成这些操作，您需要将连接和用户信息输入到 [!DNL MBI]. 您是否离开了数据库 `credentials` 是否打开页面？ 如果不能，请转到 **[!UICONTROL Manage Data** > **Connections]** 并单击 **[!UICONTROL Add New Data Source]**，则显示要连接的数据库的图标。 不要忘记更改 `Encrypted` 切换到 `Yes`.

在此页面中输入以下信息，从 `Database Connection` 部分：

* `Username`：的用户名 [!DNL MBI] 数据库用户
* `Password`：的密码 [!DNL MBI] 数据库用户
* `Port`：数据库在服务器上的端口。 默认值为：
* `MicrosoftSQL`: `1433`
* `MongoDB`: `27017`
* `MySQL`: `3306`
* `PostgreSQL`: `5432`
* `Host`：默认情况下，这是localhost `127.0.0.1`，但也可以是服务器的公共IP地址或局域网地址。
* `Database Name (optional)`：如果只允许访问一个数据库（在数据库用户创建步骤中指定），请在此处输入该数据库的名称。

在 `Encryption Connection` 部分：

* `Encryption Type`：将此项设置为 `Cisco IPsec VPN`
* `Gateway Address`：VPN服务器的IP地址
* `Group Name`：用于组身份验证的组的名称
* `Group Secret`：与组对应的密码。
* `Username`：此 [!DNL MBI] `VPN` 用户名
* `Password`：此 [!DNL MBI] `VPN` 用户密码

就是这样！ 完成后，单击 **[!UICONTROL Save & Test]** 以完成设置。
