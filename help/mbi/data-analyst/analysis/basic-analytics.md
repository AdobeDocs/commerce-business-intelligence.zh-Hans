---
title: 瞭解並建置基本分析
description: 瞭解如何瞭解和建立基本分析。
exl-id: 23cea7b3-2e66-40c3-b4bd-d197237782e3
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '3113'
ht-degree: 0%

---

# 基本Analytics

在您熟悉 [!DNL Adobe Commerce Intelligence] 平台且對該工具有基本的瞭解，您會想要開始建立報告。 您最常見的問題之一可能是「我應該看看什麼？」

以下資訊概述您可能認為有價值的一些常見量度和報表。 這些報表中有些會存在於您的帳戶內，因此請務必檢視存在於您帳戶內的量度和報表，以避免產生重複專案。

## 您想要瞭解的表格和欄

建立量度時，您需要知道四項資訊：

1. 資料所在的表格，
1. 您要執行的特定動作，
1. 您要對其執行此動作的欄，以及
1. 您要用來追蹤該資料的時間戳記。

最有可能的情況是，這些範例中使用的表格名稱與資料庫中的欄和表格名稱稍有不同，因為每個資料庫都是唯一的。 如果您需要識別資料庫中對應表格或欄的協助，請參考以下定義。

## Customers表格

此表格包含每個客戶的關鍵資訊，例如唯一的客戶ID、電子郵件地址等。 以下範例使用 **[!UICONTROL customer_entity]** 作為範例customer表格的名稱。

如果您的資料庫中目前不存在這些計算中的某些專案，則您帳戶中的任何管理員使用者都可以建立它們。 此外，您也要確定這些維度可群組至所有適用的量度。

**Dimension**

