---
title: 创建定性同类群组分析
description: 了解什么是定性同类群组，为什么您可能希望构建此分析，以及如何在Commerce Intelligence中创建此分析。
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# 创建 `Qualitative Cohort Analysis`

您知道如何 [!DNL Google Adwords] — 收购的客户群体与收购自有机搜索的客户相比，其液晶电视的播放量是否有所增加？ 你有没有想过要表演一部 `cohort` 是否在同一报告中对不同的客户区段进行并排分析？ 如果是，则 `qualitative cohort analysis` 帮助您回答这些问题。

本主题将深入探讨什么是定性同类群组，为什么您可能会对构建此分析感兴趣，以及如何在中创建此分析 [!DNL Commerce Intelligence].

## 什么是 `qualitative cohorts`反正呢？ {#whatare}

`Cohort` 分析通常可以宽泛地定义为分析在其生命周期内具有相似特征的用户组。 它允许您识别不同用户群组中的行为趋势。

请参阅 [同类群组分析](https://www.cohortanalysis.com/).

最多 `cohort` 分析 [!DNL Commerce Intelligence] 按公用日期将用户分组（例如，在指定月份首次购买的所有客户集）。 A `qualitative cohort` 稍有不同：它是一个由不基于时间的特性定义的用户组。 示例包括：

* 从广告营销活动获得的所有用户集
* 首次购买包含优惠券（或不包含优惠券）的所有用户集
* 属于某个年龄段的所有用户集

## 这跟正常情况有什么不同 `cohort` 生成器？ {#different}

此 [`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) 使用基于时间的特性为分组同类群组而优化。 这非常适合用于针对特定用户区段（例如，通过付费搜索促销活动获得的所有用户）进行分析。 在 `Cohort Analysis Builder`，您可以(1)专注于该特定用户组，以及(2) `cohort` 日期（如其首次订购日期）。

但是，如果要分析同一同类群组报表中多个用户区段的同类群组行为(`paid` 搜索与 `organic` 与直接流量相比，搜索更加先进，因此可以在以下位置构建分析： `Report Builder`.

## 我应该向支持人员发送哪些信息才能设置我的分析？ {#support}

创建 `qualitative cohort` 在中报告 `Report Builder` 涉及Adobe分析团队创建一些 [高级计算列](../data-warehouse-mgr/creating-calculated-columns.md) 在必要的表格上。

要构建这些库，请提交 [支持服务单](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) （请参考本文！）。 以下是您需要了解的信息：

* 此 `metric` 要使用及其使用的表执行同类群组分析(示例： `Revenue`，构建于 `orders` 表)。

* 此 `user segments` 您需要定义该信息在数据库中的存放位置(例如： `User's referral source`，本机 `users` ，并已重新定位到 `orders`)。

* 此 `cohort date` 希望您的分析使用(例如： `User's first order date` timestamp)。 通过此示例，我们将查看每个区段并询问 `How does a user's revenue grow in the months following their first order date?`.

* 此 `time interval` 您希望查看其分析的对象(例如： `weeks`， `months`，或 `quarters` 之后 `User's first order date`)。

一旦Adobe分析团队对上述内容做出响应，您就有了几个新的高级计算列来构建您的报表！ 然后，您可以按照以下说明执行此操作。

## 创建定性同类群组分析 {#create}

首先，您需要添加感兴趣的量度进行同类群组，逐个添加一次 `cohort` 你正在分析。 在本例中，您希望查看累积 `Revenue` 在客户首次订购后的几个月内完成，按照 `User's referral source`. 这意味着，您需要为每个区段添加一个 `Revenue` 特定区段的量度和过滤器：

![](../../assets/qualcohort1.gif)

其次，您应该对报表的时间选项进行两项更改：

1. 设置 `time interval` 到 `None`. 这是因为您最终将按时间间隔分组为维度，而不是使用常规的时间选项。

1. 设置 `time range` 到您希望报告涵盖的时间窗口。

在此示例中，您查看了 `all time` 视图 `Revenue`. 之后，您应该最终会看到一系列圆点：

![](../../assets/qualcohort2.gif)

第三，您可以调整以设置 `cohorts`. 基于 `cohort date` 和 `time interval` 您指定给Adobe分析师团队，您的帐户中有一个维度来执行 `cohort` 约会。 在此示例中，该自定义维度名为 `Months between this order and customer's first order date`. 使用此维度，您应：

* `Group by` 具有的维度 `group by` option

* 选择以下项的所有值： `dimension` 您感兴趣的内容

* 使用 `Show top/bottom option`，选择您感兴趣的前X个月，并按 `Months between this order and customer's first order date` 维度

现在，您可以为每个页面查看一行 `cohort` 你指定的那种。 立即查看示例 — 您会看到 `Revenue` 由每个反向链接源的用户参与， `grouped by` 首次订购与任何后续订购之间的间隔月数。 该示例还添加了 `Cumulative perspective` 以查看 `cohorts'` 总体增长 — 查看结果表以获得更多粒度。

这告诉我们什么？ 此处，指定反向链接来源 `Paid search` 在客户购买生命周期的第一个月很有价值，但无法通过重复收入保留其客户群。 同时 `Direct Traffic` 起点较低，其后几个月的收入实际以类似速度累积。

不管你如何挑选， `cohort` 分析是分析工具箱中的一个功能强大的工具。 此类分析可产生关于您的业务的一些有趣见解，这些见解 `time-based cohorts` 但也可能不会，这使您能够做出更好的数据驱动型决策。
