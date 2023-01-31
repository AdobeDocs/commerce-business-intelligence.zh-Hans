---
title: 创建定性同类群组分析
description: 了解什么是定性同类群组，为什么您可能有兴趣构建此分析，以及如何在中创建此分析 [!DNL MBI].
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# 创建 `Qualitative Cohort Analysis`

你知道 [!DNL Adwords]与通过自然搜索获得的客户相比，获得的客户区段的LTV增长率是多少？ 你有没有想过 `cohort` 是否在同一报表中并排分析不同的客户区段？ 如果是，则 `qualitative cohort analysis` 会帮助你回答这些问题。

在本文中，我们深入研究了定性同类群组是什么，为什么您可能有兴趣构建此分析，以及如何在中创建此分析 [!DNL MBI].

## 什么是 `qualitative cohorts`不管怎样？ {#whatare}

`Cohort` 一般而言，分析可以被广义地定义为对在其生命周期中具有相似特征的用户组的分析。 它允许您识别不同用户群组之间的行为趋势。

请参阅 [同类群组分析](https://www.cohortanalysis.com/)  — 我们在上面写了网站！

最多 `cohort` 分析 [!DNL MBI] 按共同日期（例如，在指定月份首次购买的所有客户的集合）将用户分组。 A `qualitative cohort` 有点不同：它是由非基于时间的特征定义的用户组。 一些示例包括：

* 从广告营销活动获取的所有用户集
* 首次购买时包含优惠券（或未包含优惠券）的所有用户集
* 特定年龄的所有用户集

## 这与正常情况有何不同 `cohort` 生成器？ {#different}

的 [`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) 针对使用基于时间的特征对同类群组进行分组而进行优化。 这非常适用于针对特定用户区段（例如，通过付费搜索促销活动获取的所有用户）进行分析。 在 `Cohort Analysis Builder`，您可以(1)专注于该特定用户组，以及(2) `cohort` 日期（如其首次订购日期）。

但是，如果要分析同一同类群组报表中多个用户区段的同类群组行为(`paid` 搜索与 `organic` 搜索与直接流量，可能是？)，可以在 `Report Builder`.

## 我应该向支持团队发送哪些信息来设置我的分析？ {#support}

创建 `qualitative cohort` 报表 `Report Builder` 我们的分析团队创建一些 [高级计算列](../data-warehouse-mgr/creating-calculated-columns.md) 在必要的表格上。

要构建这些库，请提交 [支持票证](../../guide-overview.md) （并参考本文！） 以下是我们需要了解的：

* 的 `metric` 您想要使用及其使用的表格(例如： `Revenue`，基于 `orders` 表)。

* 的 `user segments` 您希望定义该信息在数据库中的位置(例如：不同值 `User's referral source`，本机 `users` 桌子并放置到 `orders`)。

* 的 `cohort date` 您希望使用分析(例如：the `User's first order date` 时间戳)。 此示例将允许我们查看每个区段并询问 `How does a user's revenue grow in the months following their first order date?`.

* 的 `time interval` 要查看相关分析的信息(示例： `weeks`, `months`或 `quarters` 之后 `User's first order date`)。

一旦我们的分析团队对上述做出响应，您将拥有几个新的高级计算列来构建您的报表！ 然后，您将能够按照以下说明执行此操作。

## 创建定性同类群组分析 {#create}

首先，您需要为每个量度添加一次您感兴趣的同类群组 `cohort` 你在分析。 在本例中，我们希望查看累积 `Revenue` 在客户首次订购后的几个月内进行，由 `User's referral source`. 这意味着，对于每个区段，我们将添加一个 `Revenue` 特定区段的量度和过滤器：

![](../../assets/qualcohort1.gif)

其次，您应对报表的时间选项进行两项更改：

1. 设置 `time interval` to `None`. 这是因为我们最终会按时间间隔将分组为维度，而不是使用常规的时间选项。

1. 设置 `time range` 到您希望报表涵盖的时间范围。

在本例中，我们查看 `all time` 视图 `Revenue`. 在此之后，您应会获得一系列圆点：

![](../../assets/qualcohort2.gif)

第三，您将调整以实际设置 `cohorts`. 基于 `cohort date` 和 `time interval` 您为我们的分析团队指定的维度，您的帐户中将具有一个将执行 `cohort` 约会。 在此示例中，该自定义维度称为 `Months between this order and customer's first order date`. 使用此维度，您应：

* `Group by` 维度 `group by` 选项

* 选择 `dimension` 你感兴趣的地方

* 使用 `Show top/bottom option`，选择您感兴趣的前X个月，然后按 `Months between this order and customer's first order date` 维度

现在，您可以看到每个 `cohort` 你指定的。 请立即查看我们的示例 — 我们看到 `Revenue` 由每个反向链接来源的用户贡献， `grouped by` 首次订购与任何后续订购之间的月数。 我们还在 `Cumulative perspective` 查看 `cohorts'` 聚合增长 — 查看结果表以获取更多粒度。

这告诉我们什么？ 此处，具体的反向链接来源 `Paid search` 在客户购买生命周期的第一个月中非常有价值，但无法通过重复收入保留其客户基础。 While `Direct Traffic` 在开始时收入较低，随后几个月的收入实际上以类似的速度增长。

不管你怎么割， `cohort` 分析是分析工具箱中的一个强大工具。 此类分析可以产生一些关于您业务的非常有趣的洞察，这些洞察与传统 `time-based cohorts` 可能不会，这使您能够做出更好的数据驱动决策。
