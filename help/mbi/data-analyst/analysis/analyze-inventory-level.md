---
title: 分析库存水平
description: 了解如何分析库存水平。
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 分析库存水平

本主题演示了如何设置功能板，以便提供对当前库存的分析。 本主题包含有关旧架构或新架构上客户端的说明。 如果您没有 **[!UICONTROL Data Warehouse Views]** 选项 **[!UICONTROL Manage Data]** 菜单)。 如果您使用的是旧版架构，请提交 [新支持请求](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) 主题 **[!UICONTROL INVENTORY ANALYSIS]** 在 _计算列_ 下面的说明。

## 要跟踪的列：

### 用于跟踪说明的列

* **[!UICONTROL cataloginventory_stock_item]** 表：
   * **`item_id`**
   * **`product_id`**
   * **`qty`**

* **[!UICONTROL catalog_product_entity]** 表：
   * **`entity_id`**
   * **`sku`**
   * **`created_at`**

## 计算列：

### 新架构

* **[!UICONTROL catalog_product_entity]** 表：
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 选择 [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 选择 [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `AGE`
      * 选择 [!UICONTROL DATETIME column]: `Product's most recent order date`
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 选择 [!UICONTROL column]: `qty_ordered`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] 输入：
         * 答： `Product's lifetime number of items sold`
         * B: `Product's first order date`
      * 
         [!UICONTROL Datatype]: `Decimal`
      * 定义：
         * 当A为null或B为null时，则返回null，否则返回(A::decimal/(extract(epocfrom(current_timestamp - B))::decimal/604800.0),2)end





* **[!UICONTROL cataloginventory_stock_item]** 表：
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 选择 [!UICONTROL column]: `sku`
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 选择 [!UICONTROL column]: `Product's lifetime number of items sold`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 选择 [!UICONTROL column]: `Seconds since product's most recent order date`
   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 选择 [!UICONTROL column]: `Avg products sold per week (all time)`
   * **`Weeks on hand`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] 输入：
         * 答： `qty`
         * B: `Avg products sold per week (all time)`
      * 
         [!UICONTROL Datatype]: `Decimal`
      * 定义：
         * 当A为null或B为null或B = 0.0时，则返回null(A::decimal/B，2)结尾





### 旧版架构

* **[!UICONTROL catalog_product_entity]** 表：
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 选择 [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 选择 [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `AGE`
      * 选择DATETIME列： **`Product's most recent order date`**
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
      * 选择 [!UICONTROL column]: **`qty_ordered`**
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Avg products sold per week (all time)`**
      * 将由分析师在提交 **[库存分析]** 支持请求





* **[!UICONTROL cataloginventory_stock_item]** 表：
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 选择 [!UICONTROL column]: `sku`
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 选择 [!UICONTROL column]: `Product's lifetime number of items sold`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 选择 [!UICONTROL column]: `Seconds since product's most recent order date`
   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 选择 [!UICONTROL column]: `Avg products sold per week (all time)`
   * **`Weeks on hand`**
      * 将由分析师在提交 **[!UICONTROL INVENTORY ANALYSIS]** 支持请求





## 量度

### 量度说明

* **[!UICONTROL cataloginventory_stock_item]** 表：
   * **`Inventory on hand`**:此量度执行
      * **总和** 在
      * **`qty`** 列按
      * [无] 列

## 报表

### 报告说明

* **`Inventory on hand by sku`**
   * [!UICONTROL Metric]: `Inventory on hand`
   * [!UICONTROL Time period]: `All time`
   * 时间间隔： `None`
   * [!UICONTROL Group by]:
      * `Sku`
      * `Weeks on hand`
   * 

      [!UICONTROL Chart type]: `Table`

* **`Inventory with less than 2 weeks on hand (order now)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `< 2`
   * [!UICONTROL Time period]: `All time`
   * 时间间隔： `None`
   * 
      [!UICONTROL组依据]: `Sku`
   * 

      [!UICONTROL Chart type]: `Table`


* **`Inventory with more than 26 weeks on hand (put on sale)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `> 26`
   * [!UICONTROL Time period]: `All time`
   * 时间间隔： `None`
   * 
      [!UICONTROL组依据]: `Sku`
   * 

      [!UICONTROL Chart type]: `Table`


如果您在构建此分析时遇到任何问题，或者只想与我们的专业服务团队接洽， [联系支持](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
