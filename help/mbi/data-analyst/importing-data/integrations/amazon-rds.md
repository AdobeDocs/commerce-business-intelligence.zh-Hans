---
title: 连接Amazon RDS
description: 了解连接RDS实例的步骤。
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# Connect [!DNL Amazon RDS]

[!DNL Amazon Relational Database Services (RDS)] 是在您可能已经熟悉的数据库引擎上运行的托管数据库服务：

* [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)
* [[!DNL PostgreSQL]](../integrations/postgresql.md)

连接您的设备的步骤 [!DNL RDS] 实例会有所不同，具体取决于您使用的数据库类型以及是否使用加密连接(例如 [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md))，以下是基本信息。

## 授权 [!DNL Commerce Intelligence] 访问数据库

在凭据页面上(**[!UICONTROL Manage Data** > **Integrations]**)对于每个数据库，您会看到一个包含您必须授权才能连接的IP地址的框。[!DNL RDS] 到 [!DNL Commerce Intelligence]： `54.88.76.97` 和 `34.250.211.151`. 以下是 `MySQL credentials` 页面，在该页面中突出显示了IP地址框：

![](../../../assets/RDS_IP.png)

对象 [!DNL Commerce Intelligence] 以成功连接 [!DNL RDS] 实例中，您必须通过AWS管理控制台将这些IP地址添加到相应的数据库安全组。 可以将这些IP地址添加到现有组，也可以创建一个现有组 — 重要的是，该组有权访问您要连接的实例 [!DNL Commerce Intelligence].

添加 [!DNL Commerce Intelligence] IP地址，确保添加 `/32` 到地址的末尾，以指示 [!DNL Amazon] 即为一个精确的IP地址。 别担心；AWS界面明确说明了这是必需的。

## 创建 `Linux` 用户 [!DNL Commerce Intelligence] {#linux}

>[!NOTE]
>
>仅当使用加密连接时才需要执行此步骤。 有关如何执行此操作的说明，请参阅正在使用的数据库的设置主题（例如：MySQL）。 此 `Linux` 用户允许我们创建 `SSH tunnel`，这是通过Internet发送数据的最安全方法。

## 创建数据库用户 [!DNL Commerce Intelligence]

这是该过程的一部分，其中的步骤因您使用的数据库而异。 不过，您的想法是相同的，您为创建一个用户， [!DNL Commerce Intelligence] 用于访问数据库。 有关创建数据库的说明 [!DNL Commerce Intelligence] 用户可在正在使用的数据库的设置主题中找到。

## 将连接信息输入到 [!DNL Commerce Intelligence]

在您授予 [!DNL Commerce Intelligence] 访问您的实例并为我们创建了一个用户，您最后需要做的就是将连接信息输入到 [!DNL Commerce Intelligence].

的凭据页面 `MySQL`， `Microsoft SQL`、和 `PostgreSQL` 可通过 `Integrations` 页面(**[!UICONTROL Manage Data** > **Integrations]**)，方法是单击 **[!UICONTROL Add Integration]**. 显示集成列表后，单击用于转到“身份证明”页的数据库的图标。 如果您当前无权访问所需的集成，请联系您的Adobe客户团队。

要完成创建连接，您需要以下信息：

* RDS实例的公共地址：此地址可在 [!DNL AWS] 管理控制台。
* 数据库实例使用的端口：某些数据库具有默认端口，该端口会自动填充 `Port` 字段。 此信息还可在数据库的设置文档中找到。
* 您为其创建的用户的用户名和密码 [!DNL Commerce Intelligence].

如果您使用的是加密连接，请更改 `Encrypted` 将“数据库身份证明”页切换为 `Yes`. 这将显示一个用于设置加密的额外表单：

![](../../../assets/sql-integration-encrypted-yes.png)


