---
title: 年度、月度和周报表
description: 了解如何轻松地查看一段时间的趋势，并更改您可能想要比较的时间段的视角。
exl-id: 74cf11c3-7ce0-477f-9a28-9d782e5da3d9
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# 在时间段内报告

>[!NOTE]
>
>本主题包含有关使用原始架构和新架构的客户端的说明。 如果从主工具栏中选择[!DNL Manage Data]后有&#x200B;[!DNL _Data Warehouse视图_]&#x200B;部分可用，则您位于[新架构](../../administrator/account-management/new-architecture.md)中。

Report Builder允许您轻松查看一段时间的趋势，并更改您可能希望比较的时间段的视角。 本主题将演示如何设置功能板以更深层次地创建，从而允许您创建逐周、逐月、逐年的报表。

![](../../assets/Wow__mom__yoy.png)

在开始之前，您应该查看更多详细信息[此处](../../tutorials/using-visual-report-builder.md)和独立的时间选项[此处](../../tutorials/time-options-visual-rpt-bldr.md)，以探索视角。

此分析包含[高级计算列](../data-warehouse-mgr/adv-calc-columns.md)。

## 计算列

* **`Sales_flat_order`**&#x200B;表
* **原始架构：**&#x200B;以下列由分析师创建，作为`[YoY WoW MoM ANALYSIS]`票证的一部分
* `created_at (month-day)`
* `created_at (month)`
* `created_at (day of the month)`
* `created_at (day of the week)`
* `created_at (hour of the day)`

* **新架构：** SQL如下所列，其中包含有关如何创建此计算的示例照片
   * `created_at (month-day)` [!UICONTROL Calculation]： **to_char(A， &#39;mm-dd&#39;)**
   * `created_at (month)` [!UICONTROL Calculation]： **to_char(A， &#39;mm-month&#39;)**
   * `created_at (day of the month)`&lt; [!UICONTROL Calculation]： **to_char(A， &#39;dd&#39;)**
   * `created_at (day of the week)` [!UICONTROL Calculation]： **to_char(A， &#39;d-Day&#39;)**
   * **`created_at (hour of the day)` [!UICONTROL Calculation]： **to_char(A， &#39;hh24&#39;)**
     ![](../../assets/new-arch-create-calc.png)

## 量度

无。

>[!NOTE]
>
>确保在生成新报告之前[将所有新列作为维度添加到量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md)。

## 报告

* **按年图表**
   * [!UICONTROL Metric]： `Number of orders`

   * [!UICONTROL Metric]： `Number of orders`
   * [!UICONTROL Time options]： `Time range (Custom)`： `2 years ago to 1 year ago`

   * [!UICONTROL Show top/bottom]：前100%按&#x200B;**`created_at (month-day)`**&#x200B;排序*

* 量度`A`： `This year`
* 量度`B`： `Last year`
* [!UICONTROL Time period]： `1 year ago to 0 years ago`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]： `created_at (month-day)`
* 
  [!UICONTROL Chart Type]: `Line`

* **MoM图表**
   * [!UICONTROL Metric]： `Number of orders`

   * [!UICONTROL Metric]： `Number of orders`
   * 时间选项： `Time range (Custom)`： `2 months ago to 1 month ago`

   * 显示前/后：前100%按&#x200B;**`created_at (day of month)`**&#x200B;排序*

* 量度`A`：本月*
* 量度`B`：上个月*
* [!UICONTROL Time period]：一个月前至0个月前
* 
  [!UICONTROL Interval]: None
* [!UICONTROL Group by]： `created_at (day of month)`
* 
  [!UICONTROL Chart Type]: Line

* **WoW图表**
   * [!UICONTROL Metric]： `Number of orders`

   * [!UICONTROL Metric]： `Number of orders`
   * [!UICONTROL Time options]： `Time range (Custom)`： `2 weeks ago to 1 week ago`

   * [!UICONTROL Show top/bottom]：前100%按`created_at (day of week)`排序

* 量度`A`： `This week`
* 量度`B`： `Last week`
* [!UICONTROL Time period]： `1 week ago to 0 weeks ago`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]： `created_at (day of week)`
* 
  [!UICONTROL Chart Type]: `Line`

* **DoD图表**
   * [!UICONTROL Metric]： `Number of orders`

   * [!UICONTROL Metric]： `Number of orders`
   * [!UICONTROL Time options]： `Time range (Custom)`： `2 days ago to 1 day ago`

   * [!UICONTROL Show top/bottom]：前100%按`created_at (hour of day)`排序

* 量度`A`： `Today`
* 指标B： `Yesterday`
* [!UICONTROL Time period]： `1 day ago to 0 days ago`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]： `created_at (hour of day)`
* 
  [!UICONTROL Chart Type]: `Line`

在编译所有报告后，您可以根据需要将报告组织在功能板上。 结果可能类似于此页面顶部的图像。
