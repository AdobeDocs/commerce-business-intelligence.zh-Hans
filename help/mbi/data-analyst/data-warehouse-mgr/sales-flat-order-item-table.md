---
title: sales_order_item表
description: 了解如何使用sales_order_item表。
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---

# `sales_order_item` 表

此 `sales_order_item` 表(`sales_flat_order_item` ，其中包含订单中所购买的所有产品的记录。 每一行表示一个唯一的 `sku` 包含在订单中。 为特定购买的产品数量 `sku` 通常由 `qty_ordered` 字段。

## 产品类型

此 `sales_order_item` 捕获所有详细信息 [产品类型](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 购买过的。 中的常见做法 [!DNL Adobe Commerce] 是提供可配置产品，换句话说，就是根据尺寸、颜色和其他产品属性定制的产品。 尽管可配置产品有其自身的 `sku`，它可以与多个简单产品相关，其中每个简单产品代表一个独特的产品配置。 请参阅 [配置产品](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) 以了解更多信息。

例如，假定可配置产品为T恤。 客户结账时，会选择相应的选项来更改颜色和大小。 如果客户选择 `blue`，并且大小为 `small`，他们最终会购买简单的产品，例如 `t-shirt-blue-small` 与的父产品相关 `t-shirt`.

当可配置产品包含在订单中时， `sales_order_item` 表：一个用于 [简单](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku` 一个用于 [可配置](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) 父级。 这两个记录在 `sales_order_item` 表可以通过以下连接相互关联：

* （简单） `sales_order_item.parent_item_id` =>（可配置） `sales_order_item.item_id`

因此，可以在简单级别或可配置级别报告产品的销售情况。 默认情况下，所有标准 `order-item-level` 中的量度 [!DNL Commerce Intelligence] 配置为排除简单产品，并且 *仅限* 报告可配置版本。 这是通过以下方式实现的 `Ordered products we count` 筛选器集，用于筛选条件 `parent_item_id` 是 `NULL`.

## 公用列

| **列名称** | **描述** |
|----|----|
| `base_price` | 产品售出时的单件价格，售出后 [目录价格规则、分层折扣和特殊定价](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 在应用任何税费、运费或购物车折扣之前应用。 以存储的基本货币表示。 |
| `created_at` | 订单项的创建时间戳，以UTC本地存储。 取决于您在中的配置 [!DNL Commerce Intelligence]时，此时间戳可能会转换为中的报表时区 [!DNL Commerce Intelligence] 与数据库时区不同的时区。 |
| `item_id` (PK) | 表的唯一标识符。 |
| `name` | 订单项的文本名称。 |
| `order_id` | `Foreign key` 与关联 `sales_order` 表格。 加入 `sales_order.entity_id` 以确定与订单项目关联的订单属性。 |
| `parent_item_id` | `Foreign key` 将简单产品与其父捆绑包或可配置产品相关联。 加入 `sales_order_item.item_id` 确定与简单产品关联的父产品属性。 对于父订单项目（即捆绑包或可配置产品类型）， `parent_item_id` 是 `NULL`. |
| `product_id` | `Foreign key` 与关联 `catalog_product_entity` 表格。 加入 `catalog_product_entity.entity_id` 以确定与订单项目关联的产品属性。 |
| `product_type` | 已销售产品的类型。 潜在 [产品类型](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 包括：简单、可配置、已分组、虚拟、捆绑和可下载。 |
| `qty_ordered` | 销售时特定订单项目购物车中包含的单位数量。 |
| `sku` | 已购订单项目的唯一标识符。 |
| `store_id` | `Foreign key` 与关联 `store` 表格。 加入 `store.store_id` 以确定与订单项目关联的Commerce商店视图。 |

{style="table-layout:auto"}

## 通用计算列

| **列名称** | **描述** |
|---|---|
| `Customer's email` | 下订单客户的电子邮件地址。 通过加入计算 `sales_order_item.order_id` 到 `sales_order.entity_id` 并返回 `customer_email` 字段。 |
| `Customer's lifetime number of orders` | 此客户下达的订单总数。 通过加入计算 `sales_order_item.order_id` 到 `sales_order.entity_id` 并返回 `Customer's lifetime number of orders` 字段。 |
| `Customer's lifetime revenue` | 此客户下达的所有订单的总收入。 通过加入计算 `sales_order_item.order_id` 到 `sales_order.entity_id` 并返回 `Customer's lifetime revenue` 字段。 |
| `Customer's order number` | 此客户订单的连续订单排名。 通过加入计算 `sales_order_item.order_id` 到 `sales_order.entity_id` 并返回 `Customer's order number` 字段。 |
| `Order item total value (quantity * price)` | 订单项目在销售时的总值，晚于 [目录价格规则、分层折扣和特殊定价](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 在应用任何税费、运费或购物车折扣之前应用。 计算方法为： `qty_ordered` 按 `base_price`. |
| `Order's coupon_code` | 应用于订单的优惠券。 通过加入计算 `sales_order_item.order_id` 到 `sales_order.entity_id` 并返回 `coupon_code` 字段。 |
| `Order's increment_id` | 订单的唯一标识符。 通过加入计算 `sales_order_item.order_id` 到 `sales_order.entity_id` 并返回 `increment_id` 字段。 |
| `Order's status` | 订单的状态。 通过加入计算 `sales_order_item.order_id` 到 `sales_order.entity_id` 并返回 `status` 字段。 |
| `Store name` | 与订单项目关联的Commerce商店的名称。 通过加入计算 `sales_order_item.store_id` 到 `store.store_id` 并返回 `name` 字段。 |

{style="table-layout:auto"}

## 常用量度

| **量度名称** | **描述** | **建筑** |
|---|---|---|
| `Products ordered` | 销售时购物车中包含的产品总数 | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | 在应用目录价格规则、分层折扣和特殊定价之后以及应用任何税费、运费或购物车折扣之前，销售时购物车中包含的产品总值 | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` 联接路径

`catalog_product_entity`

* 加入 `catalog_product_entity` 表，用于创建返回与订单项目关联的产品属性的列。
   * 路径： `sales_order_item.product_id` （许多） => `catalog_product_entity.entity_id` （一）

`sales_order`

* 加入 `sales_order` 表，用于创建与订单项目关联的新订单层列。
   * 路径： `sales_order_item.order_id` （许多） => `sales_order.entity_id` （一）

`sales_order_item`

* 加入 `sales_order_item` 创建将父可配置或捆绑SKU的详细信息与简单产品关联的列。 [联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 以获取配置这些计算的帮助(如果在Data Warehouse管理器中生成)。
   * 路径： `sales_order_item.parent_item_id` （许多） => `sales_order_item.item_id` （一）

`store`

* 加入 `store` 创建列的表，这些列返回与订单项目关联的Commerce商店相关的详细信息。
   * 路径： `sales_order_item.store_id` （许多） => `store.store_id` （一）
