---
title: Enterprise_Rma_Item_Entity表格
description: 瞭解如何從要求的傳回中分析有關特定專案的資訊。
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# enterprise_rma_item_entity表格

中的每一列 `enterprise_rma_item_entity` 表格(通常稱為 `magento_rma_item_entity` 在Commerce 2.x中，但可自訂名稱)包含請求傳回的特定專案相關資訊。

>[!NOTE]
>
>唯有當您是商務帳戶成員時，此表格才隨附標準 `Enterprise Edition` 或 `Enterprise Cloud Edition` 客戶。

## 通用原生欄

| **欄名稱** | **說明** |
|---|---|
| `entity\_id` | 資料表的唯一識別碼。 每個 `entity\_id` 代表已要求退貨的專案。 |
| `rma\_entity\_id` | 與關聯的外來鍵 `enterprise\_rma` 表格。 |
| `status` | 專案傳回的狀態。 值包括「received」、「pending」、「authorized」等。 此狀態的值可能與整體傳回狀態的值不符。 |
| `qty\_requested` | 客戶要求退貨的數量。 |
| `qty\_approved` | 核准退貨的數量。 |
| `qty\_returned` | 退貨數量。 |
| `order\_item\_id` | 與關聯的外來鍵 `sales\_flat\_order\_item` 表格。 |
| `product\_sku` | 正在傳回的SKU。 |

{style="table-layout:auto"}

## 通用計算欄

| **欄名稱** | **說明** |
|---|---|
| `Return date\_requested` | 這是客戶要求退貨的日期。 |
| `Item price` | 專案的價格。 |
| `Return item's total value (qty\_returned * price)` | 這是傳回專案的總貨幣值。 用於計算以下專案的總退貨金額： `enterprise\_rma` 表格。 |

{style="table-layout:auto"}

## 通用量度

| **量度名稱** | **說明** | **建構** |
|---|---|---|
| `Number of items returned` | 傳回的專案數。 | 作業資料行：傳回數量<br>作業：總和<br>時間戳記欄：要求的傳回日期 |
| `Returned items' total value` | 傳回的貨幣金額。 | 作業欄位：退貨料號的總值（退貨數量*價格）<br>作業：總和<br>時間戳記欄：要求的傳回日期 |

{style="table-layout:auto"}

## 連線到其他表格

`enterprise_rma`

* 建立聯結欄，例如 `Return date\_requested` 於 `enterprise_rma_item_entity` 表格透過下列聯結：
* Commerce 1.x： `enterprise_rma_item_entity.rma_entity_id ` （許多） => `enterprise_rma.entity_id` （一）
* Commerce 2.x： `magento_rma_item_entity.rma_entity_id ` （許多） => `magento_rma.entity_id` （一）

`sales_flat_order_item`

* 在上建立聯結欄  `enterprise_rma_item_entity` 表格透過下列聯結：

* Commerce 1.x： `enterprise_rma_item_entity.order_item_id ` （許多） => `sales_flat_order_item.item_id` （一）
* Commerce 2.x： `magento_rma_item_entity.order_item_id ` （許多） => `sales_order_item.item_id` （一）
