---
title: sales_order表
description: 了解如何使用sales_order表。
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# `sales_order` 表

此 `sales_order` 表(`sales_flat_order` （在M1上）是捕获每个订单的位置。 通常，每行表示一个唯一订单，尽管Commerce的一些自定义实施会导致将订单拆分为单独的行。

此表包含所有客户订单，无论该订单是通过访客结帐处理的。 如果您的商店接受访客结帐，则可以找到有关此内容的更多信息 [用例](../data-warehouse-mgr/guest-orders.md).

## 公用列

| **列名称** | **描述** |
|---|---|
| `base_currency_code` | 中捕获的所有值的货币 `base_*` 字段(即 `base_grand_total`， `base_subtotal`，等等)。 这通常反映了Commerce商店的默认货币 |
| `base_discount_amount` | 应用于订单的折扣值 |
| `base_grand_total` | 应用所有税费、运费和折扣后，客户在订单上支付的最终价格。 虽然精确计算是可自定义的，但通常 `base_grand_total` 计算方式为 `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | 订单内所有项目之商品总值。 不包含税金、运费、折扣等 |
| `base_shipping_amount` | 应用于订单的装运值 |
| `base_tax_amount` | 应用于订单的税值 |
| `billing_address_id` | `Foreign key` 与 `sales_order_address` 表格。 加入 `sales_order_address.entity_id` 确定与订单关联的帐单地址详细信息 |
| `coupon_code` | 订单申请的优惠券。 如果未应用优惠券，则此字段为 `NULL` |
| `created_at` | 订单的创建时间戳，以UTC本地存储。 取决于您在中的配置 [!DNL MBI]时，此时间戳可能会转换为中的报表时区 [!DNL MBI] 与您的数据库时区不同 |
| `customer_email` | 下订单客户的电子邮件地址。 在所有情况下都填充此字段，包括通过访客结帐处理的订单 |
| `customer_group_id` | 与关联的外键 `customer_group` 表格。 加入 `customer_group.customer_group_id` 以确定与订单关联的客户组 |
| `customer_id` | `Foreign key` 与 `customer_entity` 表（如果客户已注册）。 加入 `customer_entity.entity_id` 以确定与订单关联的客户属性。 如果订单是通过访客结帐发出的，则此字段为 `NULL` |
| `entity_id` (PK) | 表的唯一标识符，通常用于连接Commerce实例中的其他表 |
| `increment_id` | 订单的唯一标识符，通常称为 `order_id` 在Adobe Commerce中。 此 `increment_id` 最常用于连接到外部源，例如 [!DNL Google Ecommerce] |
| `shipping_address_id` | 与关联的外键 `sales_order_address` 表格。 加入 `sales_order_address.entity_id` 确定与订单关联的配送地址详细信息 |
| `status` | 订单状态。 可以返回诸如“complete”、“processing”、“canceled”、“refulred”之类的值，以及在商务实例上实施的任何自定义状态。 处理订单时可能会发生更改 |
| `store_id` | `Foreign key` 与 `store` 表格。 加入 `store`.`store_id` 以确定与订单关联的Commerce商店视图 |

{style="table-layout:auto"}

## 通用计算列

| **列名称** | **描述** |
|---|---|
| `Billing address city` | 订单的计费城市。 通过加入计算 `sales_order`.`billing_address_id` 到 `sales_order_address`.`entity_id` 并返回 `city` 字段 |
| `Billing address country` | 订单的计费国家/地区代码。 通过加入计算 `sales_order`.`billing_address_id` 到 `sales_order_address`.`entity_id` 并返回 `country_id` |
| `Billing address region` | 订单的计费区域（通常为州或省）。 通过加入计算 `sales_order`.`billing_address_id` 到 `sales_order_address`.`entity_id` 并返回 `region` 字段 |
| `Customer's first order date` | 此客户下第一个订单的时间戳。 通常被认为是客户的“收购日期”。 通过返回最小值来计算 `sales_order`.`created_at` 每个独特客户的值 |
| `Customer's first order's billing region` | 下订单的客户的客户的客户获取开单区域。 计算方式为返回 `Billing address region` 与客户的第一笔订单相关联 |
| `Customer's first order's coupon_code` | 下此订单的客户的客户获取优惠券代码。 计算方式为返回 `coupon_code` 与客户的第一笔订单相关联 |
| `Customer's group code` | 下此订单的客户的组名称。 通过加入计算 `sales_order`.`customer_group_id` 到 `customer_group`.`customer_group_id` 并返回 `customer_group_code` 字段 |
| `Customer's lifetime number of coupons` | 应用于此客户所下所有订单的优惠券总数。 通过计数订单数来计算，其中 `coupon_code` 不是 `NULL` 每个独特客户 |
| `Customer's lifetime number of orders` | 此客户下达的订单总数。 通过计数行数 `sales_order` 每个独特客户的表 |
| `Customer's lifetime revenue` | 此客户下达的所有订单的总收入。 计算方式为将 `base_grand_total` 每个独特客户的所有订单的字段 |
| `Customer's order number` | 此客户订单的连续订单排名。 通过识别客户下达的所有订单，按 `created_at` 时间戳，并为每个订单分配一个递增的整数值。 例如，客户的第一笔订单会返回 `Customer's order number` （共1个），客户的第二个订单返回 `Customer's order number` 共2个，以此类推。 |
| `Customer's order number (previous-current)` | 客户上一订单的排名与此订单的排名关联，以 `-` 字符。 通过连接(&quot;计算`Customer's order number` - 1”)，带有&quot;`-`“ ，后跟“`Customer's order number`“。 例如，对于与客户第二次购买关联的订单，此列返回值 `1-2`. 最常用于表示两个订单事件之间的时间（即“订单之间的时间”图表中的） |
| `Is customer's last order?` | 确定订单对应于客户的上次订单还是最近订单。 通过比较 `Customer's order number` 值 `Customer's lifetime number of orders`. 当这两个字段在给定顺序中相等时，此列返回“是”；否则，它返回“否” |
| `Number of items in order` | 订单中包含的物料总数。 通过加入计算 `sales_order`.`entity_id` 到 `sales_order_item`.`order_id` 并总结 `sales_order_item`.`qty_ordered` 字段 |
| `Seconds between customer's first order date and this order` | 此订单与客户首次订单之间的间隔时间。 通过减法计算 `Customer's first order date` 从 `created_at` 对于每个订单，以整数秒数返回 |
| `Seconds since previous order` | 此订单与客户紧接上一订单之间的间隔时间。 计算方式为将 `created_at` 对于来自的上一个订单 `created_at` 的整数，以秒数的形式返回。 例如，对于与客户第三张订单对应的订单记录，此列返回客户第二张订单与第三张订单之间的秒数。 对于客户的第一笔订单，此字段将返回 `NULL` |
| `Shipping address city` | 订单的运输城市。 通过加入计算 `sales_order`.`shipping_address_id` 到 `sales_order_address`.`entity_id` 并返回 `city` 字段 |
| `Shipping address country` | 订单的装运国家/地区代码。 通过加入计算 `sales_order`.`Shipping_address_id` 到 `sales_order_address`.`entity_id` 并返回 `country_id` |
| `Shipping address region` | 订单的运输区域（通常为州或省）。 通过加入计算 `sales_order`.`shipping_address_id` 到 `sales_order_address`.`entity_id` 并返回 `region` 字段 |
| `Store name` | 与此订单关联的Commerce商店的名称。 通过加入计算 `sales_order`.`store_id` 到 `store`.`store_id` 并返回 `name` 字段 |

## 常用量度

| **量度名称** | **描述** | **构造** |
|---|---|---|
| `Avg order value` | 每订单的平均收入，其中收入被定义为 `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | 客户的(n-1)订单与第n订单之间的平均时间（对于所有客户和订单） | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | 在应用所有税和折扣之前，所有订单的商品总价值的总和，其中GMV定义为小计 | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | 客户(n-1)订单与第n订单之间的中间时间（对于所有客户和订单） | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | 已下订单总数 | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | 所有订单的收入总和，其中收入定义为客户支付的最终价格，扣除所有税项、折扣、装运等后，均适用 | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | 所有订单的装运金额总和 | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | 应用于所有订单的税的总和 | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | 在给定报告时间间隔内下订单的唯一客户数。 例如，如果报表的间隔是每周，则在给定周内至少下一次订单的每个客户都将被计算一次，而不管他们在该周下了多少订单 | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` 联接路径

`customer_entity`

* 加入 `customer_entity` 表，用于创建与下订单的客户关联的新客户层列。
   * 路径： `sales_order.customer_id` （许多） => `customer_entity.entity_id` （一）

`customer_group`

* 加入 `customer_group` 表，用于创建返回下订单的客户的客户组名称的列。
   * 路径： `sales_order.customer_group_id` （许多） => `customer_group.customer_group_id` （一）

`sales_order_address`

* 加入 `sales_order_address` 表，以创建返回与订单关联的开单和发运地点的列。 根据是否需要帐单或送货详细信息，可以使用两个连接路径。
   * 路径：
      * 配送： `sales_order.shipping_address_id`（许多） => `sales_order_address.entity_id` （一）
      * 帐单： `sales_order.billing_address_id`（许多） => `sales_order_address.entity_id` （一）

`store`

* 加入 `store` 表，用于创建返回与订单关联的Commerce商店相关的详细信息的列。
   * 路径： `sales_order.store_id` （许多） => `store.store_id` （一）
