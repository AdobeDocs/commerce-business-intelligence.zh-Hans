---
title: sales_order_item表
description: 了解如何使用sales_order_item表。
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# `sales_order_item`表

`sales_order_item`表（ M1上的`sales_flat_order_item`）包含订单中购买的所有产品的记录。 每一行表示一个订单中包含的唯一`sku`。 为特定`sku`购买的单位数量通常由`qty_ordered`字段表示。

## 产品类型

`sales_order_item`捕获已购买的所有[产品类型](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html?lang=zh-Hans#product-types)的详细信息。 [!DNL Adobe Commerce]中的常见做法是提供可配置的产品，换句话说，就是根据大小、颜色和其他产品属性自定义的产品。 虽然可配置产品具有自己的`sku`，但它可以关联到多个简单产品，其中每个简单产品代表一个独特的产品配置。 有关详细信息，请参阅[配置产品](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/)。

例如，假定可配置产品为T恤。 客户结账时，会选择相应的选项来更改颜色和大小。 如果客户选择`blue`的颜色和`small`的大小，则他们最终会购买与`t-shirt-blue-small`的父产品相关的简单产品，例如`t-shirt`。

当可配置产品包含在订单中时，`sales_order_item`表中将生成两行：一行用于[simple](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html?lang=zh-Hans) `sku`，另一行用于[configurable](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html?lang=zh-Hans)父级。 `sales_order_item`表中的这两个记录可以通过以下连接相互关联：

* （简单） `sales_order_item.parent_item_id` => （可配置） `sales_order_item.item_id`

因此，可以在简单级别或可配置级别报告产品的销售情况。 默认情况下，`order-item-level`中的所有标准[!DNL Commerce Intelligence]量度都配置为排除简单产品，并且&#x200B;*仅*&#x200B;报告可配置的版本。 这是通过`Ordered products we count`筛选器集实现的，该筛选器集筛选条件`parent_item_id`为`NULL`。

## 公用列

| **列名称** | **描述** |
|----|----|
| `base_price` | 在应用[目录价格规则、分层折扣和特殊定价](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=zh-Hans)之后且未应用任何税费、运费或购物车折扣之前，销售时产品的单个单位的价格。 以存储的基本货币表示。 |
| `created_at` | 订单项的创建时间戳，以UTC本地存储。 根据[!DNL Commerce Intelligence]中的配置，此时间戳可能会转换为[!DNL Commerce Intelligence]中与数据库时区不同的报表时区。 |
| `item_id` (PK) | 表的唯一标识符。 |
| `name` | 订单项的文本名称。 |
| `order_id` | 与`Foreign key`表关联的`sales_order`。 加入`sales_order.entity_id`以确定与订单项关联的订单属性。 |
| `parent_item_id` | 将简单产品与其父捆绑包或可配置产品相关联的`Foreign key`。 加入`sales_order_item.item_id`以确定与简单产品关联的父产品属性。 对于父订单项（即捆绑包或可配置产品类型），`parent_item_id`为`NULL`。 |
| `product_id` | 与`Foreign key`表关联的`catalog_product_entity`。 加入`catalog_product_entity.entity_id`以确定与订单项关联的产品属性。 |
| `product_type` | 已销售产品的类型。 潜在的[产品类型](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html?lang=zh-Hans#product-types)包括：简单、可配置、已分组、虚拟、捆绑和可下载。 |
| `qty_ordered` | 销售时特定订单项目购物车中包含的单位数量。 |
| `sku` | 已购订单项目的唯一标识符。 |
| `store_id` | 与`Foreign key`表关联的`store`。 加入`store.store_id`以确定与订单项关联的Commerce商店视图。 |

{style="table-layout:auto"}

## 通用计算列

| **列名称** | **描述** |
|---|---|
| `Customer's email` | 下订单客户的电子邮件地址。 通过将`sales_order_item.order_id`加入`sales_order.entity_id`并返回`customer_email`字段进行计算。 |
| `Customer's lifetime number of orders` | 此客户下达的订单总数。 通过将`sales_order_item.order_id`加入`sales_order.entity_id`并返回`Customer's lifetime number of orders`字段进行计算。 |
| `Customer's lifetime revenue` | 此客户下达的所有订单的总收入。 通过将`sales_order_item.order_id`加入`sales_order.entity_id`并返回`Customer's lifetime revenue`字段进行计算。 |
| `Customer's order number` | 此客户订单的连续订单排名。 通过将`sales_order_item.order_id`加入`sales_order.entity_id`并返回`Customer's order number`字段进行计算。 |
| `Order item total value (quantity * price)` | 在应用了[目录价格规则、分层折扣和特殊定价](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=zh-Hans)之后且未应用任何税、运费或购物车折扣之前，订单项目在销售时的总值。 通过`qty_ordered`乘以`base_price`计算。 |
| `Order's coupon_code` | 应用于订单的优惠券。 通过将`sales_order_item.order_id`加入`sales_order.entity_id`并返回`coupon_code`字段进行计算。 |
| `Order's increment_id` | 订单的唯一标识符。 通过将`sales_order_item.order_id`加入`sales_order.entity_id`并返回`increment_id`字段进行计算。 |
| `Order's status` | 订单的状态。 通过将`sales_order_item.order_id`加入`sales_order.entity_id`并返回`status`字段进行计算。 |
| `Store name` | 与订单项目关联的Commerce商店的名称。 通过将`sales_order_item.store_id`加入`store.store_id`并返回`name`字段进行计算。 |

{style="table-layout:auto"}

## 常用量度

| **量度名称** | **描述** | **构造** |
|---|---|---|
| `Products ordered` | 销售时购物车中包含的产品总数 | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | 在应用目录价格规则、分层折扣和特殊定价之后以及应用任何税费、运费或购物车折扣之前，销售时购物车中包含的产品总值 | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key`加入路径

`catalog_product_entity`

* 加入`catalog_product_entity`表以创建返回与订单项关联的产品属性的列。
   * 路径： `sales_order_item.product_id` （多个） => `catalog_product_entity.entity_id` （一个）

`sales_order`

* 加入`sales_order`表以创建与订单项关联的新订单级列。
   * 路径： `sales_order_item.order_id` （多个） => `sales_order.entity_id` （一个）

`sales_order_item`

* 加入`sales_order_item`以创建将父可配置或捆绑SKU的详细信息与简单产品关联的列。 在Data Warehouse管理器中构建时，[联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hans)以获得配置这些计算的帮助。
   * 路径： `sales_order_item.parent_item_id` （多个） => `sales_order_item.item_id` （一个）

`store`

* 加入`store`表以创建列，这些列返回与订单项关联的Commerce存储相关的详细信息。
   * 路径： `sales_order_item.store_id` （多个） => `store.store_id` （一个）
