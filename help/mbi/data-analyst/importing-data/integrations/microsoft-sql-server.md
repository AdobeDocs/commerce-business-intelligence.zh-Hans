---
title: 连接Microsoft SQL Server
description: 了解如何将Microsoft SQL数据库连接到 [!DNL MBI] 分四步进行。
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# 连接Microsoft SQL Server

>[!NOTE]
>
>需要 [管理员权限](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

本文介绍如何连接 `Microsoft SQL` 数据库到 [!DNL MBI] 分四步进行。 此过程需要一些与服务器连接和SQL相关的技术专业知识，并且可能需要团队开发人员的支持。

我们支持 [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure]，以及大多数其他云服务器提供程序。 如果你对你的主持人有疑问， [提交支持票证](../../../guide-overview.md) 要求我们提供这些信息。

我们的系统需要对您的数据库运行SELECT查询。 我们最初这样做是为了获取数据库结构的快照，然后定期加班以保持数据最新。 我们的更新是增量的，我们会限制更新频率和时间，以防止您服务器上出现任何不需要的负载。

实现此目的的最佳方法是，我们通过TCP/IP连接到数据库服务器。 为我们创建一个仅能运行SELECT查询的用户（或者，也只能从您指定的表中选择数据）。 您需要对要连接到的每个服务器执行此操作 [!DNL MBI].

## 连接 `Microsoft SQL` to [!DNL MBI]:

1. 确保您的服务器允许通过TCP/IP和混合模式身份验证进行连接。

1. 确保您的防火墙允许我们服务器的专用IP连接。

   您可以在 `Settings` 页面。

1. 创建一个用户，我们将使用该用户登录到您的数据库服务器。  你有两个选择；通过 `UI` 或通过 `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) （第二个示例）

1. 在 [!DNL MBI] 在 **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. 单击 **[!UICONTROL Add a Data Source]**.

1. 选择以连接 `Microsoft SQL` 数据库，并在新 `Connections` 页面。

   如果您使用 `Windows Azure`，则还必须指定数据库名称。
