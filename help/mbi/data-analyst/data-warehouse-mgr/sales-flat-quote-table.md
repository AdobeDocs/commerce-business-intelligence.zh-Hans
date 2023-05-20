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

此 `quote` 表格(`sales_flat_quote` （在M1上）包含您商店中建立的每個購物車的記錄，無論這些記錄是被捨棄或是轉換為購買。 每一列代表一個購物車。 由于此表的可能大小，Adobe Systems 建议您在满足特定条件时定期删除记录，例如，如果有任何超过60天的未转换购物车。

>[!NOTE]
>
>只有在您未刪除記錄的情況下，才可能分析歷史放棄的購物車。 `quote` 表格。 如果您確實刪除記錄，則只能看到尚未從資料庫移除的購物車。

## 通用原生欄

| **欄名稱** | **說明** |
|---|---|
| `base_currency_code` | 擷取的所有值的貨幣 `base_*` 欄位(即 `base_grand_total`， `base_subtotal`、等等)。 这通常反映商务商店的默认货币 |
| `base_grand_total` | 在应用了所有税收、运费和折扣后，最终的客户报价购物车。 虽然精确计算是可自定义的，但一般 `base_grand_total` 情况下计算方式 `base_subtotal` 为 + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | 購物車中包含之所有商品的總商品價值。 不包含稅金、運費、折扣等 |
| `created_at` | 購物車的建立時間戳記，儲存在UTC的本機。 視您在中的設定而定 [!DNL Commerce Intelligence]，此時間戳記可能會轉換為中的報表時區 [!DNL Commerce Intelligence] 與您的資料庫時區不同 |
| `customer_email` | 创建购物车的客户的电子邮件地址 |
| `customer_id` | `Foreign key` 如果客户已注册，则与 `customer_entity` 表关联。 `customer_entity.entity_id`加入确定与创建购物车的用户相关联的客户属性。如果购物车是通过来宾结帐创建的，则此字段为 `NULL` |
| `entity_id` 主键 | 表的唯一标识符，通常用于商务中其他表的联接实例 |
| `is_active` | 布尔字段，如果购物车是由客户创建且尚未转换为订单，则返回 &quot;1&quot;。 針對已轉換的購物車或透過管理員建立的購物車，傳回「0」 |
| `items_qty` | 購物車中包含之所有專案的總數量 |
| `reserved_order_id` | `Foreign key` 與 `sales_order` 表格。 加入 `sales_order.increment_id` 以判斷與已轉換購物車相關聯的訂單詳細資料。 對於未與已轉換訂單相關聯的購物車，請 `reserved_order_id` 剩餘 `NULL` |
| `store_id` | `Foreign key` 与 `store` 表关联。 `store`加入。`store_id` 确定哪些商务商店视图与购物车相关联 |

{style="table-layout:auto"}

## 通用計算欄

| **欄名稱** | **說明** |
|---|---|
| `Order date` | 反映已轉換購物車訂單建立日期的時間戳記。 透過加入計算 `quote.reserved_order_id` 至 `sales_order.increment_id` 並傳回 `sales_order.created_at` 欄位 |
| `Seconds between cart creation and order` | 從購物車建立到訂單建立之間的經過時間。 通过减去 `created_at` `Order date` （以整数秒数表示）返回的计算 |
| `Seconds since cart creation` | 從購物車建立日期到現在之間經過的時間。 计算方法是在执行查询时减去 `created_at` 服务器时间戳，以整数秒数的形式返回。 最常用於識別購物車的年齡 |
| `Store name` | 與此訂單關聯的Commerce商店名稱。 透過加入計算 `quote.store_id` 至 `store.store_id` 並傳回 `name` 欄位 |

{style="table-layout:auto"}

## 通用量度

| **量度名称** | **描述** | **建设** |
|---|---|---|
| `Number of abandoned carts` | 符合特定 &quot;放弃&quot; 条件的购物车计数 | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:``created_at`<br/>过滤器： <br><br> -\ [ `A` \] `is_active` = 1 <br> -\ [ `B` \] `items_count` > 0 <br> -\ [ `C` \ `Seconds since cart creation` ] > x，其中 &quot;x&quot; 对应于购物车创建，超过此时间后，购物车被视为放弃 |
| `Avg time to cart conversion` | 转换后的购物车购物车创建和订单创建之间的平均时间 | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | 捨棄的購物車潛在收入總和，其中收入定義為 `base_grand_total` 欄位 | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>篩選器：<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x，其中「x」對應於自建立購物車後經過的時間（以秒為單位），超過該時間，購物車會被視為放棄 |

{style="table-layout:auto"}

## 外键联接路径

`customer_entity`

* 加入到 `customer_entity` 表格，以创建与创建购物车的客户关联的新客户级列。
   * 路径： `quote.customer_id` （多） = > `customer_entity.entity_id` （一）

`sales_order`

* 加入 `sales_order` 此表格可建立傳回與已轉換購物車相關之訂單詳細資料的欄。
   * 路徑：`quote.reserved_order_id` （許多） => `sales_order.increment_id` （一）

`store`

* 加入 `store` 此表格可建立欄，傳回與購物車相關聯之Commerce商店的相關詳細資訊。
   * 路徑： `quote.store_id` （許多） => `store.store_id` （一）
