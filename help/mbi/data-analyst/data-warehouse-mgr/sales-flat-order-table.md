---
title: sales_order表格
description: 瞭解如何使用sales_order表格。
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 0%

---

# `sales_order` 表格

此 `sales_order` 表格(`sales_flat_order` （位於M1）是擷取每個訂單的位置。 雖然Commerce有一些自訂實作，會導致將訂單分割為個別的列，但通常每列都代表一個不重複的訂單。

此表格包含所有客戶訂單，無論該訂單是否透過訪客結帳處理。 如果您的商店接受訪客結帳，您可以找到更多相關資訊 [使用案例](../data-warehouse-mgr/guest-orders.md).

## 通用欄

| **欄名稱** | **說明** |
|---|---|
| `base_currency_code` | 擷取的所有值的貨幣 `base_*` 欄位(即 `base_grand_total`， `base_subtotal`、等等)。 這通常會反映Commerce商店的預設貨幣 |
| `base_discount_amount` | 套用至訂單的折扣值 |
| `base_grand_total` | 套用所有稅捐、運費和折扣後，客戶在訂單上支付的最終價格。 雖然精確計算是可自訂的，但一般而言 `base_grand_total` 計算方式為 `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | 訂單中包含之所有專案的商品總值。 不包含稅金、運費、折扣等 |
| `base_shipping_amount` | 套用至訂單的送貨值 |
| `base_tax_amount` | 套用至訂單的稅捐值 |
| `billing_address_id` | `Foreign key` 與 `sales_order_address` 表格。 加入 `sales_order_address.entity_id` 以決定與訂單相關聯的帳單地址明細 |
| `coupon_code` | 適用於訂單的優惠券。 若未套用任何抵用券，則此欄位為 `NULL` |
| `created_at` | 訂單的建立時間戳記，以UTC在本機儲存。 視您在中的設定而定 [!DNL Commerce Intelligence]，此時間戳記可能會轉換為中的報表時區 [!DNL Commerce Intelligence] 與您的資料庫時區不同 |
| `customer_email` | 下訂單客戶的電子郵件地址。 所有情況下都會填入此值，包括透過訪客結帳處理的訂單 |
| `customer_group_id` | 與關聯的外來鍵 `customer_group` 表格。 加入 `customer_group.customer_group_id` 以決定與訂單相關聯的客戶群組 |
| `customer_id` | `Foreign key` 與 `customer_entity` 表格（若客戶已註冊）。 加入 `customer_entity.entity_id` 以判斷與訂單相關聯的客戶屬性。 如果訂單是透過訪客結帳方式下達，則此欄位為 `NULL` |
| `entity_id` (PK) | 表格的唯一識別碼，通常用於聯結至Commerce執行個體內的其他表格 |
| `increment_id` | 訂單的唯一識別碼，通常稱為 `order_id` 在Adobe Commerce中。 此 `increment_id` 最常用於聯結至外部來源，例如 [!DNL Google Ecommerce] |
| `shipping_address_id` | 與關聯的外來鍵 `sales_order_address` 表格。 加入 `sales_order_address.entity_id` 以決定與訂單相關聯的送貨地址明細 |
| `status` | 訂單的狀態。 可傳回「complete」、「processing」、「cancelled」、「refolled」等值，以及Commerce執行個體上實作的任何自訂狀態。 訂單處理時可能會有所變更 |
| `store_id` | `Foreign key` 與 `store` 表格。 加入 `store`.`store_id` 以判斷與訂單相關聯的Commerce商店檢視 |

{style="table-layout:auto"}

## 通用計算欄

| **欄名稱** | **說明** |
|---|---|
| `Billing address city` | 訂單的帳單城市。 透過加入計算 `sales_order`.`billing_address_id` 至 `sales_order_address`.`entity_id` 並傳回 `city` 欄位 |
| `Billing address country` | 訂單的帳單國家/地區代碼。 透過加入計算 `sales_order`.`billing_address_id` 至 `sales_order_address`.`entity_id` 並傳回 `country_id` |
| `Billing address region` | 訂單的帳單區域（通常為州或省）。 透過加入計算 `sales_order`.`billing_address_id` 至 `sales_order_address`.`entity_id` 並傳回 `region` 欄位 |
| `Customer's first order date` | 此客戶下第一個訂單的時間戳記。 通常被認為是客戶的「贏取日期」。 透過傳回最小值來計算 `sales_order`.`created_at` 每個獨特客戶的值 |
| `Customer's first order's billing region` | 下訂單之客戶的贏取帳單區域。 計算方式為傳回 `Billing address region` 與客戶第一筆訂單相關聯 |
| `Customer's first order's coupon_code` | 下此訂單的客戶的贏取優惠券代碼。 計算方式為傳回 `coupon_code` 與客戶第一筆訂單相關聯 |
| `Customer's group code` | 下此訂單的客戶的群組名稱。 透過加入計算 `sales_order`.`customer_group_id` 至 `customer_group`.`customer_group_id` 並傳回 `customer_group_code` 欄位 |
| `Customer's lifetime number of coupons` | 套用至此客戶所下所有訂單的抵用券總數。 計算訂單數，其中 `coupon_code` 不是 `NULL` 每個獨特客戶 |
| `Customer's lifetime number of orders` | 此客戶下單的訂單總數。 計算方式為計算 `sales_order` 每個獨特客戶的表格 |
| `Customer's lifetime revenue` | 此客戶下所有訂單的收入總和。 計算方式為加總 `base_grand_total` 每個獨特客戶之所有訂單的欄位 |
| `Customer's order number` | 此客戶訂單的循序訂單排名。 透過識別客戶下的所有訂單，並依 `created_at` 時間戳記，並為每個訂單指派遞增的整數值。 例如，客戶的第一筆訂單會傳回 `Customer's order number` / 1，客戶的第二筆訂單會傳回 `Customer's order number` /2，依此類推。 |
| `Customer's order number (previous-current)` | 與此訂單排名連結的客戶先前訂單排名，以 `-` 字元。 計算方式為串連(&quot;`Customer's order number` - 1&quot;)搭配&quot;`-`&quot;後跟&quot;`Customer's order number`「。 例如，對於與客戶第二次購買相關聯的訂單，此欄會傳回值 `1-2`. 最常用於表示兩個訂單事件之間的時間（亦即「訂單之間的時間」圖表中） |
| `Is customer's last order?` | 決定訂單是否對應至客戶的上次或最近訂單。 計算方式為比較 `Customer's order number` 值 `Customer's lifetime number of orders`. 當這兩個欄位在給定順序中相等時，此欄會傳回 `Yes`；否則會傳回 `No` |
| `Number of items in order` | 訂單中包含的料號總數量。 透過加入計算 `sales_order`.`entity_id` 至 `sales_order_item`.`order_id` 並加總 `sales_order_item`.`qty_ordered` 欄位 |
| `Seconds between customer's first order date and this order` | 此訂單與客戶第一筆訂單之間的經過時間。 透過減法計算 `Customer's first order date` 從 `created_at` 會以整數秒數傳回 |
| `Seconds since previous order` | 此訂單與客戶之前訂單之間經過的時間。 計算方式為減去 `created_at` 先前訂單來自 `created_at` ，以整數秒數傳回。 例如，對於與客戶第三筆訂單對應的訂單記錄，此欄會傳回客戶第二筆訂單與第三筆訂單之間的秒數。 若為客戶的第一筆訂單，此欄位會傳回 `NULL` |
| `Shipping address city` | 訂單的送貨城市。 透過加入計算 `sales_order`.`shipping_address_id` 至 `sales_order_address`.`entity_id` 並傳回 `city` 欄位 |
| `Shipping address country` | 訂單的出貨國家/地區代碼。 透過加入計算 `sales_order`.`Shipping_address_id` 至 `sales_order_address`.`entity_id` 並傳回 `country_id` |
| `Shipping address region` | 訂單的送貨地區（通常為州或省）。 透過加入計算 `sales_order`.`shipping_address_id` 至 `sales_order_address`.`entity_id` 並傳回 `region` 欄位 |
| `Store name` | 與此訂單關聯的Commerce商店名稱。 透過加入計算 `sales_order`.`store_id` 至 `store`.`store_id` 並傳回 `name` 欄位 |

## 通用量度

| **量度名稱** | **說明** | **建構** |
|---|---|---|
| `Avg order value` | 每筆訂單的平均收入，其中收入定義為 `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | 客戶(n-1)訂單與第n筆訂單之間的平均時間（針對所有客戶和訂單） | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | 在套用所有稅金和折扣之前，所有訂單的商品總值總和（其中GMV定義為小計） | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | 客戶(n-1)訂單與第n筆訂單之間的中位時間（針對所有客戶和訂單） | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | 訂購總數 | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | 所有訂單的收入總和，其中收入定義為客戶支付的最終價格，扣除所有稅捐、折扣、出貨等之後套用 | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | 所有訂單的出貨金額總和 | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | 套用至所有訂單的稅額總和 | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | 在指定報告時間間隔內下訂單的不重複客戶數。 例如，如果報表的間隔為每週，則在指定周內下至少一筆訂單的每位客戶，無論在該周下了多少訂單，都會被計算一次 | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` 聯結路徑

`customer_entity`

* 加入 `customer_entity` 此表格可建立與下訂單的客戶相關聯的新客戶層級欄位。
   * 路徑： `sales_order.customer_id` （許多） => `customer_entity.entity_id` （一）

`customer_group`

* 加入 `customer_group` 此表格可建立傳回下訂單之客戶之客戶群組名稱的欄位。
   * 路徑： `sales_order.customer_group_id` （許多） => `customer_group.customer_group_id` （一）

`sales_order_address`

* 加入 `sales_order_address` 此表格可建立與訂單相關之退貨帳單與出貨地點的欄位。 視需要帳單或送貨詳細資料而定，可能會有兩個聯結路徑。
   * 路徑：
      * 送貨： `sales_order.shipping_address_id`（許多） => `sales_order_address.entity_id` （一）
      * 帳單： `sales_order.billing_address_id`（許多） => `sales_order_address.entity_id` （一）

`store`

* 加入 `store` 此表格可建立傳回與訂單相關聯之Commerce商店相關詳細資料的欄。
   * 路徑： `sales_order.store_id` （許多） => `store.store_id` （一）
