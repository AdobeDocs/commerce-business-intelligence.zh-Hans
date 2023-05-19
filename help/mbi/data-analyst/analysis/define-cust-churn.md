---
title: 定義客戶流失
description: 瞭解如何設定儀表板，協助您定義交易式客戶的流失率。
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# 異動客戶流失

此主題示範如何設定儀表板，協助您定義交易式客戶的流失率。

![](../../assets/churn-deashboard.png)

此分析包含 [進階計算欄](../data-warehouse-mgr/adv-calc-columns.md).

## 計算欄

要建立的欄

* `customer_entity` 表格
* `Customer's lifetime number of orders`
* 選取定義： `Count`
* 選取 [!UICONTROL table]： `sales_flat_order`
* 選取 [!UICONTROL column]： **`entity_id`**
* [!UICONTROL Path]： sales_flat_order.customer_id = customer_entity.entity_id
* [!UICONTROL Filter]:
* 已計數的訂單

* `sales_flat_order` 表格
* `Customer's lifetime number of orders`
* 選取定義：聯結資料行
* 選取 [!UICONTROL table]： `customer_entity`
* 選取 [!UICONTROL column]： `Customer's lifetime number of orders`
* [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]: `Orders we count`

* `Seconds since created_at`
* 選取定義： `Age`
* 選取 [!UICONTROL column]： `created_at`

* **`Customer's order number`** 由分析師建立，作為您的一部分 **[定義流失]** 票證
* **`Is customer's last order`** 由分析師建立，作為您的一部分 **[定義流失]** 票證
* **`Seconds since previous order`** 由分析師建立，作為您的一部分 **[定義流失]** 票證
* **`Months since order`** 由分析師建立，作為您的一部分 **[定義流失]** 票證
* **`Months since previous order`** 由分析師建立，作為您的一部分 **[定義流失]** 票證

## 量度

沒有新量度！

>[!NOTE]
>
>請確定 [將所有新欄新增為量度的維度](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 建立新報表之前。

## 報表

* **初始重複順序機率**
* 量度A：所有時間重複訂單
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 量度B：所有時間訂單
* [!UICONTROL Metric]：訂單數

* [!UICONTROL Formula]：初始重複順序機率
* 
   [！UICONTROL公式]: `A/B`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart type]: `Scalar`

* **重複訂購機率自訂購以來的指定月份**
* 量度A：重複訂購間隔月數（隱藏）
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 量度B：按訂購後月份的最後訂單（隱藏）
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 量度C：所有時間重複訂單（隱藏）
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 

   [！UICONTROL分組依據]: `Independent`

* 量度D：所有上次訂單（隱藏）
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 

   [！UICONTROL分組依據]: `Independent`

* [!UICONTROL Formula]：初始重複順序機率
* 
   [！UICONTROL公式]: `(C-A)/(C+D-A-B)`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Months since previous order`
* 顯示top.bottom：前24個類別，依類別名稱排序

* 

   [!UICONTROL Chart type]: `Line`

初始重複訂購機率報表代表「重複訂購總數/訂購總數」。 每個訂單都是產生重複訂單的機會；重複訂單的數量是實際發生的訂單的子集。

您使用的公式將簡化為（X個月後發生的重複訂單總數）/ （至少X個月前的訂單總數）。 它會顯示過去，由於自訂單以來已有X個月，使用者下其他訂單的可能性為Y%。

當您建置控制面板後，最常見的問題就是：如何使用此設定來判斷流失臨界值？

**對此沒有「一個正確的答案」。** 不過，Adobe建議找出線條與初始重複機率一半的值相交的點。 這時您可以說「如果使用者要重複訂單，他們現在可能已經完成了。」 最終目標是選取從「保留」切換為「重新啟用」是可行的臨界值。

編譯所有報表後，您可以視需要在控制面板上組織報表。 結果看起來可能像頁面頂端的影像

如果您在建立此分析時遇到任何問題，或只是想與Professional Services團隊互動， [聯絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
