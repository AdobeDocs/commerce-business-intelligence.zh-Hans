---
title: Report Builder中的公式
description: 了解如何在Report Builder中使用公式。
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---

# 中的公式 `Report Builder`

在 [`Report Builder`](../../tutorials/using-visual-report-builder.md)，您可以使用 [定义量度](../../data-user/reports/ess-manage-data-metrics.md) 在您的帐户中。 通过将这些量度组合到公式中，可从数据中获得更多分析。 在本文中，我们将深入探讨如何在 `Report Builder`  — 让我们跳进去！

## 什么是 `formula`? {#what}

在 `Report Builder`, a `formula` 只是基于某些数学逻辑的一个或多个量度的组合。 典型示例如下所示：

![](../../assets/formula-example.png)

在本例中，我们使用 `Number of orders metric (A)` 和 `Distinct buyers metric (B)`，我们的目标是回答以下问题：我的买家每月的平均订单数是多少？ 公式的参数为：

* `Definition`:在此，对输入量度应用数学。 在本例中，将订单数除以不同购买者数量将告诉我们平均订单数。 因此，定义为(A/B)。

* `Format`:您的公式是返回数字、时间段还是货币金额？ 公式定义旁有一个下拉列表，您可以使用它指定返回的格式。 在这种情况下，它是一个数字。

* `Miscellaneous`:公式的时间戳、分组、透视图和过滤器都由其输入量度继承。 这里没什么可做的！

## 如何使用 `formulas` 在我的报告里？ {#how}

现在，我们已经介绍了基础知识，接下来我们来看一下一些示例。

### 示例：我想知道，我的收入中有多少百分比可以归因于第一次订购。

![使用公式查找归因于首次订购的收入百分比](../../assets/first_time_orders.gif)

在本例中，我们使用 `Revenue` 和 `Revenue (first time orders)` 量度。 通过将 `Revenue (first time orders)(B)` 量度 `Revenue metric (A)` 并将返回格式设置为 `Percent`，我们可以找到可归因于首次订购的收入百分比。

### 示例：我想知道，在提供和不提供 `promo code`.

![使用公式查找包含和不包含促销代码的每订单平均收入](../../assets/promo_code.gif)

在本例中，我们使用 `Revenue` 和 `Number of orders` 量度。 这个问题的答案包括两个步骤： `Revenue (A)` 按 `Number of orders (B)` 并将返回格式设置为 `Currency`. 接下来，我们仅允许公式结果(`Avg. Revenue per order`)显示结果并按 `Promo code`.

### 示例：我想了解新客户UTM源的分布情况。

![使用公式查找新客户UTM源的分布](../../assets/distro.gif)

要找到此问题的答案，需要执行以下步骤：

1. 首先，我们在 `New Customers` 量度，然后按 `utm_source - all`. 这是量度 `A`或 `New Customers (grouped)`.

1. 接下来，我们复制了 `New Customers (grouped)` 量度并将其设置为使用独立维度。 量度 `B` - `New customers (ungrouped)`  — 显示新客户的总数。

1. 隐藏两个量度后，我们会将公式定义设置为 `A/B`. 这将 `New customers (grouped)` 按 `New Customers (ungrouped)`.

1. 接下来，我们将结果格式设置为 `Percent`.

在本例中，我们使用 `Stacked Columns` 透视图，以按月显示结果。 这样，我们便可以每月比较新客户的分布情况。

## 包装 {#wrapup}

在上面的示例中，您是否注意到 `timestamp`, `groupings`, `perspectives`和 `filters` 是否从其输入量度中继承？ 请记住，可以利用公式来使用 `perspectives` 和 [独立时间选项](../../tutorials/time-options-visual-rpt-bldr.md){:target=&quot;_blank&quot;}，与量度可以一样。

如果您对在 `Report Builder`, [联系支持](../../guide-overview.md).
