---
title: sales_order表
description: 了解如何使用sales_order表。
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 0%

---

# `sales_order`表

`sales_order`表（`sales_flat_order`位于M1）是捕获每个订单的位置。 通常，每行表示一个唯一顺序，不过Commerce的一些自定义实施会导致将顺序拆分为单独的行。

此表包含所有客户订单，无论该订单是通过来宾结账处理的。 如果您的商店接受访客签出，则可以找到有关此[用例](../data-warehouse-mgr/guest-orders.md)的更多信息。

## 公用列

| **列名称** | **描述** |
|---|---|
| `base_currency_code` | 在`base_*`字段（即`base_grand_total`、`base_subtotal`等）中捕获的所有值的货币。 这通常反映了Commerce商店的默认货币 |
| `base_discount_amount` | 应用于订单的折扣值 |
| `base_grand_total` | 应用所有税费、运费和折扣后，客户在订单上支付的最终价格。 虽然精确计算可自定义，但通常`base_grand_total`的计算方式为`base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | 订单中所有项目的商品总值。 不包含税、运费、折扣等 |
| `base_shipping_amount` | 应用于订单的装运值 |
| `base_tax_amount` | 应用于订单的税值 |
| `billing_address_id` | 与`sales_order_address`表关联的`Foreign key`。 加入`sales_order_address.entity_id`以确定与订单关联的帐单地址详细信息 |
| `coupon_code` | 订单申请的优惠券。 如果未应用优惠券，则此字段为`NULL` |
| `created_at` | 订单的创建时间戳，以UTC本地存储。 根据[!DNL Commerce Intelligence]中的配置，此时间戳可能会转换为[!DNL Commerce Intelligence]中与数据库时区不同的报表时区 |
| `customer_email` | 下订单客户的电子邮件地址。 在所有情况下均会填充该变量，包括通过访客结账处理的订单 |
| `customer_group_id` | 与`customer_group`表关联的外键。 加入`customer_group.customer_group_id`以确定与订单关联的客户组 |
| `customer_id` | 与`customer_entity`表关联的`Foreign key`（如果已注册客户）。 加入`customer_entity.entity_id`以确定与订单关联的客户属性。 如果订单是通过访客结帐发出的，则此字段为`NULL` |
| `entity_id` (PK) | 表的唯一标识符，通常用于联接Commerce实例中的其他表 |
| `increment_id` | 订单的唯一标识符，在Adobe Commerce中通常称为`order_id`。 `increment_id`最常用于连接外部源，如[!DNL Google Ecommerce] |
| `shipping_address_id` | 与`sales_order_address`表关联的外键。 加入`sales_order_address.entity_id`以确定与订单关联的配送地址详细信息 |
| `status` | 订单状态。 可以返回“完成”、“正在处理”、“已取消”、“已退款”等值，以及在Commerce实例上实现的任何自定义状态。 处理订单时可能会发生更改 |
| `store_id` | 与`store`表关联的`Foreign key`。 加入`store`。`store_id`以确定哪个Commerce商店视图与订单关联 |

{style="table-layout:auto"}

## 通用计算列

| **列名称** | **描述** |
|---|---|
| `Billing address city` | 订单的计费城市。 通过加入`sales_order`进行计算。`billing_address_id`到`sales_order_address`。`entity_id`并返回`city`字段 |
| `Billing address country` | 订单的计费国家/地区代码。 通过加入`sales_order`进行计算。`billing_address_id`到`sales_order_address`。`entity_id`并返回`country_id` |
| `Billing address region` | 订单的计费区域（通常为州或省）。 通过加入`sales_order`进行计算。`billing_address_id`到`sales_order_address`。`entity_id`并返回`region`字段 |
| `Customer's first order date` | 此客户下第一个订单的时间戳。 通常被认为是客户的“收购日期”。 通过返回最小值`sales_order`进行计算。每个独特客户的`created_at`值 |
| `Customer's first order's billing region` | 下订单的客户的客户获取开单区域。 通过返回与客户第一张订单关联的`Billing address region`进行计算 |
| `Customer's first order's coupon_code` | 下此订单的客户的客户获取优惠券代码。 通过返回与客户第一张订单关联的`coupon_code`进行计算 |
| `Customer's group code` | 下此订单的客户的组名称。 通过加入`sales_order`进行计算。`customer_group_id`到`customer_group`。`customer_group_id`并返回`customer_group_code`字段 |
| `Customer's lifetime number of coupons` | 应用于此客户下达的所有订单的总优惠券数量。 通过计算每个唯一客户的`coupon_code`不是`NULL`的订单数进行计算 |
| `Customer's lifetime number of orders` | 此客户下达的订单总数。 通过计算`sales_order`表中每个独特客户的行数来计算 |
| `Customer's lifetime revenue` | 此客户下达的所有订单的总收入。 计算方式为汇总每个独特客户的所有订单的`base_grand_total`字段 |
| `Customer's order number` | 此客户订单的连续订单排名。 通过识别客户下达的所有订单、按`created_at`时间戳对订单进行升序排序并为每个订单分配递增的整数值进行计算。 例如，客户的第一张订单返回`Customer's order number`为1，客户的第二张订单返回`Customer's order number`为2，依此类推。 |
| `Customer's order number (previous-current)` | 客户上一订单的排名与此订单的排名关联，以`-`字符分隔。 通过将(“`Customer's order number` - 1”)与“`-`”后接“`Customer's order number`”连接进行计算。 例如，对于与客户第二次购买关联的订单，此列返回值`1-2`。 通常用于表示两个订单事件之间的时间（即，在“订单之间的时间”图表中） |
| `Is customer's last order?` | 确定订单是对应于客户的上次订单还是最近订单。 通过将`Customer's order number`值与`Customer's lifetime number of orders`进行比较进行计算。 当这两个字段对于给定顺序相等时，此列返回`Yes`；否则，它返回`No` |
| `Number of items in order` | 订单中包含的物料总数。 通过加入`sales_order`进行计算。`entity_id`到`sales_order_item`。`order_id`并汇总`sales_order_item`。`qty_ordered`字段 |
| `Seconds between customer's first order date and this order` | 此订单与客户首次订单之间的间隔时间。 通过从每个订单的`created_at`中减去`Customer's first order date`计算，以整数秒数返回 |
| `Seconds since previous order` | 此订单与客户之前订单之间的间隔时间。 通过将此顺序的`created_at`减去前一顺序的`created_at`计算，返回整数秒数。 例如，对于与客户第三张订单对应的订单记录，此列返回客户第二张订单与第三张订单之间的秒数。 对于客户的第一个订单，此字段返回`NULL` |
| `Shipping address city` | 订单的配送城市。 通过加入`sales_order`进行计算。`shipping_address_id`到`sales_order_address`。`entity_id`并返回`city`字段 |
| `Shipping address country` | 订单的装运国家/地区代码。 通过加入`sales_order`进行计算。`Shipping_address_id`到`sales_order_address`。`entity_id`并返回`country_id` |
| `Shipping address region` | 订单的配送区域（通常为州或省）。 通过加入`sales_order`进行计算。`shipping_address_id`到`sales_order_address`。`entity_id`并返回`region`字段 |
| `Store name` | 与此订单关联的Commerce商店的名称。 通过加入`sales_order`进行计算。`store_id`到`store`。`store_id`并返回`name`字段 |

