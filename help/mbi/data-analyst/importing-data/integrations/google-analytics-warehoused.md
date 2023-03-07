---
title: ConnectGoogle Analytics仓库
description: 了解如何跟踪访客如何使用您的网站、哪些内容有吸引力、访客的退出位置等。
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# Connect [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>需要 [管理员权限](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] 是Internet上使用最广泛的Web分析服务。 实施 [!DNL Google Analytics] 允许您跟踪访客如何使用您的网站、哪些内容有吸引力、访客的退出位置等。 [!DNL Google Analytics Warehoused] 是独立于您现有的集成 [!DNL Google Analytics] 集成。 由于具备以下特性，因此可更好地进行分析 [!DNL Google Analytics] data warehouse中的数据，这与现有 [!DNL Google Analytics] 集成。 在中分析这些指标 [!DNL MBI]与其他数据一起使用可提高网站的整体运行状况和可用性。

## GA仓库与实时集成的区别

主要区别在于存储了一个集成([!DNL Google Analytics Warehoused])，而另一个不是([!DNL Google Analytics Live])。 在 [!DNL Google Analytics Warehoused]，这允许对您的 [!DNL Google Analytics] 数据，并让您能够合并 [!DNL Google Analytics] 和其他数据源，以创建富有洞察力的报表。

查看 [!DNL Google Analytics] 广告营销活动，以从操作角度说明可执行的操作。 假设您在第4季度有多个名称不同的广告营销活动。 这些营销活动是特定营销计划的成果。 使用仓库数据，您可以创建一个列，以查找有问题的促销活动名称并返回第4季度计划名称 `Operation Dumbo`.

组合方面允许 [!DNL Google Analytics] 要与其他数据结合以执行分析的数据。 例如， take `Total Time On Site By Ad Campaign` 数据来源 [!DNL Google Analytics] 并加入进来 `Total Spent Per Campaign` 数据来源 [!DNL Facebook Ads] 以全面了解参与成本是多少。

使用 [!DNL Google Analytics Live] 另一方面，集成，每 [!DNL Google Analytics] 图表就像一个小容器，不会存储在 [!DNL MBI] data warehouse。

## 正在连接 [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] 是 `Premium` 集成。 [联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) 如果您有兴趣将此集成添加到订阅。

1. 转到 `Connections` 页面位于 **[!UICONTROL Admin** > **Integrations]**.
1. 单击 **[!UICONTROL Add an Integration]**，位于屏幕右侧。
1. 单击 [!DNL Google Analytics Warehoused] 图标。 这将打开 [!DNL Google Analytics] “身份证明”页。
1. 输入您的 [!DNL Google Analytics] 凭据。 授权过程完成后，您将被重定向回 [!DNL MBI].
1. 此时将显示配置文件ID列表。 检查要连接的配置文件 [!DNL MBI]. 如果您有多个配置文件，并且需要一些帮助来识别哪个配置文件是哪个，请参阅连接多个 [!DNL Google Analytics] 配置文件部分。

## 连接多个 [!DNL Google Analytics] 用户档案

您可能已将多个网站连接到一个 [!DNL Google Analytics] 帐户，由其自身标识 [!DNL Google Analytics] 配置文件ID。 在这种情况下，您可以选择将您的所有配置文件ID包含在 [!DNL MBI]. 检查要在用户档案选择步骤中包含的用户档案ID。

识别特定网站的 [!DNL Google Analytics] 配置文件ID：

1. 登录 [!DNL Google Analytics]
1. 前往特定网站的 [!DNL Google Analytics] 仪表板
1. 查看URL — 配置文件ID对应于以下八个数字 `p` 行尾

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 断开连接 [!DNL Google Analytics Warehoused] 起始日期 [!DNL MBI] {#disconnect}

1. 访问您的 [!DNL Google Analytics] [帐户设置](https://myaccount.google.com/intro) 页面。
1. 在 `Security` 部分，然后单击 **[!UICONTROL edit]** 旁边 `Authorizing` 应用程序和站点。
1. 单击 **[!UICONTROL revoke access]** 旁边 [!DNL MBI].

## 相关文档

* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [正在连接 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [分析网站活动和客户转化率](../../analysis/web-act-cust-conversion.md)
* [使用跟踪用户获取数据 [!DNL Google Analytics] Cookie](../../analysis/google-track-user-acq.md)
