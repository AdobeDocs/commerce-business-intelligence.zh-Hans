---
title: 分析存貨層次
description: 瞭解如何分析庫存水準。
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# 分析存貨層次

此主題示範如何設定儀表板，提供您目前詳細目錄的分析，並包含舊版架構或新架構的客戶說明。 如果您沒有以下許可權，則可以使用舊版架構： **[!UICONTROL Data Warehouse Views]** 下的選項 **[!UICONTROL Manage Data]** 功能表。 如果您使用舊版架構，請提交 [新的支援要求](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 與主旨 **[!UICONTROL INVENTORY ANALYSIS]** 一旦您到達 _已計算的欄_ 以下說明。

## 要追蹤的欄：

### 要追蹤指示的欄

* **[!UICONTROL cataloginventory_stock_item]** 表格：
   * **`item_id`**
   * **`product_id`**
   * **`qty`**

* **[!UICONTROL catalog_product_entity]** 表格：
   * **`entity_id`**
   * **`sku`**
   * **`created_at`**

## 計算資料行：

+++ 新架構

* **[!UICONTROL catalog_product_entity]** 表格：
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 選取 [!UICONTROL column]： `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 選取 [!UICONTROL column]： `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `AGE`
      * 選取 [!UICONTROL DATETIME column]： `Product's most recent order date`
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 選取 [!UICONTROL column]： `qty_ordered`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] 輸入：
         * 答： `Product's lifetime number of items sold`
         * B： `Product's first order date`
      * 
         [!UICONTROL Datatype]: `Decimal`
      * 定義：
         * 當A為null或B為null時，則為空值，否則四捨五入(A：：decimal/(extract(epoch from (current_timestamp - B))：：decimal/604800.0)，2)結束





* **[!UICONTROL cataloginventory_stock_item]** 表格：
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選取 [!UICONTROL column]： `sku`
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選取 [!UICONTROL column]： `Product's lifetime number of items sold`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選取 [!UICONTROL column]： `Seconds since product's most recent order date`
   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選取 [!UICONTROL column]： `Avg products sold per week (all time)`
   * **`Weeks on hand`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] 輸入：
         * 答： `qty`
         * B： `Avg products sold per week (all time)`
      * 
         [!UICONTROL Datatype]: `Decimal`
      * 定義：
         * 當A為null或B為null或B = 0.0時則為空值，否則四捨五入(A：：decimal/B，2)結束





+++
+++ 舊版架構

* **[!UICONTROL catalog_product_entity]** 表格：
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 選取 [!UICONTROL column]： `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * 選取 [!UICONTROL column]： `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
         [!UICONTROL Column equation]: `AGE`
      * 選取DATETIME欄： **`Product's most recent order date`**
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
         [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
      * 選取 [!UICONTROL column]： **`qty_ordered`**
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`
   * **`Avg products sold per week (all time)`**
      * 由分析師在您提交您的檔案時建立 **[詳細目錄分析]** 支援要求





* **[!UICONTROL cataloginventory_stock_item]** 表格：
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選取 [!UICONTROL column]： `sku`
   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選取 [!UICONTROL column]： `Product's lifetime number of items sold`
   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選取 [!UICONTROL column]： `Seconds since product's most recent order date`
   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
         [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * 選取 [!UICONTROL column]： `Avg products sold per week (all time)`
   * **`Weeks on hand`**
      * 由分析師在您提交您的檔案時建立 **[!UICONTROL INVENTORY ANALYSIS]** 支援要求





+++

## 量度

### 量度指示

* **[!UICONTROL cataloginventory_stock_item]** 表格：
   * **`Inventory on hand`**：此量度執行
      * **總和** 於
      * **`qty`** 欄排序依據
      * [無] 欄

## 報表

### 報表指示

* **`Inventory on hand by sku`**
   * [!UICONTROL Metric]: `Inventory on hand`
   * [!UICONTROL Time period]: `All time`
   * 時間間隔： `None`
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
   * 時間間隔： `None`
   * 
      [！UICONTROL分組依據]: `Sku`
   * 

      [!UICONTROL Chart type]: `Table`


* **`Inventory with more than 26 weeks on hand (put on sale)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `> 26`
   * [!UICONTROL Time period]: `All time`
   * 時間間隔： `None`
   * 
      [！UICONTROL分組依據]: `Sku`
   * 

      [!UICONTROL Chart type]: `Table`


如果您在建立此分析時遇到任何問題，或只是想與Professional Services團隊互動， [聯絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
