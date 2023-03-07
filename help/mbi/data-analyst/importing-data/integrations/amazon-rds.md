---
title: 连接Amazon RDS
description: 了解连接RDS实例的步骤。
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# 连接Amazon RDS

Amazon Relational Database Services (RDS)是一种托管数据库服务，它运行在您可能已经熟悉的数据库引擎上 —  [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)， [[!DNL Microsoft® SQL]](../integrations/microsoft-sql-server.md)、和 [[!DNL PostgreSQ]](../integrations/postgresql.md).

连接RDS实例的步骤因所使用的数据库类型以及是否使用加密连接(如 [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md))，以下是基本信息：

## 授权 [!DNL MBI] 访问数据库

在凭据页面上(**[!UICONTROL Manage Data** > **Integrations]**)对于每个数据库，您会看到一个包含必须授权才能将RDS连接到MBI的IP地址的框： `54.88.76.97` 和 `34.250.211.151`. 以下是 `MySQL credentials` 页面，在该页面中突出显示了IP地址框：

![](../../../assets/RDS_IP.png)

对象 [!DNL MBI] 要成功连接到RDS实例，您必须通过AWS管理控制台将这些IP地址添加到相应的数据库安全组。 可以将这些IP地址添加到现有组，也可以创建一个现有组 — 重要的是，该组有权访问您要连接的实例 [!DNL MBI].

添加 [!DNL MBI] IP地址，确保添加 `/32` 到IP地址的末尾，以向Amazon表明它是精确的IP地址。 别担心；AWS界面明确说明了这是必需的。

## 创建 `Linux` 用户 [!DNL MBI] {#linux}

>[!NOTE]
>
>仅当使用加密连接时才需要执行此步骤。 有关如何执行此操作的说明，请参阅正在使用的数据库的设置文章（例如：MySQL）。 此 `Linux` 用户允许我们创建 `SSH tunnel`，这是通过Internet发送数据的最安全方法。

## 为MBI创建数据库用户

这是该过程的一部分，其中的步骤因您使用的数据库而异。 不过，其想法是相同的：您为创建一个用户， [!DNL MBI] 用于访问数据库。 有关创建数据库的说明 [!DNL MBI] 用户可在正在使用的数据库的设置文章中找到。

## 在MBI中输入连接信息

在您授予 [!DNL MBI] 访问您的实例并为我们创建了一个用户，您最后需要做的就是将连接信息输入到 [!DNL MBI].

的凭据页面 `MySQL`， `Microsoft SQL`、和 `PostgreSQL` 可通过 `Integrations` 页面(**[!UICONTROL Manage Data** > **Integrations]**)，方法是单击 **[!UICONTROL Add Integration]**. 显示集成列表后，单击用于转到“身份证明”页的数据库的图标。 如果您当前无权访问所需的集成，请联系您的Adobe客户团队。

要完成创建连接，您需要以下信息：

* RDS实例的公共地址：可在AWS管理控制台中找到它。
* 数据库实例使用的端口：某些数据库具有默认端口，该端口会自动填充 `Port` 字段。 此信息还可在数据库的设置文档中找到。
* 您为其创建的用户的用户名和密码 [!DNL MBI].

如果您使用的是加密连接，请更改 `Encrypted` 将“数据库身份证明”页切换为 `Yes`. 这将显示一个用于设置加密的额外表单：

![](../../../assets/sql-integration-encrypted-yes.png)

就这么多！ 连接RDS实例已完成。
