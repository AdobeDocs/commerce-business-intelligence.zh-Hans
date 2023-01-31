---
title: 分析网站活动和客户转化率
description: 了解如何设置功能板来跟踪您的网站活动（包括页面查看、会话和用户），以及客户在一段时间内的转化率。
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# 分析网站活动

[!DNL MBI] 使您能够轻松地将广告成本数据与其余数据相集成。 这不仅可以让您了解您的网站活动，还可让您确定您网站上成为注册用户或购买产品的访客百分比。

在本文中，我们演示了如何设置功能板来跟踪您的网站活动（包括页面查看次数、会话数和用户数），以及客户在一段时间内的转化率。

## 先决条件

**导入广告成本数据**  — 连接 [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) to [!DNL MBI]  — 此操作将自动同步 [!DNL AdWords] 花在BI上。

**跟踪用户获取渠道数据**  — 将 [!DNL Google AdWords] 数据到数据库中特定订单，我们需要 [跟踪用户获取](../analysis/google-track-user-acq.md) 通过 [!DNL Google Analytics E-commerce]，允许我们使用utm源和介质连接每个订单。

## 用户获取促销活动

此报表集合是使用以下方法构建的：

* 在您连接 [!DNL Google AdWords] 数据
* 您的帐户中应已有的基本量度，例如 `Number of orders` 和 `New users`
* Dimension [!DNL Google Analytics Ecommerce] 数据到数据库，如订单的utm源和订单的utm介质。 如果您的帐户中当前不提供这些字段，请联系我们的支持团队

## 构建报告

**首先，创建一个报表，其中显示一段时间内页面查看次数、会话数和用户数：**

1. 创建新报表。
1. 单击 **[!UICONTROL Add Metric]**，然后将鼠标悬停在 [!DNL Google Analytics] 部分，然后选择 `Page Views`.
1. 添加其他量度，再次将鼠标悬停在 [!DNL Google Analytics] 部分，此时选择 `Sessions`.
1. 添加第三个量度，再次将鼠标悬停在 [!DNL Google Analytics] 部分，此时选择 `Users`.
1. 现在，将您的时间段从31天前更改为1天前的移动范围，并将时间间隔调整为 `by day`.
1. 为您的报表提供一个名称(例如， `Page views, sessions and users by day`)，然后单击 **[!UICONTROL Save]**.

**我们的第二份报告将介绍过去一年的页面查看次数：**

1. 创建新报表。
1. 单击 **[!UICONTROL Add Metric]**，将鼠标悬停在 [!DNL Google Analytics] 部分，然后选择 _页面查看次数_.
1. 将您的时间段从13个月前更改为1个月前的移动范围，并将时间间隔调整为 `by month`.
1. 为您的报表命名，如 `Page views by month,` ，然后单击 **[!UICONTROL Save]**.

**第三个图表将查看过去一年的跳出率：**

1. 创建新报表。
1. 单击 **[!UICONTROL Add Metric]**，将鼠标悬停在 [!DNL Google Analytics] 部分，然后选择 _跳出率_.
1. 将您的时间段从13个月前更改为1个月前的移动范围，并将时间间隔调整为 `by month`.
1. 为您的报表命名，如 `Bounce rate by month`，然后单击 **[!UICONTROL Save]**.

**现在，查看新访客与回访访客的平均会话时长：**

1. 创建新报表。
1. 单击 **UICONTROL添加量度**，将鼠标悬停在 [!DNL Google Analytics] 部分，然后选择 `Average Session Length`.
1. 将您的时间段从13个月前更改为1个月前的移动范围，并将时间间隔调整为 `by month`?
1. 添加 `Group by` 选择 `New or returning visitor`.  检查 `Show All` 框；然后单击 **[!UICONTROL Apply]**.
1. 为您的报表命名，如 `Average session length`，然后单击 **[!UICONTROL Save]**.

**接下来，请查看您过去30天内的热门反向链接域名：**

1. 创建新报表。
1. 单击 **[!UICONTROL Add Metric]**，将鼠标悬停在 [!DNL Google Analytics] 部分，然后选择 `Sessions`.
1. 将您的时间段从31天前更改为1天前的移动范围，并将时间间隔调整为 `none`.
1. 添加 `Group by` 选择 `ga:source`.  检查 _显示全部_ 框；然后单击 **[!UICONTROL Apply]**.
1. 添加其他 `group by` 选择 `ga:medium`. 再次，检查 `Show All` 框；然后单击 **[!UICONTROL Apply]**.
1. 为您的报表命名，如 `Top 20 Referring Domains, 30 Days`，然后单击 **[!UICONTROL Save]**.

**最后，请查看转化情况：**

1. 创建新报表。
1. 添加以下量度：

* `New users`
   * 单击 **[!UICONTROL Hide]** 在量度名称下方

* `Number of orders`
   * 添加过滤器 `Customer's order number` = 1，单击 **[!UICONTROL Apply]**
   * 单击量度名称并调用以重命名量度 `Number of first orders`，然后单击 **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** 量度

* `Users`
   * **[!UICONTROL Hide]** 量度
   * 将时间段更改为 `24 months ago to now`，并将时间间隔调整为 `by month`.
   * 通过单击 **[!UICONTROL Formula]**.
   * A/D，然后单击 **[!UICONTROL Apply]**
   * 重命名公式 `Registration conversion`
   * B/D，然后单击 **[!UICONTROL Apply]**
   * 重命名公式 `First order conversion`
   * C/D，然后单击 **[!UICONTROL Apply]**
   * 重命名公式 `Any order conversion`

* 现在给你的报告取个名字，比如 `Conversion by month`，然后单击 **[!UICONTROL Save]**.

## 后续步骤

既然您可以访问Web流量和转化率上的数据，那么您就可以开始挖掘这些数据来推动业务决策。 哪些网站最能增加您网站的流量？  哪些促销活动在吸引具有高生命周期价值的客户方面最有效？

在调整广告支出和营销策略时，您可以继续跟踪 [!DNL MBI]，在此功能板上进行迭代，以满足您公司不断演变的优先级。
