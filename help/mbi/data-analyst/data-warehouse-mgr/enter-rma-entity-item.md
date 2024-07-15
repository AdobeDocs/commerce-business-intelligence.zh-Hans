---
title: Enterprise_Rma_Item_Entity表
description: 了解如何分析请求返回中有关特定项目的信息。
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# enterprise_rma_item_entity表

`enterprise_rma_item_entity`表(在Commerce 2.x中通常称为`magento_rma_item_entity`，但可以自定义名称)中的每一行都包含有关所请求返回的特定项的信息。

>[!NOTE]
>
>仅当您是`Enterprise Edition`或`Enterprise Cloud Edition`客户时，此表格才包含在您的Commerce帐户中。

## 通用本机列

| **列名称** | **描述** |
|---|---|
| `entity\_id` | 表的唯一标识符。 每个`entity\_id`表示已请求返回的项。 |
| `rma\_entity\_id` | 与`enterprise\_rma`表关联的外键。 |
| `status` | 项目返回的状态。 值包括“received”、“pending”、“authorized”等。 此状态的值可能与总体返回状态的值不匹配。 |
| `qty\_requested` | 客户请求的退货数量。 |
| `qty\_approved` | 批准退货的数量。 |
| `qty\_returned` | 退回的数量。 |
| `order\_item\_id` | 与`sales\_flat\_order\_item`表关联的外键。 |
| `product\_sku` | 返回的SKU。 |

{style="table-layout:auto"}

## 通用计算列

| **列名称** | **描述** |
|---|---|
| `Return date\_requested` | 这是客户请求退货的日期。 |
| `Item price` | 项目的价格。 |
| `Return item's total value (qty\_returned * price)` | 这是返回的项目的货币总值。 用于计算`enterprise\_rma`表上的总退货金额。 |

{style="table-layout:auto"}

## 常用量度

| **量度名称** | **描述** | **构造** |
|---|---|---|
| `Number of items returned` | 返回的项目数。 | 操作列：返回的数量<br>操作： Sum<br>时间戳列：请求的返回日期 |
| `Returned items' total value` | 返回的货币金额。 | 操作列：返回项目的总值（返回数量*价格）<br>操作：总和<br>时间戳列：请求的返回日期 |

{style="table-layout:auto"}

## 与其他表的连接

`enterprise_rma`

* 通过以下联接在`enterprise_rma_item_entity`表上创建联接列（如`Return date\_requested`）：
* Commerce 1.x： `enterprise_rma_item_entity.rma_entity_id ` （多个） => `enterprise_rma.entity_id` （一个）
* Commerce 2.x： `magento_rma_item_entity.rma_entity_id ` （多个）=> `magento_rma.entity_id` （一个）

`sales_flat_order_item`

* 在上创建联接列  通过下列联接的`enterprise_rma_item_entity`表：

* Commerce 1.x： `enterprise_rma_item_entity.order_item_id ` （多个） => `sales_flat_order_item.item_id` （一个）
* Commerce 2.x： `magento_rma_item_entity.order_item_id ` （多个）=> `sales_order_item.item_id` （一个）
