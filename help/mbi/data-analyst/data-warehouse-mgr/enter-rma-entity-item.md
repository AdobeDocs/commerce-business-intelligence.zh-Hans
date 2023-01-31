---
title: Enterprise_Rma_Item_Entity表
description: 了解如何从请求的返回分析有关特定项目的信息。
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# enterprise_rma_item_entity表

中的每一行 `enterprise_rma_item_entity` 表(通常称为 `magento_rma_item_entity` （在Commerce 2.x中，但可以自定义名称）包含有关请求返回中特定项目的信息。

>[!NOTE]
>
>仅当您是 `Enterprise Edition` 或 `Enterprise Cloud Edition` 客户。

## 常用本机列

| **列名称** | **描述** |
|---|---|
| `entity\_id` | 表的唯一标识符。 每个 `entity\_id` 表示已请求返回的项目。 |
| `rma\_entity\_id` | 与关联的外键 `enterprise\_rma` 表。 |
| `status` | 项目返回的状态。 值包括“已接收”、“待定”、“已授权”等。 此状态中的值不一定与整体返回状态的值匹配。 |
| `qty\_requested` | 客户请求退货的数量。 |
| `qty\_approved` | 批准退回的数量。 |
| `qty\_returned` | 实际返回的数量。 |
| `order\_item\_id` | 与关联的外键 `sales\_flat\_order\_item` 表。 |
| `product\_sku` | 返回的SKU。 |

{style=&quot;table-layout:auto&quot;}

## 常用计算列

| **列名称** | **描述** |
|---|---|
| `Return date\_requested` | 这是客户请求退货的日期。 |
| `Item price` | 项目的价格。 |
| `Return item's total value (qty\_returned * price)` | 这是返回项目的总货币值。 此值将用于计算 `enterprise\_rma` 表。 |

{style=&quot;table-layout:auto&quot;}

## 常用量度

| **量度名称** | **描述** | **建筑** |
|---|---|---|
| `Number of items returned` | 返回的项目数。 | 工序列：返回的数量<br>操作：总和<br>时间戳列：请求的返回日期 |
| `Returned items' total value` | 返回的货币金额。 | 操作列：退货项目的总值（退货数量*价格）<br>操作：总和<br>时间戳列：请求的返回日期 |

{style=&quot;table-layout:auto&quot;}

## 与其他表的连接

`enterprise_rma`

* 创建联接的列，如 `Return date\_requested` 在 `enterprise_rma_item_entity` 表格：
* 商务1.x: `enterprise_rma_item_entity.rma_entity_id ` （多个）=> `enterprise_rma.entity_id` (1)
* 商务2.x: `magento_rma_item_entity.rma_entity_id ` （多个）=> `magento_rma.entity_id` (1)

`sales_flat_order_item`

* 在  `enterprise_rma_item_entity` 表格：

* 商务1.x: `enterprise_rma_item_entity.order_item_id ` （多个）=> `sales_flat_order_item.item_id` (1)
* 商务2.x: `magento_rma_item_entity.order_item_id ` （多个）=> `sales_order_item.item_id` (1)
