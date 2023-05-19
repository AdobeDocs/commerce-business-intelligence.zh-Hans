---
title: sales_order_item表格
description: 瞭解如何使用sales_order_item表格。
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---

# `sales_order_item` 表格

此 `sales_order_item` 表格(`sales_flat_order_item` （在M1上）包含訂單中所購買所有產品的記錄。 每一列代表一個唯一 `sku` 包含在訂單中。 為特定採購的單位數量 `sku` 最常由 `qty_ordered` 欄位。

## 產品型別

此 `sales_order_item` 擷取所有專案的詳細資料 [產品型別](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 已購買的專案。 中的常見做法 [!DNL Adobe Commerce] 是提供可設定的產品，換句話說，就是可根據尺寸、顏色和其他產品屬性自訂的產品。 雖然可設定的產品有其專屬的 `sku`，這可能與多個簡單產品有關，其中每個簡單產品代表一個獨特的產品設定。 請參閱 [設定產品](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) 以取得詳細資訊。

例如，假設是可設定的產品，例如T恤。 客戶出庫時，會選取選項以變更顏色和大小。 如果客戶選取 `blue`，大小為 `small`，最後他們購買簡單產品，例如 `t-shirt-blue-small` 與的父產品相關 `t-shirt`.

當可設定的產品包含在訂單中時，會在以下兩列產生： `sales_order_item` 表格：一個用於 [簡單](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku` 一個用於 [可設定](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) 父系。 這兩個記錄位於 `sales_order_item` 表格可透過下列連線彼此關聯：

* （簡單） `sales_order_item.parent_item_id` => （可設定） `sales_order_item.item_id`

因此，您可以在簡單層次或可設定層次報告產品的銷售情況。 依預設，所有標準 `order-item-level` 中的量度 [!DNL Commerce Intelligence] 設定為排除簡單產品，以及 *僅限* 報告可設定的版本。 這是透過以下方式完成的： `Ordered products we count` 篩選器集，根據條件 `parent_item_id` 是 `NULL`.

## 通用欄

| **欄名稱** | **說明** |
|----|----|
| `base_price` | 售出後產品在銷售時的個別單位價格 [目錄價格規則、分級折扣和特殊定價](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 在套用任何稅捐、運費或購物車折扣之前使用。 以商店的基本貨幣表示。 |
| `created_at` | 訂單專案的建立時間戳記，以UTC在本機儲存。 視您在中的設定而定 [!DNL Commerce Intelligence]，此時間戳記可能會轉換為中的報表時區 [!DNL Commerce Intelligence] 與您的資料庫時區不同。 |
| `item_id` (PK) | 資料表的唯一識別碼。 |
| `name` | 訂單專案的文字名稱。 |
| `order_id` | `Foreign key` 與 `sales_order` 表格。 加入 `sales_order.entity_id` 以決定與訂單料號相關聯的訂單屬性。 |
| `parent_item_id` | `Foreign key` 將簡單產品與其父套裝或可設定產品相關聯。 加入 `sales_order_item.item_id` 以判斷與簡單產品相關聯的父產品屬性。 對於父級訂單專案（亦即套件或可配置產品型別），請 `parent_item_id` 是 `NULL`. |
| `product_id` | `Foreign key` 與 `catalog_product_entity` 表格。 加入 `catalog_product_entity.entity_id` 以決定與訂單料號相關聯的產品屬性。 |
| `product_type` | 已售出的產品型別。 潛在 [產品型別](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 包括：簡單、可設定、分組、虛擬、套件組合和可下載。 |
| `qty_ordered` | 銷售時包含在購物車中特定訂單專案的單位數量。 |
| `sku` | 所購買訂單專案的唯一識別碼。 |
| `store_id` | `Foreign key` 與 `store` 表格。 加入 `store.store_id` 以判斷與訂單專案相關聯的Commerce商店檢視。 |

{style="table-layout:auto"}

## 通用計算欄

| **欄名稱** | **說明** |
|---|---|
| `Customer's email` | 下訂單客戶的電子郵件地址。 透過加入計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 並傳回 `customer_email` 欄位。 |
| `Customer's lifetime number of orders` | 此客戶下單的訂單總數。 透過加入計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 並傳回 `Customer's lifetime number of orders` 欄位。 |
| `Customer's lifetime revenue` | 此客戶下所有訂單的收入總和。 透過加入計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 並傳回 `Customer's lifetime revenue` 欄位。 |
| `Customer's order number` | 此客戶訂單的循序訂單排名。 透過加入計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 並傳回 `Customer's order number` 欄位。 |
| `Order item total value (quantity * price)` | 之後銷售時的訂單專案總值 [目錄價格規則、分級折扣和特殊定價](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 在套用任何稅捐、運費或購物車折扣之前使用。 將計算方式為 `qty_ordered` 依據 `base_price`. |
| `Order's coupon_code` | 套用至訂單的優惠券。 透過加入計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 並傳回 `coupon_code` 欄位。 |
| `Order's increment_id` | 訂單的唯一識別碼。 透過加入計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 並傳回 `increment_id` 欄位。 |
| `Order's status` | 訂單的狀態。 透過加入計算 `sales_order_item.order_id` 至 `sales_order.entity_id` 並傳回 `status` 欄位。 |
| `Store name` | 與訂單專案相關聯的Commerce商店名稱。 透過加入計算 `sales_order_item.store_id` 至 `store.store_id` 並傳回 `name` 欄位。 |

{style="table-layout:auto"}

## 通用量度

| **量度名稱** | **說明** | **建構** |
|---|---|---|
| `Products ordered` | 銷售時包含在購物車中的產品總數 | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | 在套用目錄價格規則、階層式折扣和特殊定價之後，以及在套用任何稅捐、運費或購物車折扣之前，購物車中包含的產品總價值 | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` 聯結路徑

`catalog_product_entity`

* 加入 `catalog_product_entity` 表格以建立傳回與訂單料號相關聯之產品屬性的欄位。
   * 路徑： `sales_order_item.product_id` （許多） => `catalog_product_entity.entity_id` （一）

`sales_order`

* 加入 `sales_order` 表格，以建立與訂單料號相關的新訂單層次欄位。
   * 路徑： `sales_order_item.order_id` （許多） => `sales_order.entity_id` （一）

`sales_order_item`

* 加入 `sales_order_item` 建立將上層可設定或捆綁SKU的詳細資訊與簡單產品關聯的欄。 [聯絡支援人員](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 以取得設定這些計算的協助(若是在Data Warehouse管理員中建立)。
   * 路徑： `sales_order_item.parent_item_id` （許多） => `sales_order_item.item_id` （一）

`store`

* 加入 `store` 此表格可建立傳回與訂單專案相關Commerce商店詳細資訊的欄。
   * 路徑： `sales_order_item.store_id` （許多） => `store.store_id` （一）
