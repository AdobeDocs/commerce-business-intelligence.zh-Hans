---
title: 预期生命周期值(LTV)分析（基本）
description: 了解如何创建分析以了解当前客户的生命周期值，以及预测生命周期值随更多订单而增加的情况。
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# 预期生命周期值分析

在客户下订单时预测客户的生命周期值是任何规模业务中最重要的方面之一。

下面是创建分析以了解当前客户的生命周期值，以及预测生命周期值随更多订单而增加的步骤：

![预期存留期值](../../assets/expected_ltv_720.png)

## 生成量度

第一步是通过以下步骤构建新量度：
* 导航到 **[!UICONTROL Manage Data > Metrics]**
   * 查看现有 **[!UICONTROL Avg lifetime revenue]**.

   >[!NOTE]
   >
   >此量度构建在的表(可能 `customer_entity` 或 `sales_order` 取决于您商店接受来宾结账的能力。)

   * 单击 **[!UICONTROL Create New Metric]** 并从上面选择表。
   * 此量度执行 **中间值** 在 `Customer's lifetime revenue` 列，排序依据 `created_at`.
      * [!UICONTROL Filters]:
         * 添加 `Customers we count (Saved Filter Set)` (或 `Registered accounts we count`)
   * 为量度命名，例如 `Median lifetime revenue`.



## 创建功能板

创建量度后，您可以 **创建功能板** 通过执行以下操作：
* 导航到 **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* 为功能板指定名称，例如 `Expected LTV`.

* 我们将在此处创建和添加所有报表。

## 生成报告

* 如果您尚未注册，请签出 [此视频](https://fast.wistia.net/embed/iframe/24zz7wmjrt) 关于使用**[!UICONTROL Visual Report Builder] 来构建图表、表和标量值。

>[!NOTE]
>
>开 **[!UICONTROL Time Period:]**，则每个报表的时间段将列为 `All-time`. 请随时更改此参数以满足您的分析需求。 我们建议此仪表板上的所有报表涵盖同一时间段，例如 `All time`, `Year-to-date`或 `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL间隔]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 添加 [!UICONTROL filters]:
         * [`A`] `Customer's group code` **不等于** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **大于**`0`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL间隔]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`


* **[!UICONTROL Average and Median LTV]**
   * 量度 `1`: `Avg lifetime revenue`
   * 量度 `2`: `Median lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * 
      [!UICONTROL图表类型]: `Line`
   * 取消选中 `Multiple Y-Axes`

* **按订单生命周期数的LTV**
   * 量度 `1`: `Avg lifetime revenue`
   * 量度 `2`: `New customers`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL间隔]: `None`
   * [!UICONTROL Group by]: `Customer's lifetime number of orders`
   * 

      [!UICONTROL图表类型]: `Line`
   >[!NOTE]
   >
   >请勿为 `Customer's lifetime number of orders`，而是查看新客户数量达到小数值的时间点，然后手动将每个客户的生命周期订单数量值添加到该点。 例如，如果一次订购有200个客户，其中75个客户是2个客户，15个客户是3个客户，3个客户是4个客户，则添加 *1、2和3*.

* 添加现有 [!UICONTROL Avg customer lifetime revenue by cohort] 报表。

构建报表后，请参阅本主题顶部的图像，了解如何在功能板上组织报表。
