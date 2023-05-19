---
title: 行銷ROI
description: 瞭解如何設定儀表板來追蹤您的管道分析，包括彙總的ROI和依行銷活動。
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# 行銷ROI

>[!NOTE]
>
>本主題包含使用原始架構和新架構的使用者端指示。 您位於 [新架構](../../administrator/account-management/new-architecture.md) 如果您在從主工具列選取「管理資料」後，有「Data Warehouse檢視」區段可用。

如果您正線上上廣告上花錢，您想要追蹤此花費的回報，並針對進一步的投資做出資料導向式決策。 此主題示範如何設定控制面板來追蹤您的管道分析，包括彙總和依促銷活動的ROI。

![](../../assets/Marketing_dashboard_example.png)

開始之前，您想要連線 [!DNL [Facebook Ads]](../importing-data/integrations/facebook-ads.md)， [!DNL [Adwords]](../importing-data/integrations/google-adwords.md)、和 [!DNL [Google Ecommerce]](../importing-data/integrations/google-ecommerce.md) 帳戶，並帶入任何其他線上廣告支出資料。 此分析包含 [進階計算欄](../data-warehouse-mgr/adv-calc-columns.md).

## 整合的表格

**原始架構：** 集合來自各種來源的支出，例如 [!DNL Facebook Ads] 或 [!DNL Google Adwords]，Adobe建議建立 **合併的表格** 所有廣告支出。 您需要分析人員為您完成此步驟。 如果您沒有， [提出支援要求](../../guide-overview.md#Submitting-a-Support-Ticket) 與主旨 `[MARKETING ROI ANALYSIS]`，分析師會建立此表格。

**新架構：** 您可以依照以下範例操作： [此分析資料庫](../../data-analyst/data-warehouse-mgr/create-dw-views.md) 主題。 在新架構中，整合表格現在稱為Data Warehouse檢視。

## 計算欄

要建立的欄

* **`Consolidated Digital Ad Spend`** 表格
* **`Campaign name`** 由Adobe分析人員建立，作為您的一部分 **[行銷ROI分析]** 票證

**原始架構與新架構：**

* **`sales_flat_order`** 表格
   * **`Order's GA campaign`**
      * 選取定義： `Joined Column`
      * [!UICONTROL Create Path]:
      * 
         [!UICONTROL Many]: `sales_flat_order.increment_id`
      * 

         [!UICONTROL One]: `ecommerce####.transaction_id`

      * 選取 [!UICONTROL table]： `ecommerce####`
      * 選取 [!UICONTROL column]： `campaign`
      * [!UICONTROL Path]: `sales_flat_order.increment_id = ecommerce#####.transactionID`
   * **`Order's GA medium`**
      * 選取定義：聯結資料行
      * 選取 [!UICONTROL table]： `ecommerce####`
      * 選取 [!UICONTROL column]： `medium`
      * [!UICONTROL Path]： sales_flat_order.increment_id = e-commerce#####.transactionId
   * **`Order's GA source`**
      * 選取定義：聯結資料行
      * 選取 [!UICONTROL table]： `ecommerce####`
      * 選取 [!UICONTROL column]： `source`
      * [!UICONTROL Path]： sales_flat_order.increment_id = e-commerce####.transactionId ^



* **`customer_entity`** 表格
* **`Customer's first order GA campaign`**
   * 選取定義： `Max`
   * 選取 [!UICONTROL table]： `sales_flat_order`
   * 選取 [!UICONTROL column]： `Order's GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA source`**
   * 選取定義： `Max`
   * 選取 [!UICONTROL table]： `sales_flat_order`
   * 選取 [!UICONTROL column]： `Order's GA source`
   * [!UICONTROL Path]： sales_flat_order.customer_id = customer_entity.entity_id
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA medium`**
   * 選取定義： `Max`
   * 選取 [!UICONTROL table]： `sales_flat_order`
   * 選取 [!UICONTROL column]： `Order's GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`sales_flat_order`** 表格
* **`Customer's first order GA campaign`**
   * 選取定義： `Joined Column`
   * 選取 [!UICONTROL table]： `customer_entity`
   * 選取 [!UICONTROL column]： `Customer's first order GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
   * 選取定義：聯結資料行
   * 選取 [!UICONTROL table]： `customer_entity`
   * 選取 [!UICONTROL column]： `Customer's first order GA source`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
   * 選取定義： `Joined Column`
   * 選取 [!UICONTROL table]： `customer_entity`
   * 選取 [!UICONTROL column]： `Customer's first order GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

## 量度

* **廣告支出**
* 在 **`Consolidated Digital Ad Spend`** 表格
* 此量度會執行 **總和**
* 於 **`adCost`** 欄
* 排序依據： **`date`** timestamp

* **廣告印象**
* 在 **`Consolidated Digital Ad Spend`** 表格
* 此量度會執行 **總和**
* 於 **`Impressions`** 欄
* 排序依據： **`Month`** timestamp

* **廣告點按次數**
* 在 **`Consolidated Digital Ad Spend`** 表格
* 此量度會執行 **總和**
* 於 **`adClicks`** 欄
* 排序依據： **`Month`** timestamp

>[!NOTE]
>
>請確定 [將所有新欄新增為量度的維度](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 建立新報表之前。

## 報表

* **廣告支出（所有時間）**
   * [!UICONTROL Metric]：廣告支出

* 量度 `A`：廣告支出
* [!UICONTROL Time period]: `All time`
* 
   [！UICONTROL間隔]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **廣告客戶贏取（所有時間）**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 篩選邏輯： ([`A`] 或 [`B`] 或 [`C`])和 [`D`]

* 量度 `A`： `Ad customer acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [！UICONTROL間隔]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **廣告ROI**
   * [!UICONTROL Metric]：廣告支出

   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 篩選邏輯： ([`A`] 或 [`B`] 或 [`C`])和 [`D`]
   * [!UICONTROL Metric]：平均期限收入
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 篩選邏輯： ([`A`] 或 [`B`] 或 [`C`])和 [`D`]
   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 

      [!UICONTROL Format]: `Percentage`



* 量度 `A`： `Ad Spend (hide)`
* 量度 `B`： `Ad customer acquisitions (hide)`
* 量度 `C`： `Average LTV (hide)`
* [!UICONTROL Formula]: `Ads ROI`
* [!UICONTROL Time period]: `All time`
* 
   [！UICONTROL間隔]: `None`
* 

   [!UICONTROL Chart Type]: `Scalar`

* **按Ga媒體顯示的訂單**
   * 

      [！UICONTROL公制]: `Orders`

* 量度 `A`： `Orders`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Order's medium`
* 

   [!UICONTROL Chart Type]: `Area`

* **依行銷活動的廣告ROI**
   * [!UICONTROL Metric]: `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 篩選邏輯： ([`A`] 或 [`B`] 或 [`C`])和 [`D`]
   * [!UICONTROL Metric]：平均期限收入
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 篩選邏輯： ([`A`] 或 [`B`] 或 [`C`])和 [`D`]
   * [!UICONTROL Metric]：平均期限訂單數
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * 篩選邏輯： ([`A`] 或 [`B`] 或 [`C`])和 [`D`]
   * [!UICONTROL Formula]: `(A / B)`
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `(C - (A / B))`
   * 

      [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 

      [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric]: `Ad Clicks`

   * [!UICONTROL Metric]: `Ad Impressions`

   * [!UICONTROL Formula]: `(H / I)`
   * 

      [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Formula]: `(A / H)`
   * 

      [!UICONTROL Format]: `Currency`




* 量度 `A`： `Ad Spend` （隱藏）
* 量度 `B`： `Ad customer acquisitions`
* 量度 `C`： `Average LTV`
* 量度 `D`： `Average lifetime # of orders`
* 
   [！UICONTROL公式]: `CAC`
* [!UICONTROL Formula]: `Avg return`
* [!UICONTROL Formula]: `Ads ROI`
* 量度 `H`： `adClicks`
* 量度 `I`： `Impressions`
* 
   [！UICONTROL公式]: `CTR`
* 
   [！UICONTROL公式]: `CPC`
* [!UICONTROL Time period]: `All time`
* 
   [！UICONTROL間隔]: `None`
* 
   [！UICONTROL分組依據]: `campaign` (將「客戶的第一個訂單」行銷活動用於非廣告支出表格量度)
* 

   [!UICONTROL Chart Type]: `Table`

如果您在建立此分析時遇到任何問題，或只是想與Professional Services團隊互動， [聯絡支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

### 相關

* [中的UTM標籤最佳作法 [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [如何 [!DNL Google Analytics] UTM歸因是否有效？](../analysis/utm-attributes.md)
