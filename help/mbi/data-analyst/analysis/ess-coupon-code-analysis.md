---
title: 优惠券代码分析（基本）
description: 了解企业的优惠券表现是细分订单并更好地了解客户习惯的有趣方式。
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# 基本优惠券代码分析

了解业务的优惠券性能是划分订单细分和更好地了解客户习惯的有趣方式。

我们记录了创建此分析所需的步骤，以了解获得优惠券的客户的表现、查看趋势并跟踪单个优惠券代码的使用情况。

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## 快速入门

首先，提供有关如何跟踪优惠券代码的说明。 如果客户将优惠券应用于订单，则会发生以下三种情况：

* 折扣反映在 `base_grand_total` amount(您的 `Revenue` 量度)
* 优惠券代码存储在 `coupon_code` 字段。 如果此字段为NULL（空），则订单中没有与其关联的优惠券。
* 折扣金额存储于 `base_discount_amount`. 根据您的配置，此值可能显示为负或正。

## 生成量度

第一步是通过以下步骤构建新量度：

* 导航到 **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* 选择 `sales_order`.
* 此量度执行 **总和** 在 **base_discount_amount** 列，排序依据 **created_at**.
   * [!UICONTROL Filters]:
      * 添加 `Orders we count` （保存的过滤器集）
      * 添加以下内容：
         * `coupon_code`**IS NOT**`[NULL]`
      * 为量度命名，例如 `Coupon discount amount`.

## 创建功能板

* 创建量度后：
   * 导航到 [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**。
   * 为功能板指定名称，例如 `_Coupon Analysis_`.

* 我们将在此处创建和添加所有报表。

## 生成报告

* **新报表：**

>[!NOTE]
>
>的 [!UICONTROL Time Period]**对于每个报表，列为 `All-time`. 请随时更改此参数以满足您的分析需求。 我们建议此仪表板上的所有报表涵盖同一时间段，例如 `All time`, `Year-to-date`或 `Last 365 days`.

* **具有优惠券的订单**
   * 
      [!UICONTROL量度]: `Orders`
      * 添加过滤器：
         * [`A`] `coupon_code` **IS NOT** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL间隔]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **没有优惠券的订单**
   * 
      [!UICONTROL量度]: `Orders`
      * 添加过滤器：
         * [`A`] `coupon_code` **IS** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL间隔]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **具有优惠券的订单的净收入**
   * 
      [!UICONTROL量度]: `Revenue`
      * 添加过滤器：
         * [`A`] `coupon_code` **IS NOT** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL间隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **优惠券折扣**
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL间隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **平均存留期收入：购入优惠券的客户**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 添加过滤器：
         * [`A`] `Customer's first order's coupon_code` **IS NOT** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL间隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **平均存留期收入：购入的非优惠券客户**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 添加过滤器：
         * [A] `Customer's first order's coupon_code` **IS**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL间隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **优惠券使用详细信息（首次订购）**
   * 量度 `1`: `Orders`
      * 添加过滤器：
         * [`A`] `coupon_code` **IS NOT**`[NULL]`
         * [`B`] `Customer's order number` **等于** `1`
   * 量度 `2`: `Revenue`
      * 添加过滤器：
         * [`A`] `coupon_code` **IS NOT**`[NULL]`
         * [`B`] `Customer's order number` **等于** `1`
      * 重命名：  `Net revenue`
   * 量度 `3`: `Coupon discount amount`
      * 添加过滤器：
         * [`A`] `coupon_code` **IS NOT**`[NULL]`
         * [`B`] `Customer's order number` **等于** `1`
   * 创建新公式： `Gross revenue`
      * [!UICONTROL Formula]: `(B – C)`
      * 
         [!UICONTROL Format]: `Currency`
   * 创建新公式：**%折扣**
      * 公式： `(C / (B - C))`
      * 
         [!UICONTROL Format]: `Percentage`
   * 创建新公式： `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * 
         [!UICONTROL Format]: `Percentage`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL间隔]: `None`
   * 

      [!UICONTROL图表类型]: `Table`








* **按订单优惠券划分的平均存留期收入**
   * [!UICONTROL Metric]:**平均存留期收入**
      * 添加过滤器：
         * [`A`] `coupon_code` **IS**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL间隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **优惠券使用详细信息（首次订购）**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 添加过滤器：
         * [`A`] `Customer's first order's coupon_code` **IS NOT** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL间隔]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * 

      [!UICONTROL图表类型]: **Column**


* **按优惠券/非优惠券客户获取划分的新客户**
   * 量度 `1`: `New customers`
      * 添加过滤器：
         * [`A`] `Customer's first order's coupon_code` **IS NOT** `[NULL]`
      * [!UICONTROL Rename]: `Coupon acquisition customer`
   * 量度 `2`: `New customers`
      * 添加过滤器：
         * [`A`] `coupon_code` **IS**`[NULL]`
      * [!UICONTROL Rename]: `Non-coupon acquisition customer`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * [!UICONTROL Chart type]: `Stacked Column`





构建报表后，请参阅本主题顶部的图像，了解如何在功能板上组织报表。
