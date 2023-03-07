---
title: 连接Microsoft&reg；&reg； SQL Server
description: 了解如何将Microsoft&reg； SQL数据库连接到 [!DNL MBI] 四个步骤。
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# 连接Microsoft® SQL Server

>[!NOTE]
>
>需要 [管理员权限](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

本文说明如何连接 `Microsoft SQL` 数据库至 [!DNL MBI] 四个步骤。 此过程需要一些与服务器连接和SQL相关的技术专业知识，并且可能需要团队开发人员的支持。

MBI支持 [!DNL Amazon RDS]， [!DNL EC2]， [!DNL Microsoft®; SQL Azure]和大多数其他云服务器提供商。 如果您对某个主机有疑问， [提交支持服务单](../../../guide-overview.md) 要求我们提供此信息

您的系统需要对数据库运行SELECT查询。 最初，这样做是为了获取数据库结构的快照，然后定期超时以保持数据最新。 您的更新是增量式的，Adobe会限制更新频率和时间，以防止服务器上出现任何不需要的负载。

最佳方法是我们通过TCP/IP连接到您的数据库服务器。 为我们创建一个只能运行SELECT查询的用户（并且，可选，只能从您指定的表中选择数据）。 必须为要连接的每个服务器执行此操作 [!DNL MBI].

## 正在连接 `Microsoft SQL` 到 [!DNL MBI]：

1. 确保您的服务器允许通过TCP/IP和混合模式身份验证进行连接。

1. 确保防火墙允许服务器的专用IP进行连接。

   您可以在的“连接”部分找到用于连接到服务器的IP地址。 `Settings` 页面。

1. 创建用于登录到数据库服务器的用户。 您有两个选项；或者通过 `UI` 或通过 `query`：
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) （第二个示例）

1. 在中输入服务器IP地址、用户名和密码 [!DNL MBI] 下 **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. 单击 **[!UICONTROL Add a Data Source]**.

1. 选择以连接 `Microsoft SQL` 数据库，并在新数据库中的字段中输入您的凭据 `Connections` 页面。

   如果您使用 `Windows Azure`，还必须指定数据库名称。
