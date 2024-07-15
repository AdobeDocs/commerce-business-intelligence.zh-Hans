---
title: 常用Commerce表
description: 了解 [!DNL Commerce Intelligence] 客户使用的一些更常见的表。
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# 常用Commerce表

首次将[!DNL Adobe Commerce]实例连接到[[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md)时，[!DNL Commerce Intelligence]会自动从某些商务表（通常为4-6个表）复制数据以配置仪表板和报表的初始集。 虽然这是一个很好的起点，但大多数存储实例会生成数十个（如果不是数百个）其他表，这些表可以提供对业务性能的重要洞察。

以下是[!DNL Commerce Intelligence]客户使用的一些更常见表的列表。 将Commerce实例[连接到Commerce Intelligence](../../data-analyst/importing-data/integrations/magento.md)后，您可以使用[Data Warehouse管理器](../../data-analyst/data-warehouse-mgr/tour-dwm.md)来跟踪相关数据字段。

| 表名 | 描述 |
|---|---|
| `catalog_category_entity` | `catalog_category_entity`表中的每一行都描述了一个特定类别。 使用关联的`catalog_category_entity_varchar`表和`catalog_category_product`映射表，您可以获取每个产品的类别信息。 |
| `catalog_category_product` | `catalog_category_product`表中的每一行都列出了产品和类别的组合。 因此，给定产品可以不同类别多次存在于此表中，并且给定类别可以多次存在于此表中，这些类别与不同的产品相关联。 此表对`catalog_category_entity`表（包含类别级别详细信息）和`catalog_product_entity`表（包含产品级别详细信息）进行索引。 |
| `catalog_product_entity` | `catalog_product_entity`表中的每一行代表一个特定的产品。 其中包括在您的Commerce帐户及其SKU中创建该产品的时间。 |
| `customer_entity` | [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md)表中的每一行都表示您网站上的注册用户。 此表提供了客户级别的基本详细信息，如注册日期和电子邮件地址。 |
| `quote` | [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md)表中的每一行都表示在结帐过程中创建的购物车，无论该购物车最终是否转换为订单。 由于此表可能的大小问题，Adobe建议您在满足某些条件时定期删除记录，例如，如果有任何超过60天的未转换购物车。 |
| `quote_item` | [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md)表中的每一行都表示添加到购物车的项目，无论购物车最终是否转换为订单。 由于此表可能的大小问题，Adobe建议您在满足某些条件时定期删除记录，例如，如果有任何超过60天的未转换购物车。 |
| `sales_order` | [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md)表中的每一行都表示您网站上的订单。 此表包含订单级别的信息，如订单日期、下订单的客户、订单总额以及折扣和优惠券代码用途。 |
| `sales_order_address` | `sales_order_address`表中的每一行都包含特定订单的装运和帐单信息。 在`sales_order`表中，给定订单的`billing_address_id`和`shipping_address_id`引用了`sales_order_address`表上的特定行（由`entity_id`标识）。 |
| `sales_order_item` | [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md)表中的每一行都从特定顺序中标识一个特定项。 每一行都包含产品、购买数量和与给定项目关联的订单等详细信息。 |

{style="table-layout:auto"}

## 相关文档

[实体关系图](../data-warehouse-mgr/entity-rel-diag.md)
