---
title: 预期生命周期值(LTV)分析（基本）
description: 了解如何创建分析以了解当前客户的存留期值，并预测存留期值如何随着更多订单增加。
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# 预期生命周期值分析

预测客户下更多订单时的存留期价值是任何规模企业最重要的方面之一。

以下是创建分析以了解当前客户的存留期值，并预测存留期值如何随着更多订单增加而增加的步骤：

![预期生命周期值](../../assets/expected_ltv_720.png)

## 构建量度

第一步是通过以下步骤构建新量度：
* 导航到 **[!UICONTROL Manage Data > Metrics]**
   * 查看现有 **[!UICONTROL Avg lifetime revenue]**.

   >[!NOTE]
   >
   >构建此量度的表(可能 `customer_entity` 或 `sales_order` 取决于您的商店是否能够接受访客结帐。)。

   * 单击 **[!UICONTROL Create New Metric]** 并从上面选择表。
   * 此量度执行 **中间值** 在 `Customer's lifetime revenue` 列，排序方式 `created_at`.
      * [!UICONTROL Filters]:
         * 添加 `Customers we count (Saved Filter Set)` (或 `Registered accounts we count`)
   * 为量度命名，例如 `Median lifetime revenue`.



## 创建功能板

创建量度后，您可以 **创建功能板** 通过执行此操作：
* 导航到 **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* 为仪表板命名，例如 `Expected LTV`.

* 您可以在此处创建和添加所有报表。

## 生成报表

>[!NOTE]
>
>日期 **[!UICONTROL Time Period:]**，则每个报表的时段将列为 `All-time`. 您可以根据分析需求随意更改此设置。 Adobe建议该功能板上的所有报告都涵盖相同的时间段，例如 `All time`， `Year-to-date`，或 `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL间隔]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 添加 [!UICONTROL filters]：
         * [`A`] `Customer's group code` **不等于** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **大于**`0`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL间隔]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`


* **[!UICONTROL Average and Median LTV]**
   * 量度 `1`： `Avg lifetime revenue`
   * 量度 `2`： `Median lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * 
      [！UICONTROL图表类型]: `Line`
   * 取消选中 `Multiple Y-Axes`

* **按生命周期订单数列出的LTV**
   * 量度 `1`： `Avg lifetime revenue`
   * 量度 `2`： `New customers`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL间隔]: `None`
   * [!UICONTROL Group by]: `Customer's lifetime number of orders`
   * 

      [！UICONTROL图表类型]: `Line`
   >[!NOTE]
   >
   >不要添加的所有值 `Customer's lifetime number of orders`. 相反，看一下新客户数量达到较小数量时的情况，然后手动将每个客户的存留期订单数量值添加到该时间点。 例如，如果某订单有200个客户，其中两订单有75个，三订单有15个，四订单有3个，则添加 *1、2和3*.

* 添加现有 [!UICONTROL Avg customer lifetime revenue by cohort] 报告。

构建报表后，请参阅本主题顶部的图像，了解如何在功能板上组织报表。
