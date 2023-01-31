---
title: 定义客户流失
description: 了解如何设置功能板，以帮助您定义事务型客户的流失率。
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
source-git-commit: 3557e6370fae637cd74550b2806847bebe61d5d3
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# 交易客户流失率

在本文中，我们将演示如何设置功能板，以帮助您定义事务型客户的流失率。

![](../../assets/churn-deashboard.png)

此分析包含 [高级计算列](../data-warehouse-mgr/adv-calc-columns.md).

## 计算列

要创建的列

* `customer_entity` 表
* `Customer's lifetime number of orders`
* 选择定义： `Count`
* 选择 [!UICONTROL table]: `sales_flat_order`
* 选择 [!UICONTROL column]: **`entity_id`**
* [!UICONTROL Path]:sales_flat_order.customer_id = customer_entity.entity.id
* [!UICONTROL Filter]:
* 我们计数的订单数

* `sales_flat_order` 表
* `Customer's lifetime number of orders`
* 选择定义：联接列
* 选择 [!UICONTROL table]: `customer_entity`
* 选择 [!UICONTROL column]: `Customer's lifetime number of orders`
* [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]: `Orders we count`

* `Seconds since created_at`
* 选择定义： `Age`
* 选择 [!UICONTROL column]: `created_at`

* **`Customer's order number`** 将由分析师创建，作为 **[定义流失]** 票
* **`Is customer's last order`** 将由分析师创建，作为 **[定义流失]** 票
* **`Seconds since previous order`** 将由分析师创建，作为 **[定义流失]** 票
* **`Months since order`** 将由分析师创建，作为 **[定义流失]** 票
* **`Months since previous order`** 将由分析师创建，作为 **[定义流失]** 票

## 量度

没有新量度！

>[!NOTE]
>
>确保 [将所有新列作为量度的维度添加到](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新报告之前。

## 报表

* **初始重复顺序概率**
* 量度A:所有重复订单
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 量度B:所有时间订单
* [!UICONTROL Metric]:订单数

* [!UICONTROL Formula]:初始重复顺序概率
* 
   [!UICONTROL公式]: `A/B`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart type]: `Scalar`

* **重复顺序概率自订单后给定月份**
* 量度A:按自上一订单以来的月份重复订单（隐藏）
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 量度B:自订单（隐藏）以来按月列出的最后订单数
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 量度C:所有时间重复的订单（隐藏）
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 

   [!UICONTROL组依据]: `Independent`

* 量度D:上次订单的所有时间（隐藏）
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 

   [!UICONTROL组依据]: `Independent`

* [!UICONTROL Formula]:初始重复顺序概率
* 
   [!UICONTROL公式]: `(C-A)/(C+D-A-B)`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Months since previous order`
* 显示top.bottom:前24个类别，按类别名称排序

* 

   [!UICONTROL Chart type]: `Line`

初始重复订单概率报表表示重复订单总数/订单总数。 每项订单都是重复订单的机会；重复顺序的数量是实际执行操作的次数。

我们使用的公式将简化为（X个月后发生的重复订单总数）/（至少X个月前的订单总数）。 它向我们显示，从历史上看，由于订单已过X个月，因此用户再次下单的可能性为Y%。

构建功能板后，我们最常收到的问题是：如何使用它确定流失阈值？

**这没有“一个正确的答案”。** 但是，我们建议找到折线与初始重复概率率的一半值交叉的点。 在这里，我们可以说“如果用户要重复下单，他们现在可能已经下单了。” 最终，目标是选择从“保留”工作切换到“重新激活”工作的合理阈值。

编译完所有报告后，您可以在功能板上根据需要组织报告。 最终结果可能与页面顶部的图像类似

如果您在构建此分析时遇到任何问题，或者只想与我们的专业服务团队接洽， [联系支持](../../guide-overview.md).
