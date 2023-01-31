---
title: 引用表
description: 了解如何使用报价表。
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# 报价表

的 `quote` 表(`sales_flat_quote` （在M1上）包含在您的商店中创建的每个购物车上的记录，无论这些记录是被放弃还是转化为购买。 每行表示一个购物车。 由于此表的潜在大小，我们建议您在满足某些标准（例如，如果有任何未转换的购物车超过60天）时定期删除记录。

>[!NOTE]
>
>只有在不从 `quote` 表。 如果删除记录，您将只能看到尚未从数据库中删除的购物车。

## 常用本机列

| **列名称** | **描述** |
|---|---|
| `base_currency_code` | 中捕获的所有值的货币 `base_*` 字段( `base_grand_total`, `base_subtotal`，等等)。 这通常反映商店的默认货币 |
| `base_grand_total` | 在应用所有税、运费和折扣后，为购物车客户报价的最终价格。 虽然精确计算是可自定义的，但通常情况下， `base_grand_total` 计算为 `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | 购物车中所有物品的总商品价值。 不包括税、运费、折扣等 |
| `created_at` | 购物车的创建时间戳，通常以UTC存储在本地。 根据您在 [!DNL MBI]，此时间戳可能会转换为 [!DNL MBI] 与数据库时区不同 |
| `customer_email` | 创建购物车的客户的电子邮件地址 |
| `customer_id` | `Foreign key` 与 `customer_entity` 表中。 加入 `customer_entity.entity_id` 以确定与创建购物车的用户关联的客户属性。 如果购物车是通过来宾结帐创建的，则此字段将为 `NULL` |
| `entity_id` (PK) | 表的唯一标识符，通常用于连接到Commerce实例中的其他表 |
| `is_active` | 布尔字段，用于在客户创建购物车且尚未转换为订单时返回“1”。 对于已转换的购物车或通过管理员创建的购物车，返回“0” |
| `items_qty` | 购物车中所有项目的总数量 |
| `reserved_order_id` | `Foreign key` 与 `sales_order` 表。 加入 `sales_order.increment_id` 以确定与已转换购物车关联的订单详细信息。 对于与已转换订单无关联的购物车， `reserved_order_id` 将继续 `NULL` |
| `store_id` | `Foreign key` 与 `store` 表。 加入 `store`.`store_id` 确定与购物车关联的商店视图 |

{style=&quot;table-layout:auto&quot;}

## 常用计算列

| **列名称** | **描述** |
|---|---|
| `Order date` | 反映已转换购物车的订单创建日期的时间戳。 通过连接计算 `quote.reserved_order_id` to `sales_order.increment_id` 并返回 `sales_order.created_at` 字段 |
| `Seconds between cart creation and order` | 购物车创建和订单创建之间经过的时间。 通过减法计算 `created_at` 从 `Order date`，返回为整数秒 |
| `Seconds since cart creation` | 购物车创建日期与现在之间经过的时间。 通过减法计算 `created_at` 从执行查询时的服务器时间戳返回，以整数秒为单位。 最常用于识别购物车的年龄 |
| `Store name` | 与此订单关联的商务商店的名称。 通过连接计算 `quote.store_id` to `store.store_id` 并返回 `name` 字段 |

{style=&quot;table-layout:auto&quot;}

## 常用量度

| **量度名称** | **描述** | **建筑** |
|---|---|---|
| `Number of abandoned carts` | 满足特定“放弃”条件的购物车计数 | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>过滤器：<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x，其中“x”对应于自购物车创建后经过的时间（以秒为单位），在创建购物车之后，购物车将被视为放弃 |
| `Avg time to cart conversion` | 转化购物车的购物车创建和订单创建之间的平均时间 | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | 放弃购物车潜在收入的总和，其中收入定义为 `base_grand_total` 字段 | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>过滤器：<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x，其中“x”对应于自购物车创建后经过的时间（以秒为单位），在创建购物车之后，购物车将被视为放弃 |

{style=&quot;table-layout:auto&quot;}

## 外键连接路径

`customer_entity`

* 加入 `customer_entity` 用于创建与创建购物车的客户关联的新客户级别列的表。
   * 路径： `quote.customer_id` （多个）=> `customer_entity.entity_id` (1)

`sales_order`

* 加入 `sales_order` 表格以创建新列，返回与已转换购物车关联的订单详细信息。
   * 路径：`quote.reserved_order_id` （多个）=> `sales_order.increment_id` (1)

`store`

* 加入 `store` 用于创建新列，以返回与购物车关联的商务商店相关的详细信息。
   * 路径： `quote.store_id` （多个）=> `store.store_id` (1)
