---
title: 首次购买报告的平均时间
description: 了解如何使用平均首次购买时间报表。
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 330832e2668024b00edb2b7c49b92bb042bd004a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 首次购买报告的平均时间

许多Adobe客户都有一个名为的量度和图表 `Average time to first purchase`，显示一组用户注册日期与首次购买日期之间的平均时间。 随着时间越来越接近现在，数据几乎总是会向下倾斜。

![首次订购的平均时间](../../assets/average-time-to-first-order.png)

这是因为这些较新的客户还没有机会生成从加入日期起超过一个月的任何购买。 由于从未购买过产品的用户根本不会包括在内（直到他们真的购买产品），因此这会使较新客户群的平均购买量出现下调。

还有其他几种可能的方法来看待这个指标，它们引入的偏见较少。 浏览一个示例。

## 示例：执行 `cohort` 一阶分析

您可能会在您的 `Users` 仪表板已命名 `Time to first order cohort`. 此报表使用 `Distinct buyers` 量度，用户分组依据 `cohort` 注册的周或月，并显示比率(介于 `0` 和 `1`)注册后几周或几个月内首次购买的用户。

图表可能显示，对于2014年12月注册的用户， `0.56` (或 `56%`)在第2个月（例如，2015年1月）前进行了第一次订购。

此同类群组分析可很好地指示一段时间内用户激活率。 如果此图表开始扁平化或停滞不前，并且您仍未接近完全转化为购买者，则可能是时候通过电子邮件促销活动激活其余用户了。
