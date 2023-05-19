---
title: customer_entity表格
description: 瞭解如何存取所有已註冊帳戶的記錄。
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# customer_entity表格

此 `customer_entity` 表格包含所有已註冊帳號的記錄。 無論客戶是否完成購買，只要客戶註冊帳戶，即視為已註冊。 每一列對應一個唯一的註冊帳戶，由帳戶的 `entity_id`.

此表格不包含透過訪客結帳發出訂單的客戶記錄。 如果您的商店接受訪客結帳，請參閱 [如何說明來賓訂單](../data-warehouse-mgr/guest-orders.md) 這些訂單的。

## 通用欄

| **欄名稱** | **說明** |
|---|---|
| `created_at` | 與帳戶註冊日期對應的時間戳記，以UTC在本機儲存。 視您在中的設定而定 [!DNL Commerce Intelligence]，此時間戳記可能會轉換為中的報表時區 [!DNL Commerce Intelligence] 與您的資料庫時區不同 |
| `email` | 與帳戶相關聯的電子郵件地址 |
| `entity_id` (PK) | 表格的唯一識別碼，通常用於聯結至 `customer_id` 在例項的其他表格中 |
| `group_id` | 與關聯的外來鍵 `customer_group` 表格。 加入 `customer_group.customer_group_id` 以判斷與註冊帳戶相關聯的客戶群組 |
| `store_id` | 與關聯的外來鍵 `store` 表格。 加入 `store`.`store_id` 若要判斷哪個Commerce商店檢視與已註冊的帳戶相關聯 |

{style="table-layout:auto"}

## 通用計算欄

| **欄名稱** | **說明** |
|---|---|
| `Customer's first 30 day revenue` | 此客戶在客戶第一個訂單日期起計30天內所下所有訂單的收入總和。 透過加入計算 `customer_entity.entity_id` 至 `sales_order.customer_id` 並加總 `base_grand_total` 所有訂單的欄位，其中 `sales_order.Seconds between customer's first order date and this order` ≤ 2592000，即30天內的秒數 |
| `Customer's first order date` | 此客戶下第一個訂單的時間戳記。 透過加入計算 `customer_entity.entity_id` 至 `sales_order.customer_id` 並傳回最小值 `sales_order`.`created_at` 值 |
| `Customer's first order's billing region` | 與客戶第一筆訂單相關聯的帳單區域。 透過加入計算 `customer_entity.entity_id` 至 `sales_order.customer_id` 並傳回 `Billing address region` 位置 `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | 與客戶第一筆訂單相關聯的優惠券代碼。 透過加入計算 `customer_entity.entity_id` 至 `sales_order.customer_id` 並傳回 `sales_order.coupon_code` 位置 `sales_order.Customer's order number` = 1 |
| `Customer's group code` | 註冊客戶的群組名稱。 透過加入計算 `customer_entity.group_id` 至 `customer_group`.`customer_group_id` 並傳回 `customer_group_code` 欄位 |
| `Customer's lifetime number of coupons` | 套用至此客戶所下所有訂單的抵用券總數。 透過加入計算 `customer_entity.entity_id` 至 `sales_order.customer_id` 並計算訂單數量，其中 `sales_order.coupon_code` 不是 `NULL` |
| `Customer's lifetime number of orders` | 此客戶下單的訂單總數。 透過加入計算 `customer_entity.entity_id` 至 `sales_order.customer_id` 並計算 `sales_order` 表格 |
| `Customer's lifetime revenue` | 此客戶下所有訂單的收入總和。 透過加入計算 `customer_entity.entity_id` 至 `sales_order.customer_id` 並加總 `base_grand_total` 此客戶下所有訂單的欄位 |
| `Seconds since customer's first order date` | 客戶首次訂購日期與現在之間經過的時間。 透過減法計算 `Customer's first order date` 從執行查詢時的伺服器時間戳記傳回，以整數秒數傳回 |
| `Store name` | 與此註冊帳戶關聯的Commerce商店名稱。 透過加入計算 `customer_entity.store_id` 至 `store.store_id` 並傳回 `name` 欄位 |

{style="table-layout:auto"}

## 通用量度

| **量度名稱** | **說明** | **建構** |
|---|---|---|
| `Avg first 30 day revenue` | 每位客戶在客戶首次訂購後30天內所下的訂單的平均收入 | 作業：平均<br/>運算元： `Customer's first 30 day revenue`<br/>時間戳記： `created_at`<br/>篩選器：<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000 （排除從首次訂購起未達到30天的客戶） |
| `Avg lifetime coupons` | 每位客戶在其期限內，套用至訂單的平均優惠券數量 | 作業：平均<br/>運算元： `Customer's lifetime number of coupons`<br/>時間戳記： `created_at` |
| `Avg lifetime orders` | 每位客戶在其期限內的平均訂購次數 | 作業：平均<br/>運算元： `Customer's lifetime number of orders`<br/>時間戳記： `created_at` |
| `Avg lifetime revenue` | 所有訂購期限內的每個客戶平均總收入 | 作業：平均<br/>運算元： `Customer's lifetime revenue`<br/>時間戳記： `created_at` |
| `New customers` | 至少有一筆訂單的客戶數，計算在其第一筆訂單的日期。 不包括註冊但從未下訂單的帳戶 | 作業：計數<br/>運算元： `entity_id`<br/>時間戳記： `Customer's first order date` |
| `Registered accounts` | 註冊的帳戶數目。 包含所有已註冊的帳戶，無論帳戶是否下過訂單 | 作業：計數<br/>運算元： `entity_id`<br/>時間戳記： `created_at` |

{style="table-layout:auto"}

## 外部索引鍵聯結路徑

`customer_group`

* 加入 `customer_group` 此表格可建立傳回已註冊帳戶之客戶群組名稱的欄。
   * 路徑： `customer_entity.group_id` （許多） => `customer_group.customer_group_id` （一）

`store`

* 加入 `store` 此表格可建立傳回與已註冊帳戶相關聯之存放區之詳細資料的資料欄。
   * 路徑： `customer_entity.store_id` （許多） => `store.store_id` （一）
