---
title: 连接Google Analytics仓库
description: 了解如何跟踪访客使用网站的方式、哪些内容很有吸引力、访客在哪些地方退出等。
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# 连接 [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>需要 [管理员权限](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] 是互联网上使用最广泛的Web分析服务。 实施 [!DNL Google Analytics] 通过网站上的，您可以跟踪访客如何使用您的网站、哪些内容很有吸引力、访客在哪里退出等。 [!DNL Google Analytics Warehoused] 是与现有 [!DNL Google Analytics] 集成。 由于具有 [!DNL Google Analytics] data warehouse中的数据，与现有的实时馈送不同 [!DNL Google Analytics] 集成。 在 [!DNL MBI]与其他数据一起，将提高网站的整体健康性和可用性。

## GA Warehosed与实时集成之间的差异

主要区别在于存储了一个集成([!DNL Google Analytics Warehoused])，而另一个则不是([!DNL Google Analytics Live])。 对于 [!DNL Google Analytics Warehoused]，这允许对 [!DNL Google Analytics] 数据，并让您能够 [!DNL Google Analytics] 和其他数据源，以创建有洞察力的报表。

让我们看看 [!DNL Google Analytics] 广告营销活动，以展示从操作角度可以执行的操作。 假设您有多个不同名称的第4季度广告营销活动。 营销活动是特定营销计划的结果。 利用仓库数据，我们可以创建一个新列，以查找相关促销活动名称并返回 `Operation Dumbo`.

组合方面允许 [!DNL Google Analytics] 要连接到其他数据以进行分析的数据。 例如， `Total Time On Site By Ad Campaign` 数据 [!DNL Google Analytics] 加入到 `Total Spent Per Campaign` 数据 [!DNL Facebook Ads] 全面了解您的参与度花费。

使用 [!DNL Google Analytics Live] 另一方面， [!DNL Google Analytics] 图表就像一个小接收器，不会存储在您的 [!DNL MBI] data warehouse。

## 连接 [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] 是 `Premium` 集成。 [联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) 如果您有兴趣将此集成添加到订阅中。

1. 转到 `Connections` 页面下 **[!UICONTROL Admin** > **Integrations]**.
1. 单击 **[!UICONTROL Add a Add Integration]**，位于屏幕右侧。
1. 单击 [!DNL Google Analytics Warehoused] 图标。 这将打开 [!DNL Google Analytics] 凭据页面。
1. 输入 [!DNL Google Analytics] 凭据。 授权过程完成后，您将被重定向回 [!DNL MBI].
1. 将显示配置文件ID列表。 检查要连接的用户档案 [!DNL MBI]. 如果您有多个用户档案，并且需要一些帮助来确定哪个是用户档案，请参阅连接多个 [!DNL Google Analytics] 用户档案部分。

## 连接多个 [!DNL Google Analytics] 用户档案

您可能有多个网站连接到一个网站 [!DNL Google Analytics] 帐户，由其自己标识 [!DNL Google Analytics] 配置文件ID。 在这种情况下，您可以选择在 [!DNL MBI]. 只需检查要在用户档案选择步骤中包含的用户档案ID即可。

确定特定网站的 [!DNL Google Analytics] 配置文件ID:

1. 登录 [!DNL Google Analytics]
1. 转到特定网站的 [!DNL Google Analytics] 仪表板
1. 查看URL — 配置文件ID对应于以下8个数字 `p` 在行尾

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 断开连接 [!DNL Google Analytics Warehoused] 从 [!DNL MBI] {#disconnect}

1. 访问 [!DNL Google Analytics] [帐户设置](https://www.google.com/accounts/) 页面。
1. 在 `Security` ，然后单击 **[!UICONTROL edit]** 下一页 `Authorizing` 应用程序和站点。
1. 单击 **[!UICONTROL revoke access]** 下一页 [!DNL MBI].

## 相关文档

* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [连接 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [分析网站活动和客户转化率](../../analysis/web-act-cust-conversion.md)
* [使用跟踪用户获取数据 [!DNL Google Analytics] cookie](../../analysis/google-track-user-acq.md)
