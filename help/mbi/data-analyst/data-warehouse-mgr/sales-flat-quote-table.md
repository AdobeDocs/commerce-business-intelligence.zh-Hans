---
title: 報價表
description: 瞭解如何使用報價表。
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# 報價表

此 `quote` 表格(`sales_flat_quote` （在M1上）包含您商店中建立的每個購物車的記錄，無論這些記錄是被捨棄或是轉換為購買。 每一列代表一個購物車。 由於此表格可能會很大，Adobe建議您在符合某些條件時（例如有任何未轉換的購物車超過60天）定期刪除記錄。

>[!NOTE]
>
>只有在您未刪除記錄的情況下，才可能分析歷史放棄的購物車。 `quote` 表格。 如果您確實刪除記錄，則只能看到尚未從資料庫移除的購物車。

## 通用原生欄

| **欄名稱** | **說明** |
|---|---|
| `base_currency_code` | 擷取的所有值的貨幣 `base_*` 欄位(即 `base_grand_total`， `base_subtotal`、等等)。 這通常會反映Commerce商店的預設貨幣 |
| `base_grand_total` | 套用所有稅捐、運費和折扣後，對購物車的客戶報價的最終價格。 雖然精確計算是可自訂的，但一般而言 `base_grand_total` 計算方式為 `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | 購物車中包含之所有商品的總商品價值。 不包含稅金、運費、折扣等 |
| `created_at` | 購物車的建立時間戳記，儲存在UTC的本機。 視您在中的設定而定 [!DNL Commerce Intelligence]，此時間戳記可能會轉換為中的報表時區 [!DNL Commerce Intelligence] 與您的資料庫時區不同 |
| `customer_email` | 建立購物車的客戶的電子郵件地址 |
| `customer_id` | `Foreign key` 與 `customer_entity` 表格（若客戶已註冊）。 加入 `customer_entity.entity_id` 以判斷與建立購物車之使用者相關聯的客戶屬性。 如果購物車是透過訪客結帳建立的，則此欄位為 `NULL` |
| `entity_id` (PK) | 表格的唯一識別碼，通常用於聯結至Commerce執行個體內的其他表格 |
| `is_active` | 如果購物車是由客戶建立且尚未轉換為訂單，則傳回「1」的布林欄位。 針對已轉換的購物車或透過管理員建立的購物車，傳回「0」 |
| `items_qty` | 購物車中包含之所有專案的總數量 |
| `reserved_order_id` | `Foreign key` 與 `sales_order` 表格。 加入 `sales_order.increment_id` 以判斷與已轉換購物車相關聯的訂單詳細資料。 對於未與已轉換訂單相關聯的購物車，請 `reserved_order_id` 剩餘 `NULL` |
| `store_id` | `Foreign key` 與 `store` 表格。 加入 `store`.`store_id` 以判斷與購物車相關聯的Commerce商店檢視 |

{style="table-layout:auto"}

## 通用計算欄

| **欄名稱** | **說明** |
|---|---|
| `Order date` | 反映已轉換購物車訂單建立日期的時間戳記。 透過加入計算 `quote.reserved_order_id` 至 `sales_order.increment_id` 並傳回 `sales_order.created_at` 欄位 |
| `Seconds between cart creation and order` | 從購物車建立到訂單建立之間的經過時間。 透過減法計算 `created_at` 從 `Order date`，以整數秒數傳回 |
| `Seconds since cart creation` | 從購物車建立日期到現在之間經過的時間。 透過減法計算 `created_at` 從執行查詢時的伺服器時間戳記傳回，以整數秒數傳回。 最常用於識別購物車的年齡 |
| `Store name` | 與此訂單關聯的Commerce商店名稱。 透過加入計算 `quote.store_id` 至 `store.store_id` 並傳回 `name` 欄位 |

{style="table-layout:auto"}

## 通用量度

| **量度名稱** | **說明** | **建構** |
|---|---|---|
| `Number of abandoned carts` | 符合特定「放棄」條件的購物車計數 | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>篩選器：<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x，其中「x」對應於自建立購物車後經過的時間（以秒為單位），超過該時間，購物車會被視為放棄 |
| `Avg time to cart conversion` | 從購物車建立到轉換購物車的訂單建立之間的平均時間 | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | 捨棄的購物車潛在收入總和，其中收入定義為 `base_grand_total` 欄位 | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>篩選器：<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x，其中「x」對應於自建立購物車後經過的時間（以秒為單位），超過該時間，購物車會被視為放棄 |

{style="table-layout:auto"}

## 外部索引鍵聯結路徑

`customer_entity`

* 加入 `customer_entity` 此表格可建立與建立購物車的客戶相關聯的新客戶層級欄。
   * 路徑： `quote.customer_id` （許多） => `customer_entity.entity_id` （一）

`sales_order`

* 加入 `sales_order` 此表格可建立傳回與已轉換購物車相關之訂單詳細資料的欄。
   * 路徑：`quote.reserved_order_id` （許多） => `sales_order.increment_id` （一）

`store`

* 加入 `store` 此表格可建立欄，傳回與購物車相關聯之Commerce商店的相關詳細資訊。
   * 路徑： `quote.store_id` （許多） => `store.store_id` （一）
