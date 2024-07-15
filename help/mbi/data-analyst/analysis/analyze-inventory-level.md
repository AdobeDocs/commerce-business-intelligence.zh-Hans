---
title: 分析库存水平
description: 了解如何分析库存水平。
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# 分析库存水平

本主题将演示如何设置功能板，该功能板提供有关当前库存的洞察信息，并包含有关旧架构或新架构的客户端说明。 如果您在&#x200B;**[!UICONTROL Manage Data]**&#x200B;菜单下没有&#x200B;**[!UICONTROL Data Warehouse Views]**&#x200B;选项，则表示您使用的是旧版架构。 如果您使用的是旧架构，请在到达以下&#x200B;_计算列_&#x200B;说明中的指定部分后，提交主题为&#x200B;**[!UICONTROL INVENTORY ANALYSIS]**&#x200B;的[新支持请求](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

## 要跟踪的列：

### 要跟踪指令的列

* **[!UICONTROL cataloginventory_stock_item]**&#x200B;表：
   * **`item_id`**
   * **`product_id`**
   * **`qty`**

* **[!UICONTROL catalog_product_entity]**&#x200B;表：
   * **`entity_id`**
   * **`sku`**
   * **`created_at`**

## 计算列：

+++ 新架构

* **[!UICONTROL catalog_product_entity]**&#x200B;表：
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]： `Many to One`
      * 
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]： `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 选择[!UICONTROL column]： `created_at`
      * [!UICONTROL Filters]：
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]： `Many to One`
      * 
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]： `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 选择[!UICONTROL column]： `created_at`
      * [!UICONTROL Filters]：
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]： `Same Table`
      * 
        [!UICONTROL Column equation]: `AGE`
      * 选择[!UICONTROL DATETIME column]： `Product's most recent order date`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]： `Many to One`
      * 
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]： `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 选择[!UICONTROL column]： `qty_ordered`
      * [!UICONTROL Filters]：
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]： `Same Table`
      * 
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column]输入：
         * A： `Product's lifetime number of items sold`
         * B： `Product's first order date`
      * 
        [!UICONTROL Datatype]: `Decimal`
      * 定义：
         * 当A为null或B为null时，则为null，否则第(A：：decimal/(extract(epoch from (current_timestamp - B))：：decimal/604800.0)，2)末尾

* **[!UICONTROL cataloginventory_stock_item]**&#x200B;表：
   * **`Sku`**
      * [!UICONTROL Column type]： `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]： `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 选择[!UICONTROL column]： `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]： `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]： `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 选择[!UICONTROL column]： `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]： `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]： `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 选择[!UICONTROL column]： `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]： `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]： `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 选择[!UICONTROL column]： `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * [!UICONTROL Column type]： `Same Table`
      * 
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column]输入：
         * A： `qty`
         * B： `Avg products sold per week (all time)`
      * 
        [!UICONTROL Datatype]: `Decimal`
      * 定义：
         * 当A为null或B为null或B = 0.0时为null，否则以round(A：：decimal/B，2)结束

+++
+++ 旧式架构

* **[!UICONTROL catalog_product_entity]**&#x200B;表：
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]： `Many to One`
      * 
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]： `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 选择[!UICONTROL column]： `created_at`
      * [!UICONTROL Filters]：
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]： `Many to One`
      * 
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]： `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 选择[!UICONTROL column]： `created_at`
      * [!UICONTROL Filters]：
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]： `Same Table`
      * 
        [!UICONTROL Column equation]: `AGE`
      * 选择DATETIME列： **`Product's most recent order date`**

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]： `Many to One`
      * 
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]： **`sales_order_item.product_id => catalog_product_entity.entity_id`**
      * 选择[!UICONTROL column]： **`qty_ordered`**
      * [!UICONTROL Filters]：
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * 由分析人员在提交&#x200B;**[库存分析]**&#x200B;支持请求时创建

* **[!UICONTROL cataloginventory_stock_item]**&#x200B;表：
   * **`Sku`**
      * [!UICONTROL Column type]： `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]： `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 选择[!UICONTROL column]： `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]： `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]： `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 选择[!UICONTROL column]： `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]： `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]： `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 选择[!UICONTROL column]： `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]： `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]： `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 选择[!UICONTROL column]： `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * 在您提交您的&#x200B;**[!UICONTROL INVENTORY ANALYSIS]**&#x200B;支持请求时由分析人员创建

+++

## 量度

### 量度说明

* **[!UICONTROL cataloginventory_stock_item]**&#x200B;表：
   * **`Inventory on hand`**：此量度执行
      * **总和**&#x200B;位于
      * **`qty`**&#x200B;列排序依据
      * [无]列

## 报告

### 报表说明

* **`Inventory on hand by sku`**
   * [!UICONTROL Metric]： `Inventory on hand`
   * [!UICONTROL Time period]： `All time`
   * 时间间隔： `None`
   * [!UICONTROL Group by]：
      * `Sku`
      * `Weeks on hand`
   * 
     [!UICONTROL Chart type]: `Table`

* **`Inventory with less than 2 weeks on hand (order now)`**
   * [!UICONTROL Metric]： `Inventory on hand`
      * [!UICONTROL Filters]：
         * [A] `Weeks on hand` `< 2`

   * [!UICONTROL Time period]： `All time`
   * 时间间隔： `None`
   * 
     [！UICONTROL分组依据]: `Sku`
   * 
     [!UICONTROL Chart type]: `Table`

* **`Inventory with more than 26 weeks on hand (put on sale)`**
   * [!UICONTROL Metric]： `Inventory on hand`
      * [!UICONTROL Filters]：
         * [A] `Weeks on hand` `> 26`

   * [!UICONTROL Time period]： `All time`
   * 时间间隔： `None`
   * 
     [！UICONTROL分组依据]: `Sku`
   * 
     [!UICONTROL Chart type]: `Table`

如果您在构建此分析时遇到任何问题，或只是想与专业服务团队接洽，请[联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
