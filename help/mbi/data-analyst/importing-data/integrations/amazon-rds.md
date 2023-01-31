---
title: 连接Amazon RDS
description: 了解连接RDS实例的步骤。
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# 连接Amazon RDS

Amazon关系数据库服务(RDS)是一种托管数据库服务，它在您可能已经熟悉的数据库引擎上运行 —  [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md), [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)和 [[!DNL PostgreSQ]](../integrations/postgresql.md).

连接RDS实例的步骤会因您所使用的数据库类型（使用上面的链接了解每个数据库的详细说明）以及您是否使用加密连接(如 [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md))，但以下是基础知识：

## 授权 [!DNL MBI] 访问数据库

在凭据页面(**[!UICONTROL Manage Data** > **Integrations]**)时，您将看到一个框，其中包含您需要授权才能将RDS连接到MBI的IP地址： `54.88.76.97` 和 `34.250.211.151`. 以下是 `MySQL credentials` 页面，其中突出显示了IP地址框：

![](../../../assets/RDS_IP.png)

对于 [!DNL MBI] 要成功连接您的RDS实例，您需要通过AWS管理控制台将这些IP地址添加到相应的数据库安全组。 这些IP地址可以添加到现有组，也可以创建新组 — 重要的是，组有权访问您要连接到的实例 [!DNL MBI].

添加 [!DNL MBI] IP地址，请确保在 `/32` 地址的结尾，以向Amazon表明它是确切的IP地址。 别担心；AWS界面将明确说明这是必需的。

## 创建 `Linux` 用户 [!DNL MBI] {#linux}

>[!NOTE]
>
>只有在使用加密连接时，才需要执行此步骤。 有关如何执行此操作的说明，请参阅您所使用的数据库的设置文章(例如：MySQL)。 的 `Linux` 用户将允许我们创建 `SSH tunnel`，这是通过Internet发送数据的最安全方法。

## 为MBI创建数据库用户

在此过程中，步骤会因您所使用的数据库而异。 不过，这个想法是相同的：您将为 [!DNL MBI] 用于访问数据库。 创建数据库的说明 [!DNL MBI] 用户可在您所使用的数据库的设置文章中找到。

## 在MBI中输入连接信息

在你同意 [!DNL MBI] 访问您的实例并为我们创建了用户，您最后需要做的就是在中输入连接信息 [!DNL MBI].

的凭据页面 `MySQL`, `Microsoft SQL`和 `PostgreSQL` 通过 `Integrations` 页面(**[!UICONTROL Manage Data** > **Integrations]**) **[!UICONTROL Add Integration]**. 显示集成列表时，单击用于您的数据库的图标以转到凭据页。 如果您当前没有访问所需集成的权限，请联系您的客户成功经理。

要完成创建连接，我们需要以下信息：

* RDS实例的公共地址：这可以在AWS管理控制台中找到。
* 数据库实例使用的端口：某些数据库具有默认端口，该端口将自动填充 `Port` 字段。 此信息也可在数据库的设置文档中找到。
* 您为创建的用户的用户名和密码 [!DNL MBI].

如果您使用的是加密连接，请更改 `Encrypted` 在“数据库凭据”页上打开 `Yes`. 这将显示用于设置加密的其他表单：

![](../../../assets/sql-integration-encrypted-yes.png)

这就是一切！ 连接RDS实例已完成。
