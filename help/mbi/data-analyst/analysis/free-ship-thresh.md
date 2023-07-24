---
title: 免费配送阈值
description: 了解如何设置一个仪表板来跟踪免费配送阈值的性能。
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
role: Admin,  User
feature: Data Warehouse Manager, Dashboards, Reports
source-git-commit: 6bdbdbcc652d476fa2a22589ac99678d5855e6fe
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# 免运费

>[!NOTE]
>
>本主题包含有关使用原始架构和新架构的客户端的说明。 如果您拥有以下优势，那么您将使用新架构： `Data Warehouse Views` 部分在选择后可用 `Manage Data` 从主工具栏中。

本主题将演示如何设置功能板来跟踪免费配送阈值的性能。 此仪表板（如下所示）是A/B测试两个免费运输阈值的好方法。 例如，贵公司可能不确定您应以$50还是$100的价格提供免运费。 您应该对客户的两个随机子集执行A/B测试，并在中执行分析 [!DNL Commerce Intelligence].

在开始使用之前，您需要确定两个单独的时间段，在这些时间段中，您商店的免费配送阈值具有不同的值。

![](../../assets/free_shipping_threshold.png)

此分析包含 [高级计算列](../data-warehouse-mgr/adv-calc-columns.md).

## 计算列

如果您使用的是原始架构(例如，如果您没有 `Data Warehouse Views` 下的选项 `Manage Data` 菜单)，您希望联系支持团队以构建以下列。 在新架构上，这些列可以从 `Manage Data > Data Warehouse` 页面。 详细说明如下。

* **`sales_flat_order`** 表
   * 此计算会创建存储段，其增量相对于您的典型购物车大小。 这可以从增量开始，包括5、10、50、100

* **`Order subtotal (buckets)`** 原始架构：由分析师创建，作为您的一部分， `[FREE SHIPPING ANALYSIS]` 票证
* **`Order subtotal (buckets)`** 新架构：
   * 如上所述，此计算会创建存储段，存储段以相对于您的典型购物车大小的增量递增。 如果您有本机小计列，例如 `base_subtotal`，可用作此新列的基础。 如果没有，则它可以是计算列，不包含收入中的运费和折扣。

  >[!NOTE]
  >
  >“存储桶”的大小取决于适合您作为客户端的情况。 你可以从你的开始 `average order value` 并创建一些小于或大于该数量的存储段。 在查看下面的计算时，您会看到如何轻松复制部分查询、编辑查询以及创建其他存储段。 示例以50为增量完成。

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal`，或 `calculated column`， `Datatype`： `Integer`
   * [!UICONTROL Calculation]： `case when A >= 0 and A<=200 then 0 - 200`
时间 `A< 200` 和 `A <= 250` 则 `201 - 250`
时间 `A<251` 和 `A<= 300` 则 `251 - 300`
时间 `A<301` 和 `A<= 350` 则 `301 - 350`
时间 `A<351` 和 `A<=400` 则 `351 - 400`
时间 `A<401` 和 `A<=450` 则 `401 - 450`
否则“超过450”结束


## 量度

无新量度!!!

>[!NOTE]
>
>确保 [将所有新列作为维度添加到量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 然后再生成新报告。

## 报告

* **发运规则A的平均订单值**
   * [!UICONTROL Metric]: `Average order value`

* 量度 `A`： `Average Order Value`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **按发运规则A的分段小计列出的订单数**
   * [!UICONTROL Metric]: `Number of orders`

  >[!NOTE]
  >
  >你可以通过显示顶部来截断尾端 `X` `sorted by` `Order subtotal` （桶） `Show top/bottom`.

* 量度 `A`： `Number of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 
  [!UICONTROL Chart Type]: `Column`

* **按小计和装运规则A的订单百分比**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * 
     [！UICONTROL分组依据]: `Independent`
   * [!UICONTROL Formula]: `(A / B)`
   * 
     [!UICONTROL Format]: `%`

* 量度 `A`： `Number of orders by subtotal (hide)`
* 量度 `B`： `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 
  [!UICONTROL Chart Type]: `Line`

* **小计超过发运规则A的订单百分比**
   * [!UICONTROL Metric]: `Number of orders`
   * 
     [!UICONTROL Perspective]: `Cumulative`

   * [!UICONTROL Metric]: `Number of orders`
   * 
     [！UICONTROL分组依据]: `Independent`

   * [!UICONTROL Formula]: `1- (A / B)`
   * 
     [!UICONTROL Format]: `%`

* 量度 `A`： `Number of orders by subtotal`
* 量度 `B`： `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 
  [!UICONTROL Chart Type]: `Line`


对发运规则B和时间段，重复上述步骤和报告。

在编译所有报告后，您可以根据需要将报告组织在功能板上。 结果可能类似于此页面顶部的图像。
