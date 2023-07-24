---
title: 报价表
description: 了解如何使用报价表。
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# 报价表

此 `quote` 表(`sales_flat_quote` ，其中包含您商店中创建的每个购物车的记录，无论它们是已被放弃还是转换为购买。 每一行表示一个购物车。 由于此表可能很大，因此Adobe建议您在满足某些条件时定期删除记录，例如，如果有任何超过60天的未转换购物车。

>[!NOTE]
>
>只有当您不从以下位置删除记录时，才可能分析历史、放弃的购物车 `quote` 表格。 如果确实删除了记录，则只能查看尚未从数据库中删除的购物车。

## 通用本机列

| **列名称** | **描述** |
|---|---|
| `base_currency_code` | 中捕获的所有值的货币 `base_*` 字段(即 `base_grand_total`， `base_subtotal`，等等)。 这通常反映了Commerce商店的默认货币 |
| `base_grand_total` | 应用所有税费、运费和折扣后，购物车向客户报价的最终价格。 虽然精确计算是可自定义的，但通常 `base_grand_total` 计算方式为 `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | 购物车中包含的所有商品的商品总价值。 不包含税金、运费、折扣等 |
| `created_at` | 购物车的创建时间戳，以UTC本地存储。 取决于您在中的配置 [!DNL Commerce Intelligence]时，此时间戳可能会转换为中的报表时区 [!DNL Commerce Intelligence] 与您的数据库时区不同 |
| `customer_email` | 创建购物车的客户的电子邮件地址 |
| `customer_id` | `Foreign key` 与 `customer_entity` 表（如果客户已注册）。 加入 `customer_entity.entity_id` 以确定与创建购物车的用户关联的客户属性。 如果购物车是通过访客结帐创建的，则此字段为 `NULL` |
| `entity_id` (PK) | 表的唯一标识符，通常用于连接Commerce实例中的其他表 |
| `is_active` | 布尔字段，如果购物车由客户创建且尚未转换为订单，则返回“1”。 对于已转换的购物车或通过管理员创建的购物车，返回“0” |
| `items_qty` | 购物车中包含的所有物料的总数量 |
| `reserved_order_id` | `Foreign key` 与 `sales_order` 表格。 加入 `sales_order.increment_id` 以确定与已转换购物车关联的订单详细信息。 对于未与已转换订单关联的购物车， `reserved_order_id` 残留 `NULL` |
| `store_id` | `Foreign key` 与 `store` 表格。 加入 `store`.`store_id` 以确定哪个Commerce商店视图与购物车关联 |

{style="table-layout:auto"}

## 通用计算列

| **列名称** | **描述** |
|---|---|
| `Order date` | 反映已转换购物车的订单创建日期的时间戳。 通过加入计算 `quote.reserved_order_id` 到 `sales_order.increment_id` 并返回 `sales_order.created_at` 字段 |
| `Seconds between cart creation and order` | 从购物车创建到订单创建之间经过的时间。 通过减法计算 `created_at` 起始日期 `Order date`，以整数秒数返回 |
| `Seconds since cart creation` | 从购物车的创建日期到现在之间经过的时间。 通过减法计算 `created_at` 从执行查询时的服务器时间戳返回，以整数秒数形式返回。 最常用于识别购物车的年龄 |
| `Store name` | 与此订单关联的Commerce商店的名称。 通过加入计算 `quote.store_id` 到 `store.store_id` 并返回 `name` 字段 |

{style="table-layout:auto"}

## 常用量度

| **量度名称** | **描述** | **构造** |
|---|---|---|
| `Number of abandoned carts` | 满足特定“放弃”条件的购物车数量 | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>过滤器：<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x，其中“x”对应于自创建购物车以来经过的时间（以秒为单位），超过该时间，购物车将被视为放弃 |
| `Avg time to cart conversion` | 从创建购物车到创建已转换购物车的订单之间的平均时间 | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | 放弃的购物车潜在收入的总和，其中收入被定义为 `base_grand_total` 字段 | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>过滤器：<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x，其中“x”对应于自创建购物车以来经过的时间（以秒为单位），超过该时间，购物车将被视为放弃 |

{style="table-layout:auto"}

## 外键连接路径

`customer_entity`

* 加入 `customer_entity` 表，用于创建与创建购物车的客户关联的新客户级别列。
   * 路径： `quote.customer_id` （许多） => `customer_entity.entity_id` （一）

`sales_order`

* 加入 `sales_order` 表以创建与已转换购物车关联的退货单详细信息的列。
   * 路径：`quote.reserved_order_id` （许多） => `sales_order.increment_id` （一）

`store`

* 加入 `store` 表以创建列，这些列返回与购物车关联的Commerce商店相关的详细信息。
   * 路径： `quote.store_id` （许多） => `store.store_id` （一）