* **[!UICONTROL Entity_id]**：每個客戶的唯一識別碼。 這也可能是不重複的客戶號碼或客戶電子郵件地址，應作為您訂單表格的參考金鑰。
* **[!UICONTROL Created_at]**：建立客戶帳戶並將其新增至資料庫的日期。
* **[!UICONTROL Customer's lifetime revenue]**：客戶產生的總期限收入。
* **[!UICONTROL Customer's first 30-day revenue]**：客戶在前30天產生的收入總額。
* **[!UICONTROL Customer's lifetime number of orders]**：客戶在其存留期內下單的訂單數。
* **[!UICONTROL Customer's lifetime number of coupons]**：客戶在其存留期內使用的抵用券總數。
* **[!UICONTROL Customer's first order date]**：客戶第一筆訂單的日期。 如果客戶在建立時沒有下訂單，這可能與created_at日期不同。

**您接受客服訂單嗎？**

*若是如此，此表格可能不會包含您的所有客戶。 聯絡 [支援團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 以確保您的客戶分析包括所有客戶。*

*不確定您是否接受來賓訂單？ 請參閱 [此主題](../data-warehouse-mgr/guest-orders.md) 以進一步瞭解！*

## 訂單表格

在此表格中，每一列代表一個順序。 此表格中的欄包含每個訂單的基本資訊，例如訂單的ID、建立日期、狀態、下訂單的客戶的ID等。 以下範例使用 **[!UICONTROL sales_flat_order]** 作為範例訂單表格的名稱。

**Dimension**

* **[!UICONTROL Customer_id]**：下訂單之客戶的唯一識別碼。 這通常用於在customer和orders表格之間移動資訊。 在這些範例中，您預期的customer_id **[!UICONTROL sales_flat_order]** 對齊的表格 **[!UICONTROL entitiy_id]** 於 **[!UICONTROL customer_entity]** 表格。
* **[!UICONTROL Created_at]**：建立或下訂單的日期。
* **[!UICONTROL Customer_email]**：下訂單的客戶的電子郵件地址。 這也可能是客戶的唯一識別碼。
* **[!UICONTROL Customer's lifetime number of orders]**：在您的欄上具有相同名稱的欄副本 `Customers` 表格。
* **[!UICONTROL Customer's order number]**：與訂單相關聯的客戶連續訂單編號。 例如，如果您檢視的資料列是客戶的第一筆訂單，此欄位會顯示「1」；但如果這是客戶的第十五筆訂單，此欄位會針對此訂單顯示「15」。 如果此維度不存在於您的 `Customers` 表格，詢問 [支援團隊](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 協助您建置。
* **[!UICONTROL Customer's order number (previous-current)]**：中兩個值的串連 **[!UICONTROL Customer's order number]** 欄。 它用於以下範例報表中，以顯示任意兩筆訂單之間經過的時間。 例如，在此計算中，客戶第一次訂購日期與第二次訂購日期之間的時間表示為「1-2」。
* **[!UICONTROL Coupon_code]**：顯示每個訂單使用了哪些抵用券。
* **[!UICONTROL Seconds since previous order]**：客戶訂單之間的時間（秒）。

## 「訂購專案」表格

在此表格中，每一列代表售出的一件商品。 此表格包含每個訂單中銷售之料號的相關資訊，例如訂單參考編號、產品編號、數量等。 以下範例使用 `sales_flat_order_item` 作為範例訂單專案表格的名稱。

**Dimension**

* **[!UICONTROL Item_id]**：表格中每一列的唯一識別碼。
* **[!UICONTROL Order_id]**：參考金鑰至 `Orders` 此表格會說明哪些專案是以相同訂單購買的。 如果訂單包含多個專案，則會重複此值。
* **[!UICONTROL Product_id]**：如果您想要瞭解所購買特定產品的相關資訊（例如顏色、大小等），可以使用此欄從產品表格中擷取該資訊。
* **[!UICONTROL Order's created_at]**：下訂單的時間戳記，通常會複製到 `order line items` 表格來自 `Orders` 表格。
* **[!UICONTROL Order's coupon_code]**：類似於 `Order's created_at` 維度，此欄是從您的訂單表格複製而來。

## 訂閱表格

此表用於管理您的訂閱資訊，例如訂閱ID、訂閱者的電子郵件地址、訂閱開始日期等。

**Dimension**

* **[!UICONTROL Customer_id]**：下訂單之客戶的唯一識別碼。 這是在Customers表格和Orders表格之間建立路徑的常見方式。 在這些範例中，您預期的customer_id **sales_flat_order** 對齊的表格 `entitiy_id` 於 `customer_entity` 表格。
* **[!UICONTROL Start date]**：客戶開始訂閱的日期。

## 行銷支出表格

分析行銷支出時，您可以包含 [!DNL Facebook]， [!DNL Google AdWords]或分析中的其他來源。 如果您有多個行銷支出來源，請聯絡 [Managed Services團隊](https://business.adobe.com/products/magento/fully-managed-service.html) 以取得為行銷活動設定整合表格的協助。

**Dimension**

* **[!UICONTROL Spend]**：廣告總支出。 在 [!DNL Facebook]，這將是 `facebook_ads_insights_####` 表格。 對象 [!DNL Google AdWords]，這將會是 `adCost` 中的欄 `campaigns####` 表格。
* 此 `####` 附加到每個表格的與您的帳戶ID相關 [!DNL Facebook] 或 [!DNL Google AdWords] 帳戶。
* **[!UICONTROL Clicks]**：點按總數。 在 [!DNL Facebook]，這將會是 `facebook_ads_insights_####` 表格。 在 [!DNL Google AdWords]，這將會是 `campaigns####` 表格。
* **[!UICONTROL Impressions]**：曝光總數。 在 [!DNL Facebook]，這是以下專案中的曝光次數： `facebook_ads_insights_####` 表格。 在 [!DNL Google AdWords]，這表示此頁面的 `campaigns####` 表格。
* **[!UICONTROL Campaign]**：點按總數。 在 [!DNL Facebook]，這將會是 `facebook_ads_insights_####` 表格。 在 [!DNL Google AdWords]，這將是 `campaigns####` 表格。
* **[!UICONTROL Date]**：特定行銷活動發生活動（支出、點按或曝光數）的時間和日期。 在 [!DNL Facebook]，這將會是 `date_start` 中的欄 `facebook_ads_insights_####` 表格。 在 [!DNL Google AdWords]，這將會是 `campaigns####` 表格。
* **[!UICONTROL Customer's first order's source]**：來自客戶第一筆訂單的訂單來源。 首先，檢查您是否有名為的欄 `customer's first order's source` 在您的帳戶中。 如果您沒有看到此欄，可以使用這些指示建立所需的欄。
* **[!UICONTROL Customer's first order's medium]**：來自客戶第一筆訂單的訂單媒體。 首先，檢查您是否有名為的欄 `customer's first order's source` 在您的帳戶中。 如果您沒有看到此欄，可以使用這些指示建立所需的欄。
* **[!UICONTROL Customer's first order's campaign]**：來自客戶第一筆訂單的訂單行銷活動。 首先，檢查您是否有名為的欄 `customer's first order's source` 在您的帳戶中。 如果您沒有看到此欄，可以使用這些指示建立所需的欄。

## 常見報表和量度

以下是一些您可能會覺得實用的常見報表和量度範例：

* [Customer Analytics](#customeranalytics)
* [Order Analytics](#orderanalytics)
* [行銷支出分析](#mktgspendanalytics)

## 客戶分析 {#customeranalytics}

### 新使用者

* **說明**：指定期間內新獲得的使用者總數的計數。 `New Users` 不同於 `Unique Customers`，因為 `New Users` 具有使用您的服務建立帳戶的時間戳記（這並不意味著他們一定下了訂單），當 `Unique Customers` 已下至少一份訂單。
* **量度定義**：此量度會執行 **計數** 之 `entity_id` 從 `customer_entity` 表格排序依據 `created_at`.
* **報表範例**：上個月建立的新使用者數目
   * **[!UICONTROL Metric]**: `New Users`
   * **[!UICONTROL Time Range]**: `Last Month`
   * **[!UICONTROL Time Interval]**: `By Day`

![新使用者](../../assets/New_Users_Last_Month.png)<!--{: width="929"}-->

### 不重複客戶

* **說明**：指定期間內不同客戶的總數。 這與 `New Users`，因為它只會追蹤已下最少一張訂單的客戶。 不同的客戶報表只會追蹤客戶在指定時間間隔內的一次。 如果您將時間間隔設為 `By Day` 而客戶當天購買多次，則客戶只會被計算一次。 如果您想檢視一般購買總數，請檢視 `Number of Orders`.
* **量度定義**：此量度會執行 **相異計數** 之 `customer_id` 從 `sales_flat_order` 表格排序依據 `created_at`.
* **報表範例**：過去90天各周的不同客戶
   * **[!UICONTROL Metric]**: `Distinct Customers`
   * **[!UICONTROL Time Range]**: `Moving range > Last 90 Days`
   * **[!UICONTROL Time Interval]**: `By Day`

![不重複客戶。](../../assets/Unique_customers_last_7_days.png)<!--{: width="929"}-->

### 新訂閱者

* **說明**：在指定期間內獲得的新訂閱者總數的計數。
* **量度定義**：此量度會執行 **相異計數** 之 `customer_id` 從 `subscriptions` 表格排序依據 `start_date`.
* **報表範例**：今年新的訂閱者（按月）
   * **[!UICONTROL Metric]**: `New Subscribers`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 0 Days Ago`
   * **[!UICONTROL Time Interval]**: `By Month`

![訂閱者](../../assets/New_Subscribers_This_Year_by_Month.png)<!--{: width="929"}-->

### 回頭客戶

* **說明**：一段時間內下多筆訂單的客戶總數。 在重複客戶報表中，您可以使用 `Distinct Customers` 量度和 `Customer's Order Number` 來自您的的維度 `orders` 表格。
* **使用的量度**： `Distinct Customers`
* **報表範例**：去年進行的第2次和第3次購買數目
   * **[!UICONTROL Metric]**: `Distinct Customers`
   * **[!UICONTROL Time Range]**: `Moving Range > Last Year`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Group By]**： `Customer's Order Number`，然後選取 `2` 和 `3`

   ![](../../assets/2nd_and_3rd_purchases_last_year.png)

* **報表範例2**：去年的重複客戶數
   * **[!UICONTROL Metric]**: `Distinct Customers`
   * **[!UICONTROL Filters]**: `Customer's Order Number Greater Than 1`
   * **[!UICONTROL Time Range]**: `Moving range > Last Year`
   * **[!UICONTROL Time Interval]**: `By Month`

   ![去年回頭客戶](../../assets/Repeat_customers_last_year.png)<!--{: width="929"}-->

### 依期限訂單數排名的前幾個客戶

* **說明**：根據訂單總數的頂級客戶清單。 這可讓您直接列出最常光顧的購物者。
* **使用的量度**： `Orders`
* **報表範例**：依期限訂單數的前25名客戶
   * **[!UICONTROL Metric]**: `Orders`
   * **[!UICONTROL Time Range]**: `All Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `customer_email`
   * **[!UICONTROL Show Top/Bottom]**：依訂單排序的前25項

   ![前25名客戶（依訂單）](../../assets/Top_25_customers_by_lifetime_orders.png)<!--{: width="929"}-->

### 依期限收入排名的前幾個客戶

* **說明**：根據期限收入排名在前的客戶清單。
* **使用的量度**： `Average Lifetime Revenue`
* **報表範例**：依期限收入的前25名客戶
   * **[!UICONTROL Metric]**: `Average Lifetime Revenue`
   * **[!UICONTROL Time Range]**: `All time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `customer_email`
   * **[!UICONTROL Show Top Bottom]**：依期限收入排序的前25項

   ![前25名客戶（依收入）](../../assets/top_25_customers_by_lifetime_revneue.png)<!--{: width="929"}-->

### 依同類群組的平均期限收入

* **說明**：追蹤 [不同同類群組的平均期限收入](../dev-reports/lifetime-rev-cohort-analysis.md) 使用者在一段時間內的數量，以找出表現最佳的同類群組。 同類群組會依一般日期（例如首次訂購日期或建立日期）分組。
* **使用的量度**： `Revenue`
* **報表範例**：依同類群組的平均客戶期限收入
   * **[!UICONTROL Metric]**: `Revenue`
   * **[!UICONTROL Cohort Date]**: `Customer's first order date`
   * **[!UICONTROL Time Interval]**: `Month`
   * **[!UICONTROL Time Period]**：使用至少四個月的資料移動最近八個同類群組中的一組同類群組
   * **[!UICONTROL Duration]**: `12 Month(s)`
   * **[!UICONTROL Table]**: `Customer_entity`
   * **[!UICONTROL Perspective]**：每個同類群組成員的累積平均值

   ![依同類群組的客戶期限收入](../../assets/Avg_customer_lifetime_revenue_by_cohort.png)<!--{: width="929"}-->

### 依優惠券使用情況區分的客戶

* **說明**：已取得且使用優惠券/折扣代碼的客戶數量計數。 這可協助您清楚瞭解折扣買家與全價購買者的差異。
* **使用的量度**： `New Users`
* **報表範例**：依月份區分的優惠券與非優惠券客戶
   * **[!UICONTROL Metric A]**: `Non coupon customers`
   * **[!UICONTROL Metric]**: `New Users`
   * **[!UICONTROL Filters]**：大於0的客戶期限訂單數和等於0的客戶期限優惠券數
   * **[!UICONTROL Metric B]**: `Coupon customers`
   * **[!UICONTROL Metric]**: `New Users`
   * **[!UICONTROL Filters]**：大於0的客戶期限訂單數和大於0的客戶期限優惠券數
   * **[!UICONTROL Time range]**: `All Time`
   * **[!UICONTROL Time interval]**: `By Month`

   ![依優惠券使用情況劃分的客戶](../../assets/Customers_by_coupon_usage.png)<!--{: width="929"}-->

* **報表範例2**：按月的優惠券與非優惠券客戶的百分比
   * **[!UICONTROL Metric A]**： `Non coupon customers` （隱藏量度）
      * **[!UICONTROL Metric]**: `New Users`
      * **[!UICONTROL Filters]**： `Customer's Lifetime Number of Orders Greater Than 0` 和 `Customer's Lifetime Number of Coupons Equal to 0`
   * **[!UICONTROL Metric B]**: `Coupon customers`
      * **[!UICONTROL Metric]**: `New Users`
      * **[!UICONTROL Filters]**： `Customers Lifetime Number of Orders Greater Than 0` 和 `Customer's Lifetime Number of Coupons Greater Than 0`
   * **[!UICONTROL Time Range]**: `All Time`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Formula]**: `B/(A+B)`

>[!NOTE]
>
> **隱藏所有量度**

![優惠券使用方式](../../assets/Customers_by_coupon_usage_formula.png)<!--{: width="929"}-->

### 平均前30天收入

* **說明**：客戶在其作為客戶的前30天內產生的平均收入額。
* **量度說明**：此量度會執行 **平均** 之 `Customer's First 30 Day Revenue` 從 `customer_entity` 表格排序依據 `created_at`.
* **報表說明**：客戶前30天收入的所有時間平均值
* **[!UICONTROL Metric]**: `Average First 30 Day Revenue`
* **[!UICONTROL Time Range]**: `All Time`
* **[!UICONTROL Time Interval]**: `None`

![平均前30天收入](../../assets/Avg_first_30_day_revenue.png)<!--{: width="929"}-->

### 平均客戶期限收入

* **說明**：客戶在其期限內的平均收入額。
* **量度說明**：此量度會執行 **平均** 的 `Customer's Lifetime Revenue` 上的欄 `customer_entity` 表格根據 `created_at`.
* **報表說明**：客戶期限收入的所有時間平均值
   * **[!UICONTROL Metric]**: `Average Customer Lifetime Revenue`
   * **[!UICONTROL Time Range]**: `All Time`
   * **[!UICONTROL Time Interval]**: `None`

![客戶期限收入](../../assets/Avd_customer_lifetime_revenue_.png)<!--{: width="929"}-->

## 訂單分析 {#orderanalytics}

### 收入

* **說明**：收入量度會顯示所選時段內所賺取的總收入。
* 此量度會執行 **sum** 之 `grand_total` 從 `sales_flat_order` 表格排序依據 `created_at`.
* **報表範例**：按月份、YTD列出的收入
   * **[!UICONTROL Metric]**: `Revenue`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **時間間隔**： `By Month`

>[!TIP]
>
>確保您的收入量度的計算與您內部討論的定義一致。 例如，您可能想要計算已出貨訂單的收入、換算不同區域的幣別或排除稅捐。 此外，您也可以使用 [篩選器集](../../data-user/reports/ess-manage-data-filters.md) 以確保在同一個表格上建立的所有量度的一致性。

![收入](../../assets/revenue.png)<!--{: width="929"}-->

### 訂購

* **說明**：指定期間內的訂單總數計數。 「訂單」報表會追蹤因新產品、促銷活動或其他任何可能增加（或減少）交易量所導致的訂單量變更。 您通常可能想要依某些變數將此量度細分，以回答您的問題。
* **量度定義**：此量度會執行 **計數** 之 `entity_id` 從 `sales_flat_order` 表格排序依據 `created_at`.
* **報表範例**：按月份、年累計的訂單
   * **[!UICONTROL Metric]**: `number of orders`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Month`

>[!TIP]
>
>就像收入量度一樣，您應具有 [篩選器集](../../data-user/reports/ess-manage-data-filters.md) 用來排除不完整、測試或傳回的訂單。

![訂購](../../assets/orders_pic.png)<!--{: width="929"}-->

### 訂購的產品

* **說明**：訂購的產品量度會告訴您特定時段內售出的專案數量。
* **量度定義**：此量度會執行 **sum** 之 `qty_ordered` 從 `sales_flat_order_item` 表格排序依據 `created_at`.
* **報表範例**：依月份、年度累計的售出專案
   * **[!UICONTROL Metric]**: `Products ordered`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Month`

   ![訂購的產品](../../assets/products_ordered_pic1.png)<!--{: width="929"}-->

* 將此量度與您的訂單數量量度結合，以計算每筆訂單的專案數量。 接下來，將優惠券代碼新增至報表，以判斷您的促銷活動對購物車大小有何影響，或依新訂單與重複訂單進行細分，以便更清楚瞭解您的客戶行為。
* **報表範例**：每筆訂單的產品：第一筆訂單與重複訂單
   * **[!UICONTROL Metric A]**：訂購的產品：第一筆訂單
      * **[!UICONTROL Metric]**: `Products ordered`
      * **[!UICONTROL Filter]**: `Customer's order number = 1`
   * **[!UICONTROL Metric B]**：訂購：第一筆訂購
      * **[!UICONTROL Metric]**: `Orders`
      * **[!UICONTROL Filter]**: `Customer's order number = 1`
   * **[!UICONTROL Metric C]**：訂購的產品：重複訂購
      * **[!UICONTROL Metric]**: `Products ordered`
      * **[!UICONTROL Filter]**: `Customer's order number > 1`
   * **[!UICONTROL Metric D]**：訂購：重複訂購
      * **[!UICONTROL Metric]**: `Orders`
      * **[!UICONTROL Filter]**: `Customer's order number > 1`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Week`
   * **[!UICONTROL Formula 1]**: `A/B`
   * **[!UICONTROL Formula 2]**: `C/D`

>[!NOTE]
>
>取消勾選 `Multiple Y-Axes box` 和 `Hide` 所有量度

![訂購的產品2](../../assets/products_ordered_pic2.png)<!--{: width="929"}-->

### 平均訂購值

* **說明**：追蹤一段期間內下訂單的平均值。 使用此量度可快速判斷您的平均訂購值(AOV)如何因您的行銷工作、產品和/或業務的其他變更而波動。
* **量度定義**：此量度會執行 **平均** 之 `grand_total` 從 `sales_flat_order` 表格排序依據 `created_at`.
* **報表範例**： AOV與上一年度、YTD
   * **[!UICONTROL Metric]**: `Average order value`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Perspective]**: `Amount Change vs Previous Year`

   ![AOV](../../assets/aov_pic.png)<!--{: width="929"}-->

### 最多購買含優惠券的產品

* **說明**：此報表可讓您深入瞭解當您提供促銷活動或優惠券時售出哪些產品。
* **使用的量度**：訂購的產品
* **報表範例**：以優惠券購買次數最多的產品
   * **[!UICONTROL Metric]**: `Products ordered`
   * **[!UICONTROL Filter]**: `Order's coupon_code Is Not \[NULL\]`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By**]： `name` (或 `SKU`或任何其他產品識別碼)
   * **[!UICONTROL Show top/bottom]**：依訂購的產品排序的前25項

   ![優惠券產品](../../assets/prod_coupons_pic.png)<!--{: width="929"}-->

### 訂單之間的時間

* **說明**：使用測試測試您對客戶購買週期的假設和期望 **訂單之間的時間** 分析會檢視平均值（或中位數！） 購買間隔時間。 在下圖中，您可以看到您的最佳客戶（下超過3筆訂單的客戶）在不到六個月的時間裡完成第二次購買。 尚未下第四筆訂單的客戶，會在第二次購買前等待14個月。
* **量度定義**：此量度會執行 **平均** 之 `Time since previous order` 從 `sales_flat_order` 排序者 `created_at`.
* **報表範例**：
   * **量度1**：≤3筆訂單
      * **[!UICONTROL Metric]**: `Average time between orders`
      * **[!UICONTROL Filter]**: `Customer's lifetime number of orders ≤ 3`
   * **量度2**： > 3個訂單
      * **[!UICONTROL Metric]**: `Average time between orders`
      * **[!UICONTROL Filter]**: `Customer's lifetime number of orders > 3`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**:` Customer's order number (previous-current)`

>[!NOTE]
>
>取消勾選 `Multiple Y-Axes` 方塊。

![訂單之間的時間](../../assets/time_bw_orders_pic.png)<!--{: width="929"}-->

## 行銷支出分析 {#mktgspendanalytics}

### 廣告支出

* **說明**：您可以依行銷活動、廣告集或其他區段，分析不同時段和間隔的行銷支出。
* **量度定義**：此量度會在中的支出欄執行總和 `Marketing Spend` 表格排序依據 `date` 欄。
* **報表範例**：按行銷活動分類的廣告支出
   * **[!UICONTROL Metric]**: `Ad spend`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `campaign`

![廣告支出](../../assets/ad_spend.png)<!--{: width="929"}-->

### 廣告曝光次數和廣告點按次數

* **說明**：除了分析廣告支出之外，您還可以分析廣告曝光次數和廣告點按次數。
* **量度定義**：此量度會在的「曝光數」 （或「點按數」）欄上執行總和。 `Marketing Spend` 依日期欄排序的表格。
* **報表範例**：依日期新增曝光次數和廣告點按次數
   * **[!UICONTROL Metric A]**: `Ad impressions`
   * **[!UICONTROL Metric B]**: `Ad clicks`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 3 Months Ago`
   * **[!UICONTROL Time Interval]**: `By Day`

   ![廣告曝光次數](../../assets/ad_impressions.png)<!--{: width="929"}-->

### 點進率(CTR)

* **說明**：使用您上述建立的廣告曝光次數和廣告點按次數量度，您可以依不同促銷活動在一段時間內分析點進率。
* **報表範例**：CTR （依促銷活動）
   * **[!UICONTROL Metric A]**: `Ad impressions`
   * **[!UICONTROL Metric B]**: `Ad clicks`
   * **[!UICONTROL Time Range]**:`All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `B/A`
   * 選取 `%` 選項。
   * **[!UICONTROL Group By]**: `campaign`

>[!NOTE]
>
>您可以 **標題** 公式為 `CTR`、和 **隱藏** 所有量度。

![CTR](../../assets/CTR.png)<!--{: width="929"}-->

### 每次點按成本(CPC)

* **說明**：使用您在上面建立的廣告支出和廣告點按次數量度，您可以依不同促銷活動在一段時間內分析您的每次點按成本。
* **報表範例**：各促銷活動的CPC
   * **[!UICONTROL Metric A]**: `Ad spend`
   * **[!UICONTROL Metric B]**: `Ad clicks`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `A/B`
   * 選取 `currency` option
   * **[!UICONTROL Group By]**: `campaign`

>[!NOTE]
>
>您可以 **標題** 公式為 `CPC`、和 **隱藏** 所有量度。

![CPC](../../assets/CPC.png)<!--{: width="929"}-->

### 依贏取來源劃分的客戶

* **說明**：如果您使用追蹤訂單的來源、媒體及行銷活動 [!DNL Google eCommerce]，您可以依客戶的贏取來源來分析客戶。 這可協助您識別哪些行銷來源正在爭取客戶，並回答下列問題：「您的大多數客戶都是透過以下方式發出第一筆訂單 [!DNL Google]， [!DNL Facebook]，還是其他來源？」
* **報表範例**：依贏取來源劃分的客戶
   * **[!UICONTROL Metric Used]**: `New Customers`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Group By]**: `Customer's first order's source`

>[!NOTE]
>
>簽出 [本文](../analysis/most-value-source-channel.md) 以取得使用贏取來源的更多報表範例。

![贏取來源](../../assets/acquisition_source.png)<!--{: width="929"}-->

### 依贏取媒體和贏取促銷活動劃分的客戶

* **說明**：與依贏取來源分析客戶類似，您也可以依客戶的首次訂單媒體與促銷活動來分析客戶。 這可協助您回答「哪些行銷活動吸引新客戶？」等問題。
* **報表範例**：使用付費媒體依據贏取促銷活動的客戶
   * **[!UICONTROL Metric Used]**: `New customers`
   * **[!UICONTROL Filter]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `Customer's first order's campaign`

>[!NOTE]
>
>對於中的篩選器 `New Customers` 量度，您可以新增任何被視為您業務「付費」媒介的其他媒介，例如cpc或付費搜尋。

![贏取媒體](../../assets/acquisition_medium.png)<!--{: width="929"}-->

### 客戶採購成本(CAC)或每次採購成本(CPA)

* **說明**：分析行銷活動成本的一種方式是，將所有成本僅歸因至您透過行銷活動取得的客戶。
* **報表範例**：各促銷活動的CAC
   * **[!UICONTROL Metric A]**: `New customers`
   * **[!UICONTROL Filter]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**: `Ad Spend`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `B/A`
   * 選取 `currency` option
   * **[!UICONTROL Group By]**:
      * 針對量度 `A`，選取 `Customer's first order's campaign`
      * 針對量度 `B`，選取 `campaign`

   ![新使用者。](../../assets/New_Users_Last_Month.png)

>[!NOTE]
>
>您可以 **標題** 公式為 `CTR`、和 **隱藏** 所有量度。 另外，請出庫 [本文](../analysis/roi-ad-camp.md) 以取得詳細資訊。

![CAC 1](../../assets/New_Users_Last_Month.png)

![CAC 2](../../assets/cac-2.png)

### 依贏取來源、媒體和促銷活動區分的期限值

* **說明**：除了分析每個促銷活動取得的客戶數量之外，您還可以分析這些客戶的平均期限收入。 這可協助您識別：
   * 如果特定行銷活動吸引大量客戶，但這些客戶的期限值較低。
   * 如果特定行銷活動吸引的客戶數量偏低，但這些客戶具有高的期限值。
* **報表範例**：先新增 `New customers` 量度。 然後，新增 `Average lifetime revenue` 量度。 選取想要的時間範圍，然後選擇 `interval` 作為 `None`. 最後，選取 `group by` 選項為`Customer's first order's campaign`.
   * **[!UICONTROL Metric A]**: `New Customers`
   * **[!UICONTROL Filter A]**： `Customer's first order's source` 喜歡&#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**: `Average lifetime revenue`
   * **[!UICONTROL Filter A]**： `Customer's first order's source` 喜歡&#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `Customer's first order's campaign`

>[!NOTE]
>
>對於這兩個篩選器，您可以新增任何其他被視為您企業「付費」媒體的媒體（例如cpc或付費搜尋）。 您也可以新增您要分析的任何其他來源，例如Facebook。 簽出 [本文](../analysis/roi-ad-camp.md) 以取得有關CAC、LTV和ROI的詳細資訊。

![依贏取來源、媒體和促銷活動區分的期限值](../../assets/LTV_2.png)<!--{: width="929"}-->

### 投資報酬率(ROI)

* **說明**：依據行銷活動計算ROI的一種方式是分析透過行銷活動下的所有訂單。 不過，另一種方法是分析透過促銷活動取得的客戶期限值。 若要分析ROI，請務必確保您的支出資料和交易資料中的行銷活動名稱一致。 如果您建立下列報表，且行銷活動名稱不相符而導致ROI值不存在，您可能需要檢視 [UTM標籤](../../best-practices/utm-tagging-google.md) 您已實作。
* **報表範例**：各促銷活動的ROI
   * **[!UICONTROL Metric A]**: `New Customers`
   * **[!UICONTROL Filter A]**： `Customer's first order's source` 喜歡&#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**: `Average lifetime revenue`
   * **[!UICONTROL Filter A]**： `Customer's first order's source` 喜歡&#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric C]**: `Ad spend`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `(B-(C/A))/(C/A)`
   * 選取 `% `option
   * **[!UICONTROL Group By]**:
      * 針對量度 `A` 和 `B`，選取 `Customer's first order's campaign`
      * 針對量度 `C`，選取 `campaign`

>[!NOTE]
>
>您可以將公式命名為「ROI」，並隱藏所有量度。 此外，您可以調整量度中的篩選器，以分析替代來源和媒介。 另外，請出庫 [此主題](../analysis/roi-ad-camp.md) 以取得有關CAC、LTV和ROI的詳細資訊。

![ROI 1](../../assets/ROI_1.png)<!--{: width="929"}-->

![ROI 2](../../assets/ROI_2.png)<!--{: width="929"}-->