## 常用量度

| **量度名称** | **描述** | **构造** |
|---|---|---|
| `Avg order value` | 每个订单的平均收入，其中收入定义为`base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | 客户的(n-1)订单与所有客户和订单的n订单之间的平均时间 | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | 在应用所有税和折扣之前，所有订单的商品总价值（其中GMV定义为小计） | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | 客户的(n-1)订单与所有客户和订单的n次订单之间的中间时间 | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | 订购总数 | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | 所有订单的收入总和，其中收入定义为客户支付的最终价格，扣除所有税费、折扣、配送等在内，均适用 | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | 所有订单的装运金额总和 | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | 应用于所有订单的税的总和 | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | 在给定报告时间间隔内下订单的唯一客户数。 例如，如果报表的间隔为每周，则在给定周内至少下过一次订单的每个客户都将被计算一次，而不管他们在该周内下了多少订单 | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key`加入路径

`customer_entity`

* 加入`customer_entity`表以创建与下订单的客户关联的新客户级列。
   * 路径： `sales_order.customer_id` （多个） => `customer_entity.entity_id` （一个）

`customer_group`

* 加入`customer_group`表以创建返回下订单客户的客户组名称的列。
   * 路径： `sales_order.customer_group_id` （多个） => `customer_group.customer_group_id` （一个）

`sales_order_address`

* 加入`sales_order_address`表以创建返回与订单关联的帐单和装运位置的列。 根据是否需要帐单或送货详细信息，可以使用两个连接路径。
   * 路径：
      * 送货： `sales_order.shipping_address_id`（多个）=> `sales_order_address.entity_id`（一个）
      * 帐单： `sales_order.billing_address_id`（多个）=> `sales_order_address.entity_id`（一个）

`store`

* 加入`store`表以创建列，这些列返回与订单关联的Commerce存储相关的详细信息。
   * 路径： `sales_order.store_id` （多个） => `store.store_id` （一个）
