---
title: 连接Google Analytics仓库
description: 了解如何跟踪访客如何使用您的网站、哪些内容吸引人、访客的退出位置等。
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# 连接[!DNL Google Analytics Warehoused]

>[!NOTE]
>
>需要[管理员权限](../../../administrator/user-management/user-management.md)。

![Google Analytics徽标](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics]是Internet上使用最广泛的Web分析服务。 通过在您的网站上实施[!DNL Google Analytics]，您可以跟踪访客如何使用您的网站、哪些内容吸引人、访客的退出位置等。 [!DNL Google Analytics Warehoused]是独立于您现有[!DNL Google Analytics]集成的集成。 由于您的Data Warehouse中具有[!DNL Google Analytics]数据，这与现有[!DNL Google Analytics]集成的实时信息源不同，因此它允许更好地进行分析。 在[!DNL Commerce Intelligence]中连同其他数据一起分析这些量度，可提高网站的整体运行状况和可用性。

## GA仓库与实时集成的区别

主要区别在于存储了一个集成([!DNL Google Analytics Warehoused])，而另一个集成不是([!DNL Google Analytics Live])。 在[!DNL Google Analytics Warehoused]的情况下，这允许处理您的[!DNL Google Analytics]数据，并使您能够组合[!DNL Google Analytics]和其他数据源以创建富有洞察力的报表。

查看[!DNL Google Analytics]广告营销活动以了解从操作角度可以做些什么的示例。 假设您在第四季度有多个名称不同的广告营销活动。 这些营销活动是特定营销计划的结果。 使用仓库数据，您可以创建列以查找相关促销活动名称并返回第四季度计划名称`Operation Dumbo`。

组合方面允许将[!DNL Google Analytics]数据与其他数据连接以进行分析。 例如，获取`Total Time On Site By Ad Campaign`中的[!DNL Google Analytics]数据，并将其与来自`Total Spent Per Campaign`的[!DNL Facebook Ads]数据联接，以完整了解参与度对您造成的成本。

另一方面，使用[!DNL Google Analytics Live]集成，每个[!DNL Google Analytics]图表都像一个未存储在Data Warehouse中的小思洛存储器。

## 正在连接[!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused]是`Premium`集成。 如果您有兴趣将此集成添加到订阅，请[联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

1. 转到`Connections`下的&#x200B;**[!UICONTROL Admin** > **Integrations]**&#x200B;页面。
1. 单击右侧的&#x200B;**[!UICONTROL Add an Integration]**。
1. 单击[!DNL Google Analytics Warehoused]图标。 这将打开[!DNL Google Analytics]凭据页面。
1. 输入您的[!DNL Google Analytics]凭据。 授权过程完成后，您将被重定向回[!DNL Commerce Intelligence]。
1. 此时将显示配置文件ID列表。 检查要连接到[!DNL Commerce Intelligence]的配置文件。 如果您有多个配置文件并且需要帮助来识别哪个，请参阅下面的“连接多个[!DNL Google Analytics]配置文件”部分。

## 连接多个[!DNL Google Analytics]配置文件

您可能将多个网站连接到单个[!DNL Google Analytics]帐户，并使用其自己的[!DNL Google Analytics]配置文件ID进行标识。 在这种情况下，您可以选择在[!DNL Commerce Intelligence]中包含您的所有配置文件ID。 检查要在用户档案选择步骤中包含的用户档案ID。

要识别特定网站的[!DNL Google Analytics]配置文件ID，请执行以下操作：

1. 登录[!DNL Google Analytics]
1. 转到特定网站的[!DNL Google Analytics]仪表板
1. 查看URL — 配置文件ID对应于行末尾位于`p`后面的八个数字

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 正在断开[!DNL Google Analytics Warehoused]与[!DNL Commerce Intelligence]的连接 {#disconnect}

1. 访问您的[!DNL Google Analytics] [帐户设置](https://myaccount.google.com/intro)页面。
1. 在`Security`部分下，单击&#x200B;**[!UICONTROL edit]**&#x200B;应用程序和站点旁边的`Authorizing`。
1. 单击&#x200B;**[!UICONTROL revoke access]**&#x200B;旁边的[!DNL Commerce Intelligence]。

## 相关文档

* [正在重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [正在连接 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [分析网站活动和客户转化率](../../analysis/web-act-cust-conversion.md)
* [使用 [!DNL Google Analytics] Cookie跟踪用户获取数据](../../analysis/google-track-user-acq.md)
