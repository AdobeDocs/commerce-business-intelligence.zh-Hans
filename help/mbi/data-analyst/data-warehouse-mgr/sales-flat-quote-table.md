---
title: 报价表
description: 了解如何使用报价表。
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# 报价表

`quote`表（ M1上的`sales_flat_quote`）包含您商店中创建的每个购物车的记录，无论它们是放弃的还是转换为购买的。 每一行表示一个购物车。 由于此表可能的大小问题，Adobe建议您在满足某些条件时定期删除记录，例如，如果有任何超过60天的未转换购物车。

>[!NOTE]
>
>仅当不从`quote`表中删除记录时，才可能分析已放弃的历史购物车。 如果确实删除了记录，则只能看到尚未从数据库中删除的购物车。

## 通用本机列

| **列名称** | **描述** |
|---|---|
| `base_currency_code` | 在`base_*`字段（即`base_grand_total`、`base_subtotal`等）中捕获的所有值的货币。 这通常反映了Commerce商店的默认货币 |
| `base_grand_total` | 应用所有税费、运费和折扣后，购物车为客户报价的最终价格。 虽然精确计算可自定义，但通常`base_grand_total`的计算方式为`base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | 购物车中包含的所有商品的总商品价值。 不包含税、运费、折扣等 |
| `created_at` | 购物车的创建时间戳，以UTC本地存储。 根据[!DNL Commerce Intelligence]中的配置，此时间戳可能会转换为[!DNL Commerce Intelligence]中与数据库时区不同的报表时区 |
| `customer_email` | 创建购物车的客户的电子邮件地址 |
| `customer_id` | 与`customer_entity`表关联的`Foreign key`（如果已注册客户）。 加入`customer_entity.entity_id`以确定与创建购物车的用户关联的客户属性。 如果购物车是通过访客结帐创建的，则此字段为`NULL` |
| `entity_id` (PK) | 表的唯一标识符，通常用于联接Commerce实例中的其他表 |
| `is_active` | 如果购物车由客户创建且尚未转换为订单，则返回值为“1”的布尔字段。 对于已转换的购物车或通过管理员创建的购物车，返回“0” |
| `items_qty` | 购物车中包含的所有物料的总量 |
| `reserved_order_id` | 与`sales_order`表关联的`Foreign key`。 加入`sales_order.increment_id`以确定与已转换购物车关联的订单详细信息。 对于未与已转换订单关联的购物车，`reserved_order_id`仍为`NULL` |
| `store_id` | 与`store`表关联的`Foreign key`。 加入`store`。`store_id`以确定哪个Commerce商店视图与购物车关联 |

{style="table-layout:auto"}

## 通用计算列

| **列名称** | **描述** |
|---|---|
| `Order date` | 反映已转换购物车的订单创建日期的时间戳。 通过将`quote.reserved_order_id`加入`sales_order.increment_id`并返回`sales_order.created_at`字段进行计算 |
| `Seconds between cart creation and order` | 从购物车创建到订单创建之间经过的时间。 通过从`Order date`中减去`created_at`计算，以整数秒数返回 |
| `Seconds since cart creation` | 从购物车创建日期到现在之间经过的时间。 通过执行查询时从服务器时间戳中减去`created_at`计算，以整数秒数返回。 最常用于识别购物车的年龄 |
| `Store name` | 与此订单关联的Commerce商店的名称。 通过将`quote.store_id`加入`store.store_id`并返回`name`字段进行计算 |

{style="table-layout:auto"}

## 常用量度

| **量度名称** | **描述** | **构造** |
|---|---|---|
| `Number of abandoned carts` | 满足特定“放弃”条件的购物车数量 | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>筛选器：<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x，其中“x”对应于自创建购物车以来经过的时间（以秒为单位），超过该时间，购物车将被放弃 |
| `Avg time to cart conversion` | 从创建购物车到为已转换购物车创建订单之间的平均时间 | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | 放弃的购物车潜在收入的总和，其中收入定义为`base_grand_total`字段 | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>筛选器：<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x，其中“x”对应于自创建购物车以来经过的时间（以秒为单位），超过该时间，购物车将被放弃 |

{style="table-layout:auto"}

## 外键连接路径

`customer_entity`

* 加入`customer_entity`表以创建与创建购物车的客户关联的新客户级列。
   * 路径： `quote.customer_id` （多个） => `customer_entity.entity_id` （一个）

`sales_order`

* 加入`sales_order`表以创建返回与已转换购物车关联的订单详细信息的列。
   * 路径：`quote.reserved_order_id` （多个） => `sales_order.increment_id` （一个）

`store`

* 加入`store`表以创建列，这些列返回与购物车关联的Commerce商店相关的详细信息。
   * 路径： `quote.store_id` （多个） => `store.store_id` （一个）
