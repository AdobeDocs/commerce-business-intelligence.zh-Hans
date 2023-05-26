---
title: Report Builder中的公式
description: 了解如何在Report Builder中使用公式。
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# 中的公式 `Report Builder`

在 [`Report Builder`](../../tutorials/using-visual-report-builder.md)，您可以使用来创建功能强大的可视化图表， [定义的量度](../../data-user/reports/ess-manage-data-metrics.md) 在您的帐户中。 在公式中组合这些量度，可让您从数据获取更多见解。 本主题将深入探讨公式如何用于 `Report Builder`  — 让我们跳进去！

## 什么是 `formula`？ {#what}

在 `Report Builder`， a `formula` 只是基于某种数学逻辑的一个或多个量度的组合。 典型示例如下所示：

![](../../assets/formula-example.png)

在此示例中，您使用 `Number of orders metric (A)` 和 `Distinct buyers metric (B)`，目标是回答以下问题：我的买家每个月平均订购次数是多少？ 公式的参数为：

* `Definition`：在此，对输入量度应用数学。 在本例中，订单数除以不同的买方数可以得出平均订单数。 因此，定义为(A/B)。

* `Format`：您的公式是返回数字、时段还是货币金额？ 公式定义旁边是一个下拉列表，您可以使用它指定返回的格式。 在这种情况下，它是一个数字。

* `Miscellaneous`：公式的时间戳、分组、透视和过滤器均由其输入指标继承。 这里无事可做！

## 如何使用 `formulas` 我的报告里吗？ {#how}

既然您已介绍了基础知识，请查看一些示例。

### 示例：我想了解我的收入的哪个百分比可归因于首次订单。

![使用公式来查找首次订单的收入百分比](../../assets/first_time_orders.gif)

在此示例中，您使用了 `Revenue` 和 `Revenue (first time orders)` 量度。 通过将 `Revenue (first time orders)(B)` 量度依据 `Revenue metric (A)` 并将返回格式设置为 `Percent`，您可以找到首次订购可归因的收入百分比。

### 示例：我想知道在提供和不提供 `promo code`.

![使用公式来查找包含和不包含促销代码的每订单平均收入](../../assets/promo_code.gif)

在此示例中，您使用了 `Revenue` 和 `Number of orders` 量度。 这个问题的答案包括两个步骤 — 分隔 `Revenue (A)` 按 `Number of orders (B)` 并将返回格式设置为 `Currency`. 接下来，您仅允许公式结果(`Avg. Revenue per order`)，显示结果并按其分组 `Promo code`.

### 示例：我想了解新客户的UTM源的分布。

![使用公式查找新客户的UTM源的分配](../../assets/distro.gif)

找到此问题的答案需要几个步骤：

1. 首先，您添加了 `New Customers` 量度，然后按以下项分组 `utm_source - all`. 这是量度 `A`，或 `New Customers (grouped)`.

1. 接下来，您已复制 `New Customers (grouped)` 量度并将其设置为使用独立维度。 量度 `B` - `New customers (ungrouped)`  — 显示新客户的总数。

1. 隐藏这两个量度后，可将公式定义设置为 `A/B`. 这将 `New customers (grouped)` 按 `New Customers (ungrouped)`.

1. 接下来，将结果格式设置为 `Percent`.

在此示例中，您使用了 `Stacked Columns` 透视图，按月显示结果。 这样，我们就可以逐月比较新客户的分布。

## 总结 {#wrapup}

您是否注意到上述示例中公式的 `timestamp`， `groupings`， `perspectives`、和 `filters` 是否从其输入指标继承？ 请记住，公式可用于 `perspectives` 和 [独立时间选项](../../tutorials/time-options-visual-rpt-bldr.md){： target=&quot;_blank&quot;}，就像量度一样。

如果您对于在中使用公式还有其他任何疑问， `Report Builder`， [联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
