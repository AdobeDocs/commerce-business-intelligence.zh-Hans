---
title: enterprise_rma表格
description: 瞭解如何分析有關特定回訪請求的資訊。
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# enterprise_rma表格

中的每一列 `enterprise_rma` 表格(通常稱為 `magento_rma` Adobe Commerce （但可自訂名稱）包含特定回訪請求的相關資訊。

>[!NOTE]
>
>唯有當您是Adobe Commerce帳戶成員時，此表格才隨附於標準配備 `Enterprise Edition` 或 `Enterprise Cloud Edition` 客戶。

## 通用原生欄

| **欄名稱** | **說明** |
|---|---|
| `entity\_id` | 資料表的唯一識別碼。 每個 `entity\_id` 代表傳回要求。 |
| `date\_requested` | 要求退貨的日期。 |
| `status` | 傳回的狀態。 值包括「received」、「pending」、「authorized」等。 |
| `order\_id` | 與關聯的外來鍵 `sales\_flat\_order` 表格。 |
| `customer\_id` | 與關聯的外來鍵 `customer\_entity` 表格。 |

{style="table-layout:auto"}

## 通用計算欄

| **欄名稱** | **說明** |
|---|---|
| `Order's created\_at` | 這是原始訂單的日期。 這可用來取得訂單與退貨要求之間的時間。 |
| `Customer's order number` | 這是與原始訂單相關聯的客戶訂單編號。 |
| `Seconds between order's created\_at and return's date\_requested` | 從訂購日期到退貨請求的秒數。 |
| `Return's total value` | 這是傳回的總金額。 這是各退貨專案的個別退貨金額總和。 |

{style="table-layout:auto"}

## 通用量度

| **量度名稱** | **說明** | **建構** |
|---|---|---|
| `Number of returns` | 要求的傳回次數。 | `Operation` 欄： `entity id`<br>`Operation`： `Count`<br>`Timestamp` 欄： `date requested` |
| `Total returned amount` | 傳回的總金額。 | `Operation `欄： `Return's total value`<br>`Operation`：總和<br>`Timestamp` 欄：要求的日期 |
| `Average returned amount` | 傳回的平均貨幣金額。 | `Operation`` Column: Return's total value`<br>`Operation`： `Average`<br>`Timestamp` 欄： `date requested` |
| `Average time to return` | 從訂單到退貨的平均時間。 | `Operation` 欄：訂單建立日期與退貨請求日期之間的秒數<br>`Operation`： `Average`<br>`Timestamp` 欄： `date requested` |

{style="table-layout:auto"}

## 連線到其他表格

`sale_flat_order`

* 建立聯結欄以依據上的訂單層級屬性進行區段和篩選 `enterprise_rma` 表格透過下列聯結：
   * Commerce 1.x： `enterprise_rma.order_id` （許多） => `sales_flat_order.entity_id` （一）
   * Commerce 2.x： `magento_rma.order_id` （許多） => `sales_order.entity_id` （一）

`enterprise_rma_item_entity`

* 建立多對一欄，例如 `Return's total value` 於 `enterprise_rma` 表格透過下列聯結：
   * Commerce 1.x： `enterprise_rma_item_entity.rma_entity_id` （許多） => `enterprise_rma.entity_id` （一）
   * Commerce 2.x： `magento_rma_item_entity.rma_entity_id ` （許多） => `magento_rma.entity_id` （一）
