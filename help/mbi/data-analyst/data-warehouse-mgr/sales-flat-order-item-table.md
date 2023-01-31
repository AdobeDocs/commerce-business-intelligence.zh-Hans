---
title: sales_order_item表
description: 了解如何使用sales_order_item表。
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
source-git-commit: c0892aa046c80f90561b4a178525ef9ed05b435a
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 0%

---

# `sales_order_item` 表

的 `sales_order_item` 表(`sales_flat_order_item` on [!DNL Magento] 1)包含订单中购买的所有产品的记录。 每行表示一个唯一 `sku` 包含在订单中。 为特定 `sku` 通常由 `qty_ordered` 字段。

## 产品类型

的 `sales_order_item` 捕获所有 [产品类型](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 已购买。 商务中的常见做法是提供可配置的产品，即可根据大小、颜色和其他产品属性进行自定义的产品。 尽管可配置产品有其自己的 `sku`，则它可以与多个简单产品相关，其中每个简单产品表示一个唯一的产品配置。 请参阅 [配置产品](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) 以了解更多信息。

例如，请考虑可配置的产品，如t恤。 客户签出时，会选择选项以更改颜色和大小。 如果客户选择 `blue`，以及 `small`，他们最终购买了一个简单的产品，例如 `t-shirt-blue-small` 与 `t-shirt`.

当可配置产品按顺序包含时， `sales_order_item` 表：一个 [简单](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku`，一个用于 [可配置](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) 父项。 这两张记录 `sales_order_item` 表可通过以下连接相互关联：

* （简单） `sales_order_item.parent_item_id` =>（可配置） `sales_order_item.item_id`

因此，可以在简单级别或可配置级别报告产品的销售情况。 默认情况下，所有标准 `order-item-level` 量度 [!DNL MBI] 配置为排除简单的产品，以及 *仅* 报告可配置版本。 这是通过 `Ordered products we count` 过滤器集，该过滤器在 `parent_item_id` is `NULL`.

## 常用列

| **列名称** | **描述** |
|----|----|
| `base_price` | 产品在售后单位的价格 [目录价格规则、分层折扣和特价](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 在应用任何税、送货或购物车折扣之前，以商店的基本货币表示 |
| `created_at` | 订单项的创建时间戳，通常以UTC存储在本地。 根据您在 [!DNL MBI]，此时间戳可能会转换为 [!DNL MBI] 与数据库时区不同 |
| `item_id` (PK) | 表的唯一标识符 |
| `name` | 订单项的文本名称 |
| `order_id` | `Foreign key` 与 `sales_order` 表。 加入 `sales_order.entity_id` 确定与订单项目关联的订单属性 |
| `parent_item_id` | `Foreign key` 将简单产品与其父捆绑包或可配置产品相关联。 加入 `sales_order_item.item_id` 以确定与简单产品关联的父产品属性。 对于父订单项（即捆绑或可配置的产品类型）， `parent_item_id` 将 `NULL` |
| `product_id` | `Foreign key` 与 `catalog_product_entity` 表。 加入 `catalog_product_entity.entity_id` 确定与订单项目关联的产品属性 |
| `product_type` | 已销售的产品类型。 潜在 [产品类型](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 包括：简单、可配置、分组、虚拟、捆绑和可下载 |
| `qty_ordered` | 在销售时购物车中特定订单项目的件数 |
| `sku` | 已购买订单项目的唯一标识符 |
| `store_id` | `Foreign key` 与 `store` 表。 加入 `store.store_id` 确定与订单项目关联的商务商店视图 |

{style=&quot;table-layout:auto&quot;}

## 常用计算列

| **列名称** | **描述** |
|---|---|
| `Customer's email` | 下订单客户的电子邮件地址。 通过连接计算 `sales_order_item.order_id` to `sales_order.entity_id` 并返回 `customer_email` 字段 |
| `Customer's lifetime number of orders` | 此客户下达的订单总数。 通过连接计算 `sales_order_item.order_id` to `sales_order.entity_id` 并返回 `Customer's lifetime number of orders` 字段 |
| `Customer's lifetime revenue` | 此客户下达的所有订单的总收入。 通过连接计算 `sales_order_item.order_id` to `sales_order.entity_id` 并返回 `Customer's lifetime revenue` 字段 |
| `Customer's order number` | 此客户订单的顺序排名。 通过连接计算 `sales_order_item.order_id` to `sales_order.entity_id` 并返回 `Customer's order number` 字段 |
| `Order item total value (quantity * price)` | 订单项目在售后的总价值 [目录价格规则、分层折扣和特价](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 在应用任何税、送货或购物车折扣之前应用。 计算方法是将 `qty_ordered` 按 `base_price` |
| `Order's coupon_code` | 应用于订单的优惠券。 通过连接计算 `sales_order_item.order_id` to `sales_order.entity_id` 并返回 `coupon_code` 字段 |
| `Order's increment_id` | 订单的唯一标识符。 通过连接计算 `sales_order_item.order_id` to `sales_order.entity_id` 并返回 `increment_id` 字段 |
| `Order's status` | 订单的状态。 通过连接计算 `sales_order_item.order_id` to `sales_order.entity_id` 并返回 `status` 字段 |
| `Store name` | 与订单项目关联的商务商店的名称。 通过连接计算 `sales_order_item.store_id` to `store.store_id` 并返回 `name` 字段 |

{style=&quot;table-layout:auto&quot;}

## 常用量度

| **量度名称** | **描述** | **建筑** |
|---|---|---|
| `Products ordered` | 销售时购物车中包含的产品总数 | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | 在应用目录价格规则、分层折扣和特殊定价之后，在应用任何税、运费或购物车折扣之前，购物车中包含的产品在销售时的总价值 | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style=&quot;table-layout:auto&quot;}

## `Foreign Key` 连接路径

`catalog_product_entity`

* 加入 `catalog_product_entity` 表格，以创建新列，返回与订单项目关联的产品属性。
   * 路径： `sales_order_item.product_id` （多个）=> `catalog_product_entity.entity_id` (1)

`sales_order`

* 加入 `sales_order` 表格，以创建与订单项目关联的新订单级别列。
   * 路径： `sales_order_item.order_id` （多个）=> `sales_order.entity_id` (1)

`sales_order_item`

* 加入 `sales_order_item` 创建新列，以将父可配置或捆绑SKU的详细信息与简单产品相关联。 请注意，您需要 [联系支持](../../guide-overview.md) 如果是在Data warehouse管理器中构建，则可帮助配置这些计算。
   * 路径： `sales_order_item.parent_item_id` （多个）=> `sales_order_item.item_id` (1)

`store`

* 加入 `store` 表格以创建新列，这些列返回与订单项目关联的商务商店相关的详细信息。
   * 路径： `sales_order_item.store_id` （多个）=> `store.store_id` (1)
