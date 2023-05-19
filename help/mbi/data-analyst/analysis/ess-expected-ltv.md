---
title: 預期期限值(LTV)分析（基本）
description: 瞭解如何建立分析以瞭解您目前客戶的期限值，並預測期限值如何隨著更多訂單而增加。
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# 預期期限值分析

預測客戶下更多訂單時的期限價值，是任何規模企業最重要的方面之一。

以下是建立分析的步驟，以瞭解您目前客戶的期限值，並預測期限值如何隨著更多訂單而增加。

![預期期限值](../../assets/expected_ltv_720.png)

## 建立量度

第一步是透過下列步驟建構新量度：
* 導覽至 **[!UICONTROL Manage Data > Metrics]**
   * 檢視現有 **[!UICONTROL Avg lifetime revenue]**.

   >[!NOTE]
   >
   >建構此量度的資料表(可能 `customer_entity` 或 `sales_order` 視您的商店是否接受訪客結帳而定。)

   * 按一下 **[!UICONTROL Create New Metric]** 並從上方選取表格。
   * 此量度會執行 **中位數** 於 `Customer's lifetime revenue` 欄，排序方式 `created_at`.
      * [!UICONTROL Filters]:
         * 新增 `Customers we count (Saved Filter Set)` (或 `Registered accounts we count`)
   * 為量度命名，例如 `Median lifetime revenue`.



## 建立您的控制面板

建立量度後，您可以 **建立控制面板** 藉由執行下列動作：
* 導覽至 **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* 為儀表板命名，例如 `Expected LTV`.

* 您可以在此處建立和新增所有報表。

## 建立報表

>[!NOTE]
>
>開啟 **[!UICONTROL Time Period:]**，則每個報表的時段會列為 `All-time`. 您可以隨時根據您的分析需求加以變更。 Adobe建議此儀表板上的所有報告涵蓋相同時段，例如 `All time`， `Year-to-date`，或 `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL間隔]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 新增 [!UICONTROL filters]：
         * [`A`] `Customer's group code` **不等於** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **大於**`0`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL間隔]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`


* **[!UICONTROL Average and Median LTV]**
   * 量度 `1`： `Avg lifetime revenue`
   * 量度 `2`： `Median lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * 
      [！UICONTROL圖表型別]: `Line`
   * 取消核取 `Multiple Y-Axes`

* **LTV （依期限訂單數）**
   * 量度 `1`： `Avg lifetime revenue`
   * 量度 `2`： `New customers`
   * [!UICONTROL Time period]: `All time`
   * 
      [！UICONTROL間隔]: `None`
   * [!UICONTROL Group by]: `Customer's lifetime number of orders`
   * 

      [！UICONTROL圖表型別]: `Line`
   >[!NOTE]
   >
   >不要新增以下專案的所有值： `Customer's lifetime number of orders`. 反之，看看新客戶數目達到一個小數點的情況，然後手動將每個客戶的存留期編號訂單值增加到該點。 舉例來說，如果同一筆訂單有200名客戶、兩筆有75名客戶、三筆有15名客戶、四筆有3名客戶，則新增 *1、2和3*.

* 新增現有 [!UICONTROL Avg customer lifetime revenue by cohort] 報告。

建立報表後，請參閱本主題頂端的影像，瞭解如何在控制面板上組織報表。
