---
title: sales_order表
description: 了解如何使用sales_order表。
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
source-git-commit: 73373924b7adaffabf643b65bd290ce2d9408574
workflow-type: tm+mt
source-wordcount: '1218'
ht-degree: 0%

---

# `sales_order` 表

的 `sales_order` 表(`sales_flat_order` （在M1上）是捕获每个订单的位置。 在大多数情况下，每行表示一个唯一的顺序，不过有一些自定义的商务实施会导致将顺序拆分为不同的行。

此表包括所有客户订单，无论该订单是否通过来宾结帐处理。 如果您的商店接受来宾结帐，您可以找到有关此内容的更多信息 [用例](../data-warehouse-mgr/guest-orders.md).

## 常用列

| **列名称** | **描述** |
|---|---|
| `base_currency_code` | 中捕获的所有值的货币 `base_*` 字段( `base_grand_total`, `base_subtotal`，等等)。 这通常反映商店的默认货币 |
| `base_discount_amount` | 应用于订单的折扣值 |
| `base_grand_total` | 在应用所有税、运费和折扣后，客户在订单上支付的最终价格。 虽然精确计算是可自定义的，但通常情况下， `base_grand_total` 计算为 `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | 订单中所有项目的总商品价值。 不包括税、运费、折扣等 |
| `base_shipping_amount` | 应用于订单的发运值 |
| `base_tax_amount` | 应用于订单的税值 |
| `billing_address_id` | `Foreign key` 与 `sales_order_address` 表。 加入 `sales_order_address.entity_id` 确定与订单关联的帐单地址详细信息 |
| `coupon_code` | 应用于订购的优惠券。 如果未应用优惠券，则此字段将 `NULL` |
| `created_at` | 订单的创建时间戳，通常以UTC存储在本地。 根据您在 [!DNL MBI]，此时间戳可能会转换为 [!DNL MBI] 与数据库时区不同 |
| `customer_email` | 下订单客户的电子邮件地址。 这将在所有情况下填充，包括通过来宾结帐处理的订单 |
| `customer_group_id` | 与关联的外键 `customer_group` 表。 加入 `customer_group.customer_group_id` 确定与订单关联的客户组 |
| `customer_id` | `Foreign key` 与 `customer_entity` 表中。 加入 `customer_entity.entity_id` 以确定与订单关联的客户属性。 如果订单是通过来宾结帐下达的，则此字段将 `NULL` |
| `entity_id` (PK) | 表的唯一标识符，通常用于连接到Commerce实例中的其他表 |
| `increment_id` | 订单的唯一标识符，通常称为 `order_id` Magento。 的 `increment_id` 最常用于连接到外部源，例如 [!DNL Google Ecommerce] |
| `shipping_address_id` | 与关联的外键 `sales_order_address` 表。 加入 `sales_order_address.entity_id` 确定与订单关联的发运地址详细信息 |
| `status` | 订单状态。 可返回“complete”、“processing”、“cancelled”、“requanted”等值，以及在商务实例中实现的任何自定义状态。 在处理订单时可能发生更改 |
| `store_id` | `Foreign key` 与 `store` 表。 加入 `store`.`store_id` 确定与订单关联的商店视图 |

{style=&quot;table-layout:auto&quot;}

## 常用计算列

| **列名称** | **描述** |
|---|---|
| `Billing address city` | 按订单计费城市。 通过连接计算 `sales_order`.`billing_address_id` to `sales_order_address`.`entity_id` 并返回 `city` 字段 |
| `Billing address country` | 订单的帐单国家/地区代码。 通过连接计算 `sales_order`.`billing_address_id` to `sales_order_address`.`entity_id` 并返回 `country_id` |
| `Billing address region` | 订单的账单区域（通常为州或省）。 通过连接计算 `sales_order`.`billing_address_id` to `sales_order_address`.`entity_id` 并返回 `region` 字段 |
| `Customer's first order date` | 此客户下单的第一个订单的时间戳。 通常被视为客户的“收购日期”。 通过返回最小值计算 `sales_order`.`created_at` 每个独特客户的价值 |
| `Customer's first order's billing region` | 下订单的客户的客户的客户获取开单区域。 通过返回 `Billing address region` 与客户的首笔订单关联 |
| `Customer's first order's coupon_code` | 下达此订单的客户的客户获取优惠券代码。 通过返回 `coupon_code` 与客户的首笔订单关联 |
| `Customer's group code` | 下达此订单的客户的组名称。 通过连接计算 `sales_order`.`customer_group_id` to `customer_group`.`customer_group_id` 并返回 `customer_group_code` 字段 |
| `Customer's lifetime number of coupons` | 应用于此客户下达的所有订单的优惠券总数量。 通过计算 `coupon_code` 不是 `NULL` 每个独特客户 |
| `Customer's lifetime number of orders` | 此客户下达的订单总数。 通过计算 `sales_order` 每个独特客户的表 |
| `Customer's lifetime revenue` | 此客户下达的所有订单的总收入。 通过总计 `base_grand_total` 每个独特客户的所有订单的字段 |
| `Customer's order number` | 此客户订单的顺序排名。 计算方式：确定客户下的所有订单，然后按 `created_at` 时间戳，并为每个订单分配递增的整数值。 例如，客户的首次订购返回 `Customer's order number` 1;他们的第二顺序返回 `Customer's order number` 2;等等 |
| `Customer's order number (previous-current)` | 客户上一订单的排名与此订单的排名连接，并以 `-` 字符。 通过连接(&quot;`Customer's order number` - 1&quot;)`-`&quot;后跟&quot;`Customer's order number`&quot; 例如，对于与客户第二次购买关联的订单，此列将返回值“ `1-2`. 在表示两个订单事件之间的时间（即“订单之间的时间”图表中）时最常用的方法 |
| `Is customer's last order?` | 确定订单是否与客户的上次订单或最近订单相对应。 通过比较 `Customer's order number` 值 `Customer's lifetime number of orders`. 当给定顺序的这两个字段相等时，此列将返回“是”；否则，返回“否” |
| `Number of items in order` | 订单中包含的物料的总数量。 通过连接计算 `sales_order`.`entity_id` to `sales_order_item`.`order_id` 并求和 `sales_order_item`.`qty_ordered` 字段 |
| `Seconds between customer's first order date and this order` | 此订单与客户首次订购之间经过的时间。 通过减法计算 `Customer's first order date` 从 `created_at` 对于每个订单，以整数秒的形式返回 |
| `Seconds since previous order` | 从此订单到客户紧接先前订单之间经过的时间。 通过减去 `created_at` 从 `created_at` ，以整数秒数返回。 例如，对于对应于客户第三顺序的订单记录，此列返回客户第二顺序与第三顺序之间的秒数。 对于客户的首次订购，此字段将返回 `NULL` |
| `Shipping address city` | 订单的送货城市。 通过连接计算 `sales_order`.`shipping_address_id` to `sales_order_address`.`entity_id` 并返回 `city` 字段 |
| `Shipping address country` | 订单的装运国家/地区代码。 通过连接计算 `sales_order`.`Shipping_address_id` to `sales_order_address`.`entity_id` 并返回 `country_id` |
| `Shipping address region` | 订单的装运区域（通常为州或省）。 通过连接计算 `sales_order`.`shipping_address_id` to `sales_order_address`.`entity_id` 并返回 `region` 字段 |
| `Store name` | 与此订单关联的商务商店的名称。 通过连接计算 `sales_order`.`store_id` to `store`.`store_id` 并返回 `name` 字段 |

## 常用量度

| **量度名称** | **描述** | **建筑** |
|---|---|---|
| `Avg order value` | 每个订单的平均收入，其中收入定义为 `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | 客户(n-1)订单与第n次订单之间的平均时间，适用于所有客户和订单 | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | 所有订单（GMV被定义为小计）在应用所有税和折扣前的商品总价值总和 | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | 客户(n-1)订单与第n次订单之间的中间时间（适用于所有客户和订单） | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | 下达订单总数 | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | 所有订单的收入总和，其中收入被定义为客户支付的最终价格，并且已应用所有税、折扣、发运等 | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | 所有订单的发运金额总和 | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | 应用于所有订单的税金总和 | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | 在给定报表时间间隔内下订单的独特客户数。 例如，如果报表的间隔为每周，则在给定周内至少下达一次订单的每位客户将被计数一次，而不管他们在该周下达了多少次订单 | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` 连接路径

`customer_entity`

* 加入 `customer_entity` 表格，以创建与下订单的客户关联的新客户级别列。
   * 路径： `sales_order.customer_id` （多个）=> `customer_entity.entity_id` (1)

`customer_group`

* 加入 `customer_group` 表格，以创建新列，以返回下订单的客户的客户组名称。
   * 路径： `sales_order.customer_group_id` （多个）=> `customer_group.customer_group_id` (1)

`sales_order_address`

* 加入 `sales_order_address` 表格以创建新列，返回与订单关联的开单和发运位置。 根据是否需要计费或送货详细信息，可以使用两个连接路径。
   * 路径：
      * 装运： `sales_order.shipping_address_id`（多个）=> `sales_order_address.entity_id` (1)
      * 账单： `sales_order.billing_address_id`（多个）=> `sales_order_address.entity_id` (1)

`store`

* 加入 `store` 表格以创建新列，这些列返回与订单关联的商务商店相关的详细信息。
   * 路径： `sales_order.store_id` （多个）=> `store.store_id` (1)
