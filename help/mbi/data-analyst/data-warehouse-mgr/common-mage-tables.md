---
title: 常见Commerce表
description: 了解一些更常见的表 [!DNL Commerce Intelligence] 客户使用。
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 常见Commerce表

当您首次连接 [!DNL Adobe Commerce] 实例到 [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md)， [!DNL Commerce Intelligence] 自动复制某些commerce表（通常为4-6个表）中的数据以配置初始功能板和报表集。 虽然这是一个很好的起点，但大多数存储实例会生成数十个（如果不是数百个）其他表，这些表可以提供对业务性能的重要洞察。

以下是一些更常见的表的列表， [!DNL Commerce Intelligence] 客户使用。 在您之后 [将您的Commerce实例连接到Commerce Intelligence](../../data-analyst/importing-data/integrations/magento.md)，您可以使用 [Data Warehouse管理器](../../data-analyst/data-warehouse-mgr/tour-dwm.md) 以跟踪相关数据字段。

| 表名 | 描述 |
|---|---|
| `catalog_category_entity` | 中的每一行 `catalog_category_entity` 该表描述了特定类别。 与关联的 `catalog_category_entity_varchar` 表格和 `catalog_category_product` 映射表，获取每个产品的类别信息。 |
| `catalog_category_product` | 中的每一行 `catalog_category_product` 该表列出了产品和类别的组合。 因此，给定产品可以不同类别多次存在于此表中，并且给定类别可以多次存在于此表中，这些类别与不同的产品相关联。 此表对 `catalog_category_entity` 表（保存类别层详细信息）和 `catalog_product_entity` 表（保存产品级详细信息）。 |
| `catalog_product_entity` | 中的每一行 `catalog_product_entity` 表表示特定产品。 其中包括在您的商务帐户及其SKU中创建该产品的时间。 |
| `customer_entity` | 中的每一行 [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) 表表示您网站上的注册用户。 此表提供了客户级别的基本详细信息，如注册日期和电子邮件地址。 |
| `quote` | 中的每一行 [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) 表表示在结帐过程中创建的购物车，无论该购物车最终是否转换为订单。 由于此表可能的大小问题，Adobe建议您在满足某些条件时定期删除记录，例如，如果有任何超过60天的未转换购物车。 |
| `quote_item` | 中的每一行 [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) 表表示添加到购物车的项目，无论购物车最终是否转换为订单。 由于此表可能的大小问题，Adobe建议您在满足某些条件时定期删除记录，例如，如果有任何超过60天的未转换购物车。 |
| `sales_order` | 中的每一行 [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) 表表示您网站上的订单。 此表包含订单级别的信息，如订单日期、下订单的客户、订单总额以及折扣和优惠券代码用途。 |
| `sales_order_address` | 上的每一行 `sales_order_address` 此表包含特定订单的发运和开单信息。 在 `sales_order` 表， `billing_address_id` 和 `shipping_address_id` 对于给定顺序，请参阅特定行(标识为 `entity_id`) `sales_order_address` 表格。 |
| `sales_order_item` | 中的每一行 [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) 表标识特定订单中的特定项目。 每一行都包含产品、购买数量和与给定项目关联的订单等详细信息。 |

{style="table-layout:auto"}

## 相关文档

[实体关系图](../data-warehouse-mgr/entity-rel-diag.md)
