---
title: enterprise_rma表
description: 了解如何分析有关特定返回请求的信息。
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# enterprise_rma表

中的每一行 `enterprise_rma` 表(通常称为 `magento_rma` （在Commerce 2.x中，但可以自定义名称）包含有关特定返回请求的信息。

>[!NOTE]
>
>仅当您是 `Enterprise Edition` 或 `Enterprise Cloud Edition` 客户。

## 常用本机列

| **列名称** | **描述** |
|---|---|
| `entity\_id` | 表的唯一标识符。 每个 `entity\_id` 表示返回请求。 |
| `date\_requested` | 请求返回的日期。 |
| `status` | 返回的状态。 值包括“已接收”、“待定”、“已授权”等。 |
| `order\_id` | 与关联的外键 `sales\_flat\_order` 表。 |
| `customer\_id` | 与关联的外键 `customer\_entity` 表。 |

{style=&quot;table-layout:auto&quot;}

## 常用计算列

| **列名称** | **描述** |
|---|---|
| `Order's created\_at` | 这是原始订单的日期。 这可用于获取订单和退货请求之间的时间。 |
| `Customer's order number` | 这是与原始订单关联的客户订单编号。 |
| `Seconds between order's created\_at and return's date\_requested` | 从订单日期到返回请求的秒数。 |
| `Return's total value` | 这是返回的总货币金额。 这将是每个回访项目的单个回访金额的总和。 |

{style=&quot;table-layout:auto&quot;}

## 常用量度

| **量度名称** | **描述** | **建筑** |
|---|---|---|
| `Number of returns` | 请求的返回次数。 | `Operation` 列： `entity id`<br>`Operation`: `Count`<br>`Timestamp` 列： `date requested` |
| `Total returned amount` | 返回的总货币金额。 | `Operation `列： `Return's total value`<br>`Operation`:总和<br>`Timestamp` 列：请求的日期 |
| `Average returned amount` | 返回的平均货币金额。 | `Operation`` Column: Return's total value`<br>`Operation`: `Average`<br>`Timestamp` 列： `date requested` |
| `Average time to return` | 从订单返回的平均时间。 | `Operation` 列：订单创建日期与请求返回日期之间的秒数<br>`Operation`: `Average`<br>`Timestamp` 列： `date requested` |

{style=&quot;table-layout:auto&quot;}

## 与其他表的连接

`sale_flat_order`

* 创建联接的列，以按 `enterprise_rma` 表格：
   * 商务1.x: `enterprise_rma.order_id` （多个）=> `sales_flat_order.entity_id` (1)
   * 商务2.x: `magento_rma.order_id` （多个）=> `sales_order.entity_id` (1)

`enterprise_rma_item_entity`

* 创建多对一列，例如 `Return's total value` 在 `enterprise_rma` 表格：
   * 商务1.x: `enterprise_rma_item_entity.rma_entity_id` （多个）=> `enterprise_rma.entity_id` (1)
   * 商务2.x: `magento_rma_item_entity.rma_entity_id ` （多个）=> `magento_rma.entity_id` (1)
