---
title: 現成可用的儀表板
description: 瞭解現成可用的儀表板，為您的企業提供深入分析。
exl-id: fe61c92e-de87-4317-96d7-01d2a9846bf9
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1932'
ht-degree: 0%

---

# 現成可用的儀表板

[!DNL Adobe Commerce Intelligence] 包含現成可用的儀表板，提供您對業務的深入分析。 透過控制面板，您可以檢查基本量度的健康狀況，例如使用者期限收入、重複購買次數、在指定時段內購買的熱門產品等。 建立這些預先設定的控制面板是為了協助您做出明智的業務決策。

>[!NOTE]
>
>這些儀表板的存取權取決於您的帳戶型別和存取層級。 如果您沒有看到這些儀表板，請聯絡 [支援](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## 報告可用性

對於 `Customers` 和 `Executive Summary` 儀表板，部分報表的可用性僅取決於您商店的結帳設定。 具體來說，如果您的商店允許訪客結帳或不允許訪客結帳。

## 客戶（允許訪客結帳）

「客戶」（允許訪客結帳）控制面板會提供有關客戶群的資訊，例如他們的購買行為。 此儀表板可協助您改善客戶保留率，以及判斷哪些客戶帶來最高收入。

### 報表

| 名稱 | 說明 |
|---|---|
| `Orders by New Customers (Past 30 Days)` | 過去30天內從未下過訂單的客戶所下的訂單。 |
| `Orders by Existing Customers (Past 30 Days)` | 過去30天內，來自先前已下過至少一個訂單的客戶的訂單。 |
| `Total Unique Customers (Past 30 Days)` | 過去30天內下訂單的不重複客戶數。 |
| `Orders by New vs Existing Customers` | 無先前訂單的客戶與至少有一筆先前訂單的客戶之訂單數。 |
| `Subsequent Order Probability (All Time)` | 已下訂單的客戶下另一個訂單的可能性。 |
| `% of Customers with Multiple Orders (All Time)` | 已下多筆訂單之所有客戶的百分比。 |
| `Median Time Between Orders (All Time)` | 每位客戶在下單與下單之間所花費的時間中位數。 |
| `Subsequent Order Probability` | 已下訂單的客戶下另一筆訂單的可能性，依訂單編號細分。 也就是說，同一份訂單下第二份的客戶百分比，以及第二份訂單下第三份的客戶百分比，依此類推。 |
| `Time Between Orders` | 客戶在訂單之間花費的平均和中位數，依訂單編號細分（即訂單一和二、二和三之間的時間，依此類推）。 |
| `Number of Customers - Lifetime Orders` | 對於客戶期限內的指定訂單數，已下該數量訂單的客戶人數以及該數字代表的整個客戶基礎的百分比。 |
| `One-Time Customers who Bought 3-6 Months Ago` | 首次購買且僅於三個月至六個月前購買的客戶。 |
| `Avg LTV by First Order` | 比較同類群組之間的累積平均客戶期限收入。 同類群組是根據客戶首次購買的月份來定義。 例如， `Jan 2020` 同類群組顯示首次購買於2020年1月之客戶的累積平均LTV。 |
| `Customer's First 30 Day vs Lifetime Revenue` | 比較客戶首次購買後30天內的平均收入與其整個期限內的收入。 每個泡泡圖都對應一個出貨地區，每個泡泡圖的大小代表從該地區取得的客戶數量。 |

## 客戶（不允許訪客結帳）

「客戶」（不允許訪客結帳）控制面板提供客戶群的相關資訊，例如他們的購買行為以及從帳戶註冊到訂單位置的轉換。 此儀表板可協助您改善客戶保留率，以及判斷哪些客戶帶來最高收入。

### 報表

| 名稱 | 說明 |
|---|---|
| `Account Registration (Past 30 Days)` | 過去30天內在您的商店註冊帳戶的人數。 |
| `Accounts Registered (Past 30 Days) with 1 or More Orders` | 過去30天內在您的商店註冊帳戶，且已下至少一次訂單的人數。 |
| `% Conversion from Registration to First Order (Past 30 Days)` | 在過去30天內註冊並已下訂單的帳戶百分比。 |
| `% Conversion from Registration to First Order` | 已註冊並已下訂單的帳戶百分比（按註冊月份）。 |
| `Orders by New vs Existing Customers` | 無先前訂單的客戶與至少有一筆先前訂單的客戶之訂單數。 |
| `Subsequent Order Probability (All Time)` | 已下訂單的客戶下另一個訂單的可能性。 |
| `% of Customers with Multiple Orders (All Time)` | 已下多筆訂單之所有客戶的百分比。 |
| `Median Time Between Orders (All Time)` | 每位客戶在下單與下單之間所花費的時間中位數。 |
| `Subsequent Order Probability` | 已下訂單的客戶下另一個訂單的可能性（依訂單編號劃分）。 也就是說，同一份訂單的客戶中，有第二份訂單的百分比，有第二份訂單的客戶中，有第三份訂單的百分比，依此類推。 |
| `Time Between Orders` | 客戶在訂單之間花費的平均和中位數，依訂單編號細分（即訂單一和二、二和三之間的時間，依此類推）。 |
| `Number of Customers - Lifetime Orders` | 對於客戶期限內的指定訂單數，已下該數量訂單的客戶人數以及該數字代表的整個客戶基礎的百分比。 |
| `One-Time Customers who Bought 3-6 Months Ago` | 首次購買且僅於三個月至六個月前購買的客戶。 |
| `Avg LTV by First Order` | 比較同類群組之間的累積平均客戶期限收入。 同類群組是根據客戶首次購買的月份來定義。 例如，2020年1月同類群組會顯示首次購買於2020年1月的客戶的累積平均LTV。 |
| `Customer's First 30 Day vs Lifetime Revenue` | 比較客戶首次購買後30天內的平均收入與其整個期限內的收入。 每個泡泡圖都對應一個出貨地區，每個泡泡圖的大小代表從該地區取得的客戶數量。 |

## 執行摘要（允許訪客結帳）

「執行摘要」（允許來賓結帳）控制面板可讓您清楚瞭解訂單和收入方面的業務狀況。 此儀表板是專為高階主管所設計，以便全面瞭解業務績效，但也可供其他人深入瞭解。

### 報表

| 名稱 | 說明 |
|---|---|
| `Revenue (Current Month)` | 您的商店本月產生的收入。 在此案例中，收入定義為客戶在訂單上支付的最終價格。 |
| `Revenue (Past 6 Months by Day)` | 每日收入總計，加上前七天的平均每日收入。 在此案例中，收入定義為客戶在訂單上支付的最終價格。 |
| `% Change in Revenue (MoM MTD)` | 本月（迄今）與上個月同一部分的收入比較。 |
| `Revenue from New vs Existing Customers (Current Month)` | 目前歸屬於新（首次）客戶的當月收入與現有客戶（下第二筆或以上訂單）的收入。 |
| `Average Order Value (Current Month)` | 當月（到目前為止）所下訂單的每日平均值。 訂單值定義為客戶在訂單上支付的最終價格。 |
| `Orders (Current Month)` | 目前月份（到目前為止）在商店中下單的訂單數。 |
| `% Change in Orders (MoM MTD)` | 本月份訂單數（截至目前）與上個月同一部分的比較。 |
| `Orders by New Customers (Current Month)` | 從未下過訂單之客戶的當月訂單。 |
| `Orders by Existing Customers (Current Month)` | 先前下過至少一個訂單的客戶當月訂單。 |
| `Orders by New vs Existing Customers (Current Year by Week)` | 當年（到目前為止）每週沒有先前訂單的客戶與至少有一個先前訂單的客戶訂單數。 |

## 執行摘要（不允許訪客結帳）

「執行摘要」（不允許訪客結帳）控制面板可讓您清楚瞭解訂單、收入和帳戶註冊方面的業務狀況。 此儀表板是專為高階主管所設計，以便全面瞭解業務績效，但也可供其他人深入瞭解。

### 報表

| 名稱 | 說明 |
|---|---|
| `Revenue (Current Month)` | 您的商店本月產生的收入。 在此案例中，收入定義為客戶在訂單上支付的最終價格。 |
| `Revenue (Past 6 Months by Day)` | 每日收入總計，加上前七天的平均每日收入。 在此案例中，收入定義為客戶在訂單上支付的最終價格。 |
| `% Change in Revenue (MoM MTD)` | 本月到目前為止與上個月同一部分的收入比較。 |
| `Revenue from New vs Existing Customers (Current Month)` | 目前歸屬於新（首次）客戶的當月收入與現有客戶（下第二筆或以上訂單）的收入。 |
| `Average Order Value (Current Month)` | 當月（到目前為止）所下訂單的每日平均值。 訂單值定義為客戶在訂單上支付的最終價格。 |
| `Orders (Current Month)` | 目前月份（到目前為止）在商店中下單的訂單數。 |
| `% Change in Orders (MoM MTD)` | 本月份訂單數（截至目前）與上個月同一部分的比較。 |
| `Account Registrations (Current Month)` | 本月到目前為止新註冊的帳戶數目。 |
| `% Conversion from Registration to First Order (Current Month)` | 本月到目前為止已註冊並已下訂單的帳戶百分比。 |
| `% Conversion from Registration to First Order (Current Year by Week)` | 今年截至目前每週已註冊並已下訂單的帳戶百分比。 |

## 訂購

「訂單」儀表板提供交易訂單量、訂單狀態、使用的優惠券代碼、產生的收入，以及使用的付款方式的深入分析。 例如，您可以追蹤履行處理，並確保沒有問題或瓶頸發生。

>[!NOTE]
>
>此儀表板上的報告適用於連線到具有任一設定型別（訪客結帳，無訪客結帳）之商店的帳戶。

### 報表

| 名稱 | 說明 |
|---|---|
| `Orders (Past 30 Days)` | 過去30天內在商店下單的訂單數。 |
| `Revenue (Past 30 Days)` | 您的商店在過去30天內產生的收入。 收入定義為客戶在訂單上支付的最終價格。 |
| `Average Order Value (Past 30 Days)` | 過去30天內訂單的平均值。 訂單值定義為客戶在訂單上支付的最終價格。 |
| `Orders` | 每個月在您的商店中下單的訂單數。 |
| `Revenue by Payment Method` | 依付款方式分割的商店所產生的收入。 收入定義為客戶在訂單上支付的最終價格。 |
| `AOV by New vs Existing Customers` | 商店中訂單的每月平均值，依沒有先前訂單的客戶與至少有一個先前訂單的客戶所下的訂單進行分割。 訂單值定義為客戶在訂單上支付的最終價格。 |
| `% Orders by Status (Past 30 Days)` | 過去30天內每天處於各訂單狀態的訂單百分比。 |
| `Incomplete Orders (Created more than 1 Day Ago)` | 超過1天前所下的所有訂單清單，這些訂單仍然處於未完成狀態（未取消或完成）。 |
| `Orders Per Hour (Past 7 Days)` | 按日按小時訂購數量。 |
| `Revenue Details (Past 30 Days)` | 將過去30天的每日收入劃分至總收入值的所有元件。 |
| `Order Details by Coupon Code (Past 30 Days)` | 對於商店提供的每個優惠券代碼，詳細說明該優惠券代碼的使用方式以及過去30天內該代碼帶來的回報。 |
| `% Orders with Coupon (Past 30 Days)` | 過去30天內使用抵用券的訂單與未使用抵用券的訂單的百分比。 |

## 產品

「產品」儀表板顯示一般產品績效，包括訂購的產品、其商品總值(GMV)以及購買和退款的頂級產品。 這可協助您平衡購買與回報，並判斷產品成功與受歡迎程度。 您的存放區必須 [設定為追蹤退款](https://experienceleague.adobe.com/docs/commerce-admin/customers/customer-accounts/store-credit/credit-configure.html) 用於要填入的圖表。

>[!NOTE]
>
>此儀表板上的報告適用於連線到具有任一設定型別（訪客結帳，無訪客結帳）之商店的帳戶。

### 報表

| 名稱 | 說明 |
|---|---|
| `GMV (Past 30 Days)` | 過去30天內銷售之所有產品的商品總值。 GMV定義為訂購數量乘以各產品的基準價格。 |
| `% GMV (Past 30 Days) Refunded` | 過去30天內購買導致退款之產品的GMV百分比。 |
| `Product Quantity Ordered (Past 30 Days)` | 過去30天內訂購的料號總數量。 |
| `% Purchased Products (Past 30 Days) Refunded` | 過去30天內購買並導致退款的專案百分比。 |
| `Gross Merchandise Value` | 所有已售出產品的商品總值（按月份）。 GMV定義為訂購數量乘以各產品的基準價格。 |
| `Purchases vs Refund Rate per Product (Past 30 Days)` | 針對每項產品，比較過去30天內訂購的總數與產品退款率。 每個泡泡的大小代表退款率。 |
| `Product Performance Details (Past 30 Days)` | 依產品SKU和產品名稱，列出過去30天內的銷售與後續退款的詳細資訊。 |
| `Top Purchased Products by GMV (Past 30 Days)` | 過去30天內銷售的產品帶來最多收入（前10項）。 |
| `Top Refunded Products by GMV (Past 30 Days)` | 在過去30天內購買的產品因退款而損失的GMV最高（前10項）。 |
| `Top Purchased Products by Quantity (Past 30 Days)` | 過去30天內銷售的產品數量最多（前10名）。 |
| `Top Refunded Products by Quantity (Past 30 Days)` | 在過去30天內購買導致最多退款（前10項）的產品。 |
