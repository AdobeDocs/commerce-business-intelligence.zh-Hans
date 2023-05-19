---
title: 免費送貨閾值
description: 瞭解如何設定儀表板來追蹤您免運費運送臨界值的效能。
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# 免運費

>[!NOTE]
>
>本主題包含使用原始架構和新架構的使用者端指示。 如果您擁有以下優勢，即可使用新架構： `Data Warehouse Views` 選取後可用的區段 `Manage Data` 從主工具列。

此主題示範如何設定追蹤免運費運送臨界值績效的控制面板。 這個儀表板（如下所示）是A/B測試兩個免運費臨界值的好方法。 例如，貴公司可能不確定您應以$50或$100的價格提供免運費。 您應針對客戶的兩個隨機子集執行A/B測試，並在下列位置執行分析： [!DNL Commerce Intelligence].

開始之前，您想要識別兩個不同的時段，您在此時段擁有商店免運費閾值的不同值。

![](../../assets/free_shipping_threshold.png)

此分析包含 [進階計算欄](../data-warehouse-mgr/adv-calc-columns.md).

## 計算欄

如果您使用原始架構(例如，如果您沒有 `Data Warehouse Views` 下的選項 `Manage Data` 功能表)，您想要聯絡支援團隊以建置以下欄。 在新架構上，這些欄可從以下網址建立： `Manage Data > Data Warehouse` 頁面。 詳細指示如下。

* **`sales_flat_order`** 表格
   * 此計算會以相對於您一般購物車大小的增量建立貯體。 這可以從增量開始，包括5、10、50、100

* **`Order subtotal (buckets)`** 原始架構：由分析師建立，隸屬於 `[FREE SHIPPING ANALYSIS]` 票證
* **`Order subtotal (buckets)`** 新架構：
   * 如上所述，此計算會以相對於您一般購物車大小的增量建立貯體。 如果您有原生小計欄，例如 `base_subtotal`，可作為此新欄的基礎。 如果沒有，它可以是計算欄，不包含收入的送貨和折扣。
   >[!NOTE]
   >
   >「貯體」大小取決於適合您作為使用者端的尺寸。 您可以先從您的 `average order value` 並建立小於或大於該數量的值區。 檢視以下計算時，您會看到如何輕鬆複製部分查詢、編輯查詢以及建立其他值區。 範例以50為增量完成。

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal`，或 `calculated column`， `Datatype`： `Integer`
   * [!UICONTROL Calculation]： `case when A >= 0 and A<=200 then 0 - 200`
當 `A< 200` 和 `A <= 250` 則 `201 - 250`
時間 `A<251` 和 `A<= 300` 則 `251 - 300`
時間 `A<301` 和 `A<= 350` 則 `301 - 350`
時間 `A<351` 和 `A<=400` 則 `351 - 400`
時間 `A<401` 和 `A<=450` 則 `401 - 450`
否則&#39;超過450&#39;結尾



## 量度

沒有新量度!!!

>[!NOTE]
>
>請確定 [將所有新欄新增為量度的維度](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 建立新報表之前。

## 報表

* **具有出貨規則A的平均訂單值**
   * [!UICONTROL Metric]: `Average order value`

* 量度 `A`： `Average Order Value`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **具有出貨規則A的訂單小計時段數**
   * [!UICONTROL Metric]: `Number of orders`

   >[!NOTE]
   >
   >您可以顯示頂端來截斷尾端 `X` `sorted by` `Order subtotal` （貯體） `Show top/bottom`.

* 量度 `A`： `Number of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Column`

* **具有出貨規則A之小計的訂單百分比**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * 
      [！UICONTROL分組依據]: `Independent`
   * [!UICONTROL Formula]: `(A / B)`
   * 

      [!UICONTROL Format]: `%`

* 量度 `A`： `Number of orders by subtotal (hide)`
* 量度 `B`： `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Line`

* **小計超過出貨規則A的訂單百分比**
   * [!UICONTROL Metric]: `Number of orders`
   * 

      [!UICONTROL Perspective]: `Cumulative`

   * [!UICONTROL Metric]: `Number of orders`
   * 

      [！UICONTROL分組依據]: `Independent`

   * [!UICONTROL Formula]: `1- (A / B)`
   * 

      [!UICONTROL Format]: `%`

* 量度 `A`： `Number of orders by subtotal`
* 量度 `B`： `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 

   [!UICONTROL Chart Type]: `Line`


針對「出貨B」及具有出貨規則B的時間期間，重複上述步驟與報表。

編譯所有報表後，您可以視需要在控制面板上組織報表。 結果看起來可能像這個頁面頂端的影像。
