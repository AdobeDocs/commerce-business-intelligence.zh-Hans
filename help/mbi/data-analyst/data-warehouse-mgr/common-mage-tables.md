---
title: 通用商务表
description: 了解一些比较常见的表 [!DNL MBI] 客户利用。
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# 通用商务表

首次将商务实例连接到 [[!DNL MBI]](../importing-data/integrations/magento.md), [!DNL MBI] 自动从某些商务表（通常为4-6个表）复制数据，以配置初始的功能板和报表集。 尽管这提供了一个很好的起点，但大多数存储实例会生成数十个（甚至数百个）附加表，这些表可以提供对业务性能的关键分析。

下面是一些比较常见的表的列表， [!DNL MBI] 客户利用。 在 [将您的商务实例连接到MBI](../../data-analyst/importing-data/integrations/magento.md)，则可以使用 [data warehouse管理器](../../data-analyst/data-warehouse-mgr/tour-dwm.md) 以跟踪相关数据字段。

| 表名称 | 描述 |
|---|---|
| `catalog_category_entity` | 中的每一行 `catalog_category_entity` 表描述了特定类别。 与 `catalog_category_entity_varchar` 表格和 `catalog_category_product` 映射表时，您可以获取每个产品的类别信息。 |
| `catalog_category_product` | 中的每一行 `catalog_category_product` 表格列出了产品和类别的组合。 因此，给定产品可以在此表中多次存在，但具有不同的类别，并且给定的类别可以在此表中多次存在，并且与不同产品关联。 此表对 `catalog_category_entity` 表（包含类别级别的详细信息）和 `catalog_product_entity` 表（包含产品级别的详细信息）。 |
| `catalog_product_entity` | 中的每一行 `catalog_product_entity` 表代表特定产品。 这包括在您的商务帐户及其SKU中创建该产品的时间。 |
| `customer_entity` | 中的每一行 [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) 表表示您网站上的注册用户。 此表中提供了客户级别的基本详细信息（如其注册日期和电子邮件地址）。 |
| `quote` | 中的每一行 [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) 表表示在结帐过程中创建的购物车，无论该购物车最终是否转换为订单。 由于此表的潜在大小，我们建议您在满足某些标准（例如，如果有任何未转换的购物车超过60天）时定期删除记录。 |
| `quote_item` | 中的每一行 [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) 表表示添加到购物车的项目，无论购物车最终是否转换为订单。 由于此表的潜在大小，我们建议您在满足某些标准（例如，如果有任何未转换的购物车超过60天）时定期删除记录。 |
| `sales_order` | 中的每一行 [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) 表格表示网站上的订单。 此表包含订单级别的信息，如订单日期、下订单的客户、订单总数、折扣和优惠券代码使用情况。 |
| `sales_order_address` | 在 `sales_order_address` 表包含特定订单的送货和帐单信息。 在 `sales_order` 表格， `billing_address_id` 和 `shipping_address_id` 对于给定订单，引用特定行(由 `entity_id`) `sales_order_address` 表。 |
| `sales_order_item` | 中的每一行 [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) 表从特定顺序中标识特定项目。 每行都包含产品、已购买数量以及与给定项目关联的订单等详细信息。 |

{style=&quot;table-layout:auto&quot;}

## 相关文档

[实体关系图](../data-warehouse-mgr/entity-rel-diag.md)
