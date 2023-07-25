---
title: 连接Google Analytics
description: 了解如何连接Google Analytics [!DNL Commerce Intelligence].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Connect [!DNL Google Analytics]

>[!NOTE]
>
>需要 [管理员权限](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] 是Internet上使用最广泛的Web分析服务。 实施 [!DNL Google Analytics] 允许您跟踪访客如何使用您的网站、哪些内容有吸引力、访客的退出位置等。 在中分析这些指标 [!DNL Commerce Intelligence]与其他数据一起使用可提高网站的整体运行状况和可用性。

通过输入您的 [!DNL Google Analytics] 凭据进入 [!DNL Commerce Intelligence]：

1. 转到 **[!UICONTROL Manage Data** > **Integrations]**.

1. 单击 **[!UICONTROL Add Integration]**，位于屏幕右侧。

1. 单击 [!DNL Google Analytics] 图标。 这将打开 [!DNL Google Analytics] “身份证明”页。

1. 输入您的 [!DNL Google Analytics] 凭据。 授权过程完成后，您将被重定向回 [!DNL Commerce Intelligence].

1. 此时将显示配置文件ID列表。 检查要连接的配置文件 [!DNL Commerce Intelligence]. 如果您有多个配置文件，并且需要一些帮助来识别哪个配置文件是哪个，请参阅连接多个 [!DNL Google Analytics] 配置文件部分。

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. 更改会自动保存，因此请单击 **返回连接** 等你完事了。

## 连接多个 [!DNL Google Analytics] 用户档案

您可能已将多个网站连接到一个 [!DNL Google Analytics] 帐户，由其自身标识 [!DNL Google Analytics] 配置文件ID。 在这种情况下，您可以选择将您的所有配置文件ID包含在 [!DNL Commerce Intelligence]. 检查要在用户档案选择步骤中包含的用户档案ID。

识别特定网站的 [!DNL Google Analytics] 配置文件ID：

1. 登录 [!DNL Google Analytics]
1. 前往特定网站的 [!DNL Google Analytics] 仪表板
1. 查看URL — 配置文件ID对应于以下八个数字 `p` 行末：

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 断开连接 [!DNL Google Analytics] 起始日期 [!DNL Commerce Intelligence] {#disconnect}

1. 访问您的 [!DNL Google Analytics] [帐户设置](https://accounts.google.com/) 页面。
1. 在 `Security` 部分，然后单击 **[!UICONTROL edit]** 旁边 `Authorizing` 应用程序和站点。
1. 单击 **[!UICONTROL revoke access]** 旁边 [!DNL Commerce Intelligence].

## 相关：

* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [正在连接 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [分析网站活动和客户转化率](../../analysis/web-act-cust-conversion.md)
* [使用跟踪用户获取数据 [!DNL Google Analytics] Cookie](../../analysis/google-track-user-acq.md)
