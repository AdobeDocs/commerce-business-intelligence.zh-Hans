---
title: 优惠券代码分析（基本）
description: 了解业务的优惠券表现对于细分您的订单和更好地了解客户习惯是一种有趣的方式。
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# 基本优惠券代码分析

了解业务的优惠券表现对于细分您的订单和更好地了解客户习惯是一种有趣的方式。

本文记录创建此分析所需的步骤，以便了解获得优惠券的客户表现、查看趋势并跟踪各个优惠券代码的使用情况。

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## 快速入门

首先，介绍如何跟踪优惠券代码。 如果客户将优惠券应用于订单，则会发生以下三种情况：

* 折扣反映在 `base_grand_total` 金额(您的 `Revenue` 量度（以MBI为单位）
* 优惠券代码存储在 `coupon_code` 字段。 如果此字段为NULL （空），则订单没有与其关联的优惠券。
* 折扣金额存储在 `base_discount_amount`. 根据您的配置，此值可能显示为负值或正值。

## 构建量度

第一步是通过以下步骤构建新量度：

* 导航到 **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* 选择 `sales_order`.
* 此量度执行 **总和** 在 **base_discount_amount** 列，排序方式 **created_at**.
   * [!UICONTROL Filters]:
      * 添加 `Orders we count` （保存的筛选器集）
      * 添加以下内容：
         * `coupon_code`**不是**`[NULL]`
      * 为量度命名，例如 `Coupon discount amount`.

## 创建功能板

* 创建量度后：
   * 导航到 [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**。
   * 为仪表板命名，例如 `_Coupon Analysis_`.

* 您可以在此处创建和添加所有报表。

## 生成报表

* **新报告：**

>[!NOTE]
>
>此 [!UICONTROL Time Period]每个报表的**列为 `All-time`. 您可以根据分析需求随意更改此设置。 Adobe建议该功能板上的所有报告都涵盖相同的时间段，例如 `All time`， `Year-to-date`，或 `Last 365 days`.

* **含优惠券的订单**
   * 
      [！UICONTROL量度]: `Orders`
      * 添加筛选器：
         * [`A`] `coupon_code` **不是** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL间隔]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **无优惠券的订单**
   * 
      [！UICONTROL量度]: `Orders`
      * 添加筛选器：
         * [`A`] `coupon_code` **是** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL间隔]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **带有优惠券的订单的净收入**
   * 
      [！UICONTROL量度]: `Revenue`
      * 添加筛选器：
         * [`A`] `coupon_code` **不是** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL间隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **优惠券折扣**
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL间隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **平均生命周期收入：获得优惠券的客户**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 添加筛选器：
         * [`A`] `Customer's first order's coupon_code` **不是** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL间隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **平均期限收入：非优惠券收购客户**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 添加筛选器：
         * [A] `Customer's first order's coupon_code` **是**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL间隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **优惠券使用情况详细信息（首次订购）**
   * 量度 `1`： `Orders`
      * 添加筛选器：
         * [`A`] `coupon_code` **不是**`[NULL]`
         * [`B`] `Customer's order number` **等于** `1`
   * 量度 `2`： `Revenue`
      * 添加筛选器：
         * [`A`] `coupon_code` **不是**`[NULL]`
         * [`B`] `Customer's order number` **等于** `1`
      * 重命名：  `Net revenue`
   * 量度 `3`： `Coupon discount amount`
      * 添加筛选器：
         * [`A`] `coupon_code` **不是**`[NULL]`
         * [`B`] `Customer's order number` **等于** `1`
   * 创建公式： `Gross revenue`
      * [!UICONTROL Formula]: `(B – C)`
      * 
         [!UICONTROL Format]: `Currency`
   * 创建公式：**折扣百分比**
      * 公式： `(C / (B - C))`
      * 
         [!UICONTROL Format]: `Percentage`
   * 创建公式： `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * 
         [!UICONTROL Format]: `Percentage`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL间隔]: `None`
   * 

      [！UICONTROL图表类型]: `Table`








* **按一阶优惠券计算的平均生命周期收入**
   * [!UICONTROL Metric]：**平均生命周期收入**
      * 添加筛选器：
         * [`A`] `coupon_code` **是**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL间隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **优惠券使用情况详细信息（首次订购）**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 添加筛选器：
         * [`A`] `Customer's first order's coupon_code` **不是** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL间隔]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * 

      [！UICONTROL图表类型]: **Column**


* **按优惠券/无优惠券收购划分的新客户**
   * 量度 `1`： `New customers`
      * 添加筛选器：
         * [`A`] `Customer's first order's coupon_code` **不是** `[NULL]`
      * [!UICONTROL Rename]: `Coupon acquisition customer`
   * 量度 `2`： `New customers`
      * 添加筛选器：
         * [`A`] `coupon_code` **是**`[NULL]`
      * [!UICONTROL Rename]: `Non-coupon acquisition customer`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * [!UICONTROL Chart type]: `Stacked Column`





构建报表后，请参阅本主题顶部的图像，了解如何在功能板上组织报表。
