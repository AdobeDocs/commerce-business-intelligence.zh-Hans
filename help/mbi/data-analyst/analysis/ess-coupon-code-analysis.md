---
title: 抵用券代碼分析（基本）
description: 瞭解您企業的優惠券成效，是細分訂單，並更好地瞭解客戶習慣的有趣方式。
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# 基本優惠券代碼分析

瞭解您企業的優惠券成效，是細分訂單、更妥善瞭解客戶習慣的有趣方式。

本主題會記錄建立此分析所需的步驟，以瞭解取得優惠券之客戶的表現、檢視趨勢以及追蹤個別優惠券代碼的使用情況。

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## 快速入門

首先，附註說明如何追蹤優惠券代碼。 如果客戶將優惠券套用至訂單，則會發生下列三件事：

* 折扣會反映在 `base_grand_total` 金額(您的 `Revenue` Commerce Intelligence中的量度)
* 優惠券代碼會儲存在 `coupon_code` 欄位。 如果此欄位為NULL （空白），則訂單沒有關聯的抵用券。
* 折扣金額儲存在 `base_discount_amount`. 根據您的設定，此值可能顯示為負數或正數。

## 建立量度

第一步是透過下列步驟建構新量度：

* 導覽至 **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* 選取 `sales_order`.
* 此量度會執行 **總和** 於 **base_discount_amount** 欄，排序方式 **created_at**.
   * [!UICONTROL Filters]:
      * 新增 `Orders we count` （儲存的篩選器集）
      * 新增下列專案：
         * `coupon_code`**不是**`[NULL]`
      * 為量度命名，例如 `Coupon discount amount`.

## 建立您的控制面板

* 建立量度後：
   * 導覽至 [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**。
   * 為儀表板命名，例如 `_Coupon Analysis_`.

* 您可以在此處建立和新增所有報表。

## 建立報表

* **新報告：**

>[!NOTE]
>
>此 [!UICONTROL Time Period]每個報表的**列為 `All-time`. 您可以隨時根據您的分析需求加以變更。 Adobe建議此儀表板上的所有報告涵蓋相同時段，例如 `All time`， `Year-to-date`，或 `Last 365 days`.

* **含優惠券的訂單**
   * 
      [！UICONTROL公制]: `Orders`
      * 新增篩選器：
         * [`A`] `coupon_code` **不是** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **沒有優惠券的訂單**
   * 
      [！UICONTROL公制]: `Orders`
      * 新增篩選器：
         * [`A`] `coupon_code` **是** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **含抵用券的訂單淨收入**
   * 
      [！UICONTROL公制]: `Revenue`
      * 新增篩選器：
         * [`A`] `coupon_code` **不是** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **優惠券折扣**
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **平均期限收入：獲得優惠券的客戶**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 新增篩選器：
         * [`A`] `Customer's first order's coupon_code` **不是** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **平均期限收入：非優惠券取得的客戶**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 新增篩選器：
         * [A] `Customer's first order's coupon_code` **是**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **優惠券使用量詳細資料（首次訂購）**
   * 量度 `1`： `Orders`
      * 新增篩選器：
         * [`A`] `coupon_code` **不是**`[NULL]`
         * [`B`] `Customer's order number` **等於** `1`
   * 量度 `2`： `Revenue`
      * 新增篩選器：
         * [`A`] `coupon_code` **不是**`[NULL]`
         * [`B`] `Customer's order number` **等於** `1`
      * 重新命名：  `Net revenue`
   * 量度 `3`： `Coupon discount amount`
      * 新增篩選器：
         * [`A`] `coupon_code` **不是**`[NULL]`
         * [`B`] `Customer's order number` **等於** `1`
   * 建立公式： `Gross revenue`
      * [!UICONTROL Formula]: `(B – C)`
      * 
         [!UICONTROL Format]: `Currency`
   * 建立公式：**折扣百分比**
      * 公式： `(C / (B - C))`
      * 
         [!UICONTROL Format]: `Percentage`
   * 建立公式： `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * 
         [!UICONTROL Format]: `Percentage`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL間隔]: `None`
   * 

      [！UICONTROL圖表型別]: `Table`








* **依第一筆抵用券的平均期限收入**
   * [!UICONTROL Metric]：**平均期限收入**
      * 新增篩選器：
         * [`A`] `coupon_code` **是**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **優惠券使用量詳細資料（首次訂購）**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 新增篩選器：
         * [`A`] `Customer's first order's coupon_code` **不是** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL間隔]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * 

      [！UICONTROL圖表型別]: **Column**


* **依優惠券/非優惠券贏取的新客戶**
   * 量度 `1`： `New customers`
      * 新增篩選器：
         * [`A`] `Customer's first order's coupon_code` **不是** `[NULL]`
      * [!UICONTROL Rename]: `Coupon acquisition customer`
   * 量度 `2`： `New customers`
      * 新增篩選器：
         * [`A`] `coupon_code` **是**`[NULL]`
      * [!UICONTROL Rename]: `Non-coupon acquisition customer`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * [!UICONTROL Chart type]: `Stacked Column`





建立報表後，請參閱本主題頂端的影像，瞭解如何在控制面板上組織報表。
