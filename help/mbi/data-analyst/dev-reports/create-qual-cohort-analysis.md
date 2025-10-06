---
title: 创建定性同类群组分析
description: 了解什么是定性同类群组，为什么您可能希望构建此分析，以及如何在Commerce Intelligence中创建此分析。
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 0%

---

# 创建`Qualitative Cohort Analysis`

您知道与通过自然搜索获得的客户相比，您收购的[!DNL Google Adwords]客户区段的LTV增长情况吗？ 您是否曾考虑在同一报告中对不同的客户区段并排执行`cohort`分析？ 如果是这样的话，`qualitative cohort analysis`将帮助您回答这些问题。

本主题将深入探讨什么是定性同类群组，为什么您可能希望构建此分析，以及如何在[!DNL Commerce Intelligence]中创建此分析。

## 什么是`qualitative cohorts`？ {#whatare}

`Cohort`分析通常可以宽泛地定义为分析在其生命周期内具有相似特征的用户组。 它允许您识别不同用户群组中的行为趋势。

请参阅[同类群组分析](https://www.cohortanalysis.com/)。

`cohort`中的大多数[!DNL Commerce Intelligence]用户按共同日期一起进行分析（例如，在给定月份中首次购买的所有客户集）。 `qualitative cohort`稍有不同：它是一个由不基于时间的特性定义的用户组。 示例包括：

* 从广告营销活动获得的所有用户集
* 首次购买包含优惠券（或不包含优惠券）的所有用户集
* 属于某个年龄段的所有用户集

## 这跟常规的`cohort`生成器有何不同？ {#different}

[`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md)已针对使用基于时间的特征对同类群组进行了优化。 这非常适合用于针对特定用户区段（例如，通过付费搜索促销活动获得的所有用户）进行分析。 在`Cohort Analysis Builder`中，您可以(1)重点关注该特定用户组，以及(2)在某个日期（如其首次订购日期）上`cohort`。

但是，如果要分析同一同类群组报告中多个用户区段的同类群组行为（`paid`搜索与`organic`搜索对比，或者直接流量对比？），则可以在`Report Builder`中构建此更高级的分析。

## 我应该向支持人员发送哪些信息才能设置我的分析？ {#support}

在`qualitative cohort`中创建`Report Builder`报告涉及Adobe分析团队在必要的表中创建一些[高级计算列](../data-warehouse-mgr/creating-calculated-columns.md)。

要生成这些文件，请提交[支持票证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hans)（并引用此文章！）。 以下是您需要了解的信息：

* 您要使用执行同类群组分析的`metric`及其使用的表（示例： `Revenue`，基于`orders`表构建）。

* 您要定义的`user segments`以及该信息在数据库中的位置（例如： `User's referral source`的不同值，它在`users`表中本地并且被重新定位到`orders`）。

* 您希望您的分析使用的`cohort date`（示例： `User's first order date`时间戳）。 此示例将允许我们查看每个区段并询问`How does a user's revenue grow in the months following their first order date?`。

* 您希望查看分析的`time interval`（示例： `weeks`、`months`或`quarters`之后的`User's first order date`）。

Adobe分析团队对上述内容做出响应后，您就有了几个新的高级计算列来构建您的报表！ 然后，您可以按照以下说明执行此操作。

## 创建定性同类群组分析 {#create}

首先，您要添加感兴趣的量度进行同类群组，即为您正在分析的每个`cohort`添加一次。 在本例中，您希望查看客户在首次订购后的几个月内完成的累积`Revenue`，按`User's referral source`分段。 这意味着对于每个区段，您添加一个`Revenue`量度并为特定区段过滤：

![创建定性同类群组分析的动画演示](../../assets/qualcohort1.gif)

其次，您应该对报表的时间选项进行两项更改：

1. 将`time interval`设置为`None`。 这是因为您最终将按时间间隔分组为维度，而不是使用常规的时间选项。

1. 将`time range`设置为您希望报告涵盖的时间范围。

在此示例中，您查看了`all time`的`Revenue`视图。 之后，您应该最终会看到一系列圆点：

![同类群组分组和分析选项的动画演示](../../assets/qualcohort2.gif)

第三，您调整以设置`cohorts`。 根据您指定给Adobe分析团队的`cohort date`和`time interval`，您的帐户中有一个执行`cohort`约会的维度。 在此示例中，该自定义维度称为`Months between this order and customer's first order date`。 使用此维度，您应：

* `Group by`包含`group by`选项的维度

* 选择您感兴趣的`dimension`的所有值

* 使用`Show top/bottom option`，选择您感兴趣的前X个月，并按`Months between this order and customer's first order date`维度排序

现在，您可以看到为您指定的每个`cohort`显示一行。 立即查看示例 — 您会看到每个反向链接源的用户贡献的`Revenue`，`grouped by`他们的第一张订单与任何后续订单之间的月数之差。 该示例还添加了`Cumulative perspective`以查看`cohorts'`聚合增长 — 查看结果表以了解更多粒度。

这告诉我们什么？ 在此，特定反向链接源`Paid search`在客户购买生命周期的第一个月很有价值，但无法通过重复收入保留其客户群。 虽然`Direct Traffic`的开头金额较低，但随后几个月的收入实际以类似的速度累积。

无论您如何选择，`cohort`分析都是分析工具箱中一个功能强大的工具。 此类分析可产生一些传统`time-based cohorts`所无法提供的关于您的业务的有趣见解，从而使您能够做出更好的数据驱动型决策。
