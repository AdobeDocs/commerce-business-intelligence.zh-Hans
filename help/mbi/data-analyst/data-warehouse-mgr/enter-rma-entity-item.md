---
title: Enterprise_Rma_Item_Entity表
description: 了解如何分析请求返回中有关特定项目的信息。
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 1%

---

# enterprise_rma_item_entity表

中的每一行 `enterprise_rma_item_entity` 表(通常称为 `magento_rma_item_entity` 在Commerce 2.x中，但可以自定义名称)包含有关所请求返回的特定项的信息。

>[!NOTE]
>
>仅当您是Commerce帐户成员时，此表才随附于标准值 `Enterprise Edition` 或 `Enterprise Cloud Edition` 客户。

## 通用本机列

| **列名称** | **描述** |
|---|---|
| `entity\_id` | 表的唯一标识符。 每个 `entity\_id` 表示已请求返回的项。 |
| `rma\_entity\_id` | 与关联的外键 `enterprise\_rma` 表格。 |
| `status` | 项目返回的状态。 值包括“received”、“pending”、“authorized”等。 此状态的值可能与总体返回状态的值不匹配。 |
| `qty\_requested` | 客户请求的退货数量。 |
| `qty\_approved` | 批准退货的数量。 |
| `qty\_returned` | 退回的数量。 |
| `order\_item\_id` | 与关联的外键 `sales\_flat\_order\_item` 表格。 |
| `product\_sku` | 返回的SKU。 |

{style="table-layout:auto"}

## 通用计算列

| **列名称** | **描述** |
|---|---|
| `Return date\_requested` | 这是客户请求退货的日期。 |
| `Item price` | 项目的价格。 |
| `Return item's total value (qty\_returned * price)` | 这是返回的项目的货币总值。 用于计算以下网站的总退货金额： `enterprise\_rma` 表格。 |

{style="table-layout:auto"}

## 常用量度

| **量度名称** | **描述** | **建筑** |
|---|---|---|
| `Number of items returned` | 返回的项目数。 | 操作列：返回的数量<br>操作：总和<br>时间戳列：请求的返回日期 |
| `Returned items' total value` | 返回的货币金额。 | 工序列：退货物料的总值（退货数量x价格）<br>操作：总和<br>时间戳列：请求的返回日期 |

{style="table-layout:auto"}

## 与其他表的连接

`enterprise_rma`

* 创建联接列，例如 `Return date\_requested` 在 `enterprise_rma_item_entity` 表通过以下连接：
* Commerce 1.x： `enterprise_rma_item_entity.rma_entity_id ` （许多） => `enterprise_rma.entity_id` （一）
* Commerce 2.x： `magento_rma_item_entity.rma_entity_id ` （许多） => `magento_rma.entity_id` （一）

`sales_flat_order_item`

* 在上创建联接列  `enterprise_rma_item_entity` 表通过以下连接：

* Commerce 1.x： `enterprise_rma_item_entity.order_item_id ` （许多） => `sales_flat_order_item.item_id` （一）
* Commerce 2.x： `magento_rma_item_entity.order_item_id ` （许多） => `sales_order_item.item_id` （一）
