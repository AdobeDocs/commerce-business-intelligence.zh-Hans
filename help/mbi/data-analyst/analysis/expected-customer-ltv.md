---
title: Pro的預期期限值(LTV)分析
description: 瞭解如何設定儀表板，協助您瞭解客戶期限值成長和客戶的預期期限值。
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# 預期期限值分析

此主題示範如何設定儀表板，協助您瞭解客戶期限值成長和客戶的預期期限值。

![](../../assets/exp-lifetim-value-anyalysis.png)

此分析僅供使用新架構的Pro客戶使用。 如果您的帳戶有權存取 `Persistent Views` 下的功能 `Manage Data` 側欄中，您所使用的是新架構，可以依照此處列出的指示，自行建立此分析。

開始使用前，請先熟悉 [同類群組report builder。](../dev-reports/cohort-rpt-bldr.md)

## 計算欄

要在上建立的欄 **訂購** 表格（若使用） **30天月**：

* [!UICONTROL Column name]: `Months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]： A = `Seconds between customer's first order date and this order`
* 
   [!UICONTROL Datatype]: `Integer`
* **定義：**`case when A is null then null when A <= 0 then '1'::int else (ceil(A)/2629800)::int end`

* [!UICONTROL Column name]: `Months since order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]： A = `created_at`
* 
   [!UICONTROL Datatype]: `Integer`
* 定義： `case when created_at is null then null else (ceil((extract(epoch from current_timestamp) - extract(epoch from created_at))/2629800))::int end`

要在上建立的欄 **`orders`** 表格（若使用） **行事曆** 月：

* [!UICONTROL Column name]: `Calendar months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column inputs]:
   * `A` = `created_at`
   * `B` = `Customer's first order date`

* 
   [!UICONTROL Datatype]: `Integer`
* 定義： `case when (A::date is null) or (B::date is null) then null else ((date_part('year',A::date) - date_part('year',B::date))*12 + date_part('month',A::date) - date_part('month',B::date))::int end`

* [!UICONTROL Column name]: `Calendar months since order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: `A` = `created_at`
* 
   [!UICONTROL Datatype]: `Integer`
* **定義：**`case when A is null then null else ((date_part('year',current_timestamp::date) - date_part('year',A::date))*12 + date_part('month',current_timestamp::date) - date_part('month',A::date))::int end`

* [!UICONTROL Column name]: `Is in current month? (Yes/No)`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]： A = `created_at`
* 
   [!UICONTROL Datatype]: `String`
* 定義： `case when A is null then null when (date_trunc('month', current_timestamp::date))::varchar = (date_trunc('month', A::date))::varchar then 'Yes' else 'No' end`

## 量度

### 量度指示

要建立的量度

* **依第一筆訂單日期區分的不同客戶**
   * 如果您啟用來賓訂單，請使用 `customer_email`

* 在 **`orders`** 表格
* 此量度會執行 **計算不同的值**
* 於 **`customer_id`** 欄
* 排序依據： **`Customer's first order date`** timestamp

>[!NOTE]
>
>請確定 [將所有新欄新增為量度的維度](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 建立新報表之前。

## 報表

### 報表指示

**每個客戶的預期收入（按月）**

* 量度 `A`： `Revenue (hide)`
   * `Calendar months between first order and this order` `<= X` （為X選取一些合理的數字，例如24個月）
   * `Is in current month?` = `No`

* 
   [！UICONTROL公制]: `Revenue`
* [!UICONTROL Filter]:

* 量度 `B`： `All time customers (hide)`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* 量度 `C`： `All time customers by month since first order (hide)`
   * `Calendar months since order` `<= X`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Expected revenue`
* [!UICONTROL Formula]: `A / (B - C)`
* 

   [!UICONTROL Format]: `Currency`

其他圖表詳細資料

* [!UICONTROL Time period]: `All time`
* 時間間隔： `None`
* [!UICONTROL Group by]： `Calendar months between first order and this order`  — 全部顯示
* 變更 `group by` 的 `All time customers` 量度變更為獨立(使用 `group by`
* 編輯 `Show top/bottom` 欄位如下所示：
   * [!UICONTROL Revenue]: `Top 24 sorted by Calendar months between first order and this order`
   * [!UICONTROL All time customers]: `Top 24 sorted by All time customers`
   * [!UICONTROL All time customers by month since first order]: `Top 24 sorted by All time customers by month since first order`

**每個月依同類群組的平均收入**

* 量度 `A`： `Revenue`
* 
   [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Average value per cohort member`

**按同類群組分類的每月累計平均收入**

* 量度 `A`： `Revenue`
* 
   [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Cumulative average value per cohort member`

編譯所有報表後，您可以視需要在控制面板上組織報表。 結果看起來可能像頁面頂端的影像。

如果您在建立此分析時遇到任何問題，或只是想與Professional Services團隊互動， [聯絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
