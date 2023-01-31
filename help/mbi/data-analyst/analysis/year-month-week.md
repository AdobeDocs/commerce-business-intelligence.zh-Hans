---
title: 每年、每月和每周报表
description: 了解如何轻松查看一段时间的趋势以及更改您可能想要比较的时间段的视角。
exl-id: 74cf11c3-7ce0-477f-9a28-9d782e5da3d9
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# 时间段的报告

>[!NOTE]
>
>本文包含使用原始架构和新架构的客户端的说明。 你在 [新架构](../../administrator/account-management/new-architecture.md) 如果您 _data warehouse视图_ 选择 `Manage Data` 中。

通过报表生成器，您可以轻松查看一段时间的趋势以及更改您要比较的时间段的透视。 在本文中，我们将演示如何设置功能板以更深入地了解，以便您能够针对逐周、逐月和逐年分析创建报表。

![](../../assets/Wow__mom__yoy.png)

在开始之前，您需要详细了解探索视角 [此处](../../tutorials/using-visual-report-builder.md) 以及独立的时间选项 [此处](../../tutorials/time-options-visual-rpt-bldr.md).

此分析包含 [高级计算列](../data-warehouse-mgr/adv-calc-columns.md).

## 计算列

* **`Sales_flat_order`** 表
* **原始架构：** 以下列将由分析师创建，作为 `[YoY WoW MoM ANALYSIS]` 票
* `created_at (month-day)`
* `created_at (month)`
* `created_at (day of the month)`
* `created_at (day of the week)`
* `created_at (hour of the day)`

* **新架构：** 下面列出了SQL，其中包含有关如何创建此计算的示例照片
   * `created_at (month-day)` [!UICONTROL Calculation]: **to_char(A， &#39;mm-dd&#39;)**
   * `created_at (month)` [!UICONTROL Calculation]: **to_char(A， &#39;mm-month&#39;)**
   * `created_at (day of the month)`&lt; [!UICONTROL Calculation]: **to_char(A， &#39;dd&#39;)**
   * `created_at (day of the week)` [!UICONTROL Calculation]: **to_char(A， &#39;d-Day&#39;)**
   * **`created_at (hour of the day)` [!UICONTROL Calculation]: **to_char(A， &#39;hh24&#39;)**

      ![](../../assets/new-arch-create-calc.png)

## 量度

无。

>[!NOTE]
>
>确保 [将所有新列作为量度的维度添加到](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 生成新报告之前。

## 报表

* **YoY图**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 years ago to 1 year ago`

   * [!UICONTROL Show top/bottom]:前100%按 **`created_at (month-day)`***

* 量度 `A`: `This year`
* 量度 `B`: `Last year`
* [!UICONTROL Time period]: `1 year ago to 0 years ago`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (month-day)`
* 
   [!UICONTROL Chart Type]: `Line`

* **MoM图**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * 时间选项： `Time range (Custom)`: `2 months ago to 1 month ago`

   * 显示顶部/底部：前100%按 **`created_at (day of month)`***

* 量度 `A`:本月*
* 量度 `B`:上个月*
* [!UICONTROL Time period]:1个月前到0个月前
* 
   [!UICONTROL Interval]: None
* [!UICONTROL Group by]: `created_at (day of month)`
* 
   [!UICONTROL Chart Type]: Line

* **WoW图**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 weeks ago to 1 week ago`

   * [!UICONTROL Show top/bottom]:前100%按 `created_at (day of week)`

* 量度 `A`: `This week`
* 量度 `B`: `Last week`
* [!UICONTROL Time period]: `1 week ago to 0 weeks ago`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (day of week)`
* 
   [!UICONTROL Chart Type]: `Line`

* **DoD图**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 days ago to 1 day ago`

   * [!UICONTROL Show top/bottom]:前100%按 `created_at (hour of day)`

* 量度 `A`: `Today`
* 量度B: `Yesterday`
* [!UICONTROL Time period]: `1 day ago to 0 days ago`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (hour of day)`
* 
   [!UICONTROL Chart Type]: `Line`

编译完所有报告后，您可以在功能板上根据需要组织报告。 最终结果可能与本页顶部的图像类似。
