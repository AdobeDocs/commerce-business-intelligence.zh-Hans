---
title: 格式化及匯入電子商務資料
description: 瞭解用於上傳電子商務資料的理想資料格式。
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# 格式化及匯入資料

如果您使用目前不支援的整合 [!DNL Adobe Commerce Intelligence]，您仍可使用 [檔案上傳功能](using-file-uploader.md) 將您的資料匯入Data Warehouse。 本主題說明用於上傳電子商務資料的理想資料格式。

## `Orders` 表格

此 `orders` 表格中應包含企業已進行之每項交易的一列。 可能的欄包括：

| 欄名稱 | 說明 |
|----|----|
| `Order ID` | 表格中每一列的訂單ID應該是唯一的。 此外，這通常是表格的主索引鍵。 |
| `Customer` | 下訂單的客戶。 |
| `Order total` | 訂單總計。 這可能是以計算為基礎的欄，其他欄中的值（例如小計和運送）構成此欄的總計。 |
| `Currency` | 支付訂單所用的貨幣。 包含相關專案。 |
| ` Order status` | 訂單的狀態，例如 `In Progress`， `Refunded`，或 `Complete`. 此欄的值會變更（如果未完成）。 新的和更新的資料可以使用匯入 [附加資料功能](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) 於 `File Uploads` 頁面。 |
| `Acquisition/marketing channel` | 下訂單的客戶反向連結的贏取或行銷管道。 |
| `Order datetime` | 建立訂單的日期和時間。 |
| `Order updated at` | 上次修改訂單記錄的日期與時間。 |

{style="table-layout:auto"}

## `Order detail/items` 表格 {#itemstable}

此 `order_detail / items` 表格應包含每個順序中每個不同專案的一列。 可能的欄包括：

| 欄名稱 | 說明 |
|----|----|
| `Order item ID` | 表格中每一列的訂單專案ID應該是唯一的。 此外，這通常是 `primary key` 以取得表格。 |
| `Order ID` | 訂單的ID。 |
| `Product ID` | 產品的ID。 |
| `Product name` | 產品的名稱。 |
| `Product's unit price` | 單一產品單位的價格。 |
| `Quantity` | 訂單中的產品數量。 |

## `Customers` 表格 {#customerstable}

此 `customers` 表格應包含每個客戶帳戶的一列。 可能的欄包括：

| 欄名稱 | 說明 |
|----|----|
| `Customer ID` | 表格中每一列的客戶ID都應是唯一的。 此外，這通常是表格的主索引鍵。 |
| `Customer created at` | 建立客戶帳戶的日期和時間。 |
| `Customer modified at` | 上次修改客戶帳戶的日期和時間。 |
| `Acquisition/marketing channel source` | 反向連結客戶的贏取或行銷管道。 |
| `Demographic info` | 年齡範圍和性別等人口統計資訊可用於細分您的報表。 |
| `Acquisition/marketing channel` | 下訂單的客戶反向連結的贏取或行銷管道。 |

## `Subscription payments` 表格

此 `subscriptions` 表格應包含每個訂閱付款的一列。 可能的欄包括：

| 欄名稱 | 說明 |
|----|----|
| `Subscription ID` | 表格中每一列的訂閱ID都應是唯一的。 此外，這通常是表格的主索引鍵。 |
| `Customer ID` | 付款客戶的識別碼。 |
| `Payment amount` | 訂閱付款的金額。 |
| `Start date` | 付款涵蓋期間的開始日期時間。 |
| `End date` | 付款涵蓋期間的結束日期時間。 |
