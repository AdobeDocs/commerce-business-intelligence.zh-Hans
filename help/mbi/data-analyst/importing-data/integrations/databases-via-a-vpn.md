---
title: 通过VPN连接数据库
description: 了解如何通过VPN而不是SSH通道连接数据库。
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# 通过VPN连接数据库

虽然Adobe建议您使用`SSH tunnel`连接数据库，但也可以使用加密的`VPN`连接来确保安全。 `VPN`可用于您的任何数据库集成，为了简化操作，该过程与设置`SSH tunnel`的过程大致相同：

1. [创建 [!DNL Commerce Intelligence] 数据库用户](#database)
1. [创建 [!DNL Commerce Intelligence] VPN用户](#vpn)
1. [允许访问 [!DNL Commerce Intelligence] IP地址](#allowlist)
1. [在Commerce Intelligence中输入连接和VPN用户信息](#finish)

除了数据库身份证明之外，还必须为VPN用户输入身份证明以总结经验。 任何VPN用户均可工作，但Adobe建议您创建一个[!DNL Commerce Intelligence]用户，因为这样可以更轻松地跟踪您帐户上的用户。

## 正在为[!DNL Commerce Intelligence]创建数据库用户 {#database}

创建数据库用户的过程因您连接的数据库类型而异。 要查看每种数据库类型的说明，请单击下面的链接。

* [MICROSOFT SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## 正在为`VPN`创建[!DNL Commerce Intelligence]用户 {#vpn}

如前所述，任何有效的`VPN`用户均可工作 — 但Adobe建议仅创建供[!DNL Commerce Intelligence]使用的用户。

## 允许访问[!DNL Commerce Intelligence] IP地址 {#allowlist}

要使连接成功，必须将防火墙配置为允许从IP地址访问。 它们是`54.88.76.97`和`34.250.211.151`，但它也位于任何数据库集成的`credentials`页面上：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 正在将连接和`VPN`用户信息输入到[!DNL Commerce Intelligence] {#finish}

要完成工作，您需要在[!DNL Commerce Intelligence]中输入连接和用户信息。 是否使数据库`credentials`页面保持打开状态？ 如果不是，则转到&#x200B;**[!UICONTROL Manage Data** > **Connections]**。 单击&#x200B;**[!UICONTROL Add New Data Source]**，然后单击要连接的数据库的图标。 别忘了将`Encrypted`切换更改为`Yes`。

在此页面中输入以下信息，从`Database Connection`部分开始：

* `Username`： [!DNL Commerce Intelligence]数据库用户的用户名
* `Password`： [!DNL Commerce Intelligence]数据库用户的密码
* `Port`：您服务器上的数据库端口。 默认为：
   * `MicrosoftSQL`： `1433`
   * `MongoDB`： `27017`
   * `MySQL`： `3306`
   * `PostgreSQL`： `5432`
* `Host`：默认情况下，这是localhost `127.0.0.1`，但它也可以是服务器的公共IP地址或局域网地址。
* `Database Name (optional)`：如果只允许访问一个数据库（在数据库用户创建步骤中指定），请在此处输入该数据库的名称。

在`Encryption Connection`部分下：

* `Encryption Type`：将此项设置为`Cisco IPsec VPN`
* `Gateway Address`： VPN服务器的IP地址
* `Group Name`：用于组身份验证的组的名称
* `Group Secret`：与组对应的密码。
* `Username`： [!DNL Commerce Intelligence] `VPN`用户名
* `Password`： [!DNL Commerce Intelligence] `VPN`用户密码

完成后，单击&#x200B;**[!UICONTROL Save & Test]**&#x200B;以完成设置。
