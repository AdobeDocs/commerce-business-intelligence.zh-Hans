---
title: 免费装运阈值
description: 了解如何设置功能板以跟踪免费送货阈值的性能。
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# 免运费

>[!NOTE]
>
>本文包含针对使用原始架构和新架构的客户端的说明。 如果在从主工具栏中选择“管理数据”后，“Data warehouse视图”部分可用，则您将处于新架构中。

在本文中，我们演示了如何设置仪表板，以跟踪免费送货阈值的性能。 下面显示的仪表板是A/B测试两个不同免费送货阈值的绝佳方法。 例如，您的公司可能不确定您应该以50美元还是100美元提供免费送货服务。 您应该对客户的两个随机子集执行A/B测试，并在 [!DNL MBI].

在开始之前，您需要确定两个不同的时间段，其中您对商店的免费装运阈值具有不同的值。

![](../../assets/free_shipping_threshold.png)

此分析包含 [高级计算列](../data-warehouse-mgr/adv-calc-columns.md).

## 计算列

如果您位于原始架构上(例如，如果您没有 `Data Warehouse Views` 选项 `Manage Data` 菜单)，则需要联系我们的支持团队以构建以下列。 在新架构上，可以通过 `Manage Data > Data Warehouse` 页面。 详细说明如下。

* **`sales_flat_order`** 表
   * 此计算会创建相对于典型购物车大小的分段。 此值可以从以下增量中进行：包括、5、10、50、100

* **`Order subtotal (buckets)`** 原始架构：将由分析师创建，作为 `[FREE SHIPPING ANALYSIS]` 票
* **`Order subtotal (buckets)`** 新架构：
   * 如上所述，此计算会创建相对于典型购物车大小的分段。 如果您有本机小计列，例如 `base_subtotal`，可用作此新列的基础。 如果没有，则可以是从收入中排除运费和折扣的计算列。
   >[!NOTE]
   >
   >“存储段”的大小取决于您作为客户端的适当内容。 你可以从 `average order value` 并创建一定数量的存储段，这些存储段小于或大于该数量。 查看下面的计算时，您将看到如何轻松复制部分查询、编辑查询以及创建其他存储段。 此示例以50为增量完成。

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal`或 `calculated column`, `Datatype`: `Integer`
   * [!UICONTROL Calculation]: `case when A >= 0 and A<=200 then 0 - 200`
何时 `A< 200` 和 `A <= 250` then `201 - 250`
when `A<251` 和 `A<= 300` then `251 - 300`
when `A<301` 和 `A<= 350` then `301 - 350`
when `A<351` 和 `A<=400` then `351 - 400`
when `A<401` 和 `A<=450` then `401 - 450`
else &#39;over 450&#39;结束



## 量度

无新量度!!!

>[!NOTE]
>
>确保 [将所有新列作为量度的维度添加到](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新报告之前。

## 报表

* **发运规则A的平均订单值**
   * [!UICONTROL Metric]: `Average order value`

* 量度 `A`: `Average Order Value`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **按装运规则A的小计时段划分的订单数**
   * [!UICONTROL Metric]: `Number of orders`

   >[!NOTE]
   >
   >您可以通过显示顶部 `X` `sorted by` `Order subtotal` （分段） `Show top/bottom`.

* 量度 `A`: `Number of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Column`

* **按小计和发运规则A列出的订单百分比**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * 
      [!UICONTROL组依据]: `Independent`
   * [!UICONTROL Formula]: `(A / B)`
   * 

      [!UICONTROL Format]: `%`

* 量度 `A`: `Number of orders by subtotal (hide)`
* 量度 `B`: `Total number of orders (hide)`
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

      [!UICONTROL组依据]: `Independent`

   * [!UICONTROL Formula]: `1- (A / B)`
   * 

      [!UICONTROL Format]: `%`

* 量度 `A`: `Number of orders by subtotal`
* 量度 `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Line`


对发运规则B的上述步骤和报表以及发运规则B的时间段重复执行上述步骤和报表。

编译完所有报告后，您可以在功能板上根据需要组织报告。 最终结果可能与本页顶部的图像类似。
