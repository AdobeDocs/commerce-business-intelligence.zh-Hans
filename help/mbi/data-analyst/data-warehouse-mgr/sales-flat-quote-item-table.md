---
title: quote_item表
description: 了解如何使用quote_item表。
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 0%

---

# quote_item表

的 `quote_item` 表(`sales_flat_quote_item` on [!DNL Magento] 1)包含有关添加到购物车的每个项目的记录，无论该购物车是被放弃还是被转换为购买。 每行表示一个购物车项目。 由于此表的潜在大小，我们建议您在满足某些标准（例如，如果有任何未转换的购物车超过60天）时定期删除记录。

>[!NOTE]
>
>只有在不从 `quote` 和 `quote_item` 表。 如果删除记录，您将只能看到尚未从数据库中删除的购物车。

## 常用本机列

| **列名称** | **描述** |
|---|---|
| `base_price` | 在将产品添加到购物车时(在 [目录价格规则、分层折扣和特价](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 在应用任何税、送货或购物车折扣之前，以商店的基本货币表示 |
| `created_at` | 购物车项目的创建时间戳，通常以UTC存储在本地。 根据您在 [!DNL MBI]，此时间戳可能会转换为 [!DNL MBI] 与数据库时区不同 |
| `item_id` (PK) | 表的唯一标识符 |
| `name` | 订单项的文本名称 |
| `parent_item_id` | `Foreign key` 将简单产品与其父捆绑包或可配置产品相关联。 加入 `quote_item.item_id` 以确定与简单产品关联的父产品属性。 对于父购物车项目（即捆绑或可配置产品类型）， `parent_item_id` 将 `NULL` |
| `product_id` | `Foreign key` 与 `catalog_product_entity` 表。 加入 `catalog_product_entity.entity_id` 确定与订单项目关联的产品属性 |
| `product_type` | 添加到购物车的产品类型。 潜在 [产品类型](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 包括：简单、可配置、分组、虚拟、捆绑和可下载 |
| `qty` | 购物车中特定购物车项目包含的件数 |
| `quote_id` | `Foreign key` 与 `quote` 表。 加入 `quote.entity_id` 确定与购物车项目关联的购物车属性 |
| `sku` | 购物车项目的唯一标识符 |
| `store_id` | 与关联的外键 `store` 表。 加入 `store.store_id` 确定与购物车项目关联的商店视图 |

{style=&quot;table-layout:auto&quot;}

## 常用计算列

| **列名称** | **描述** |
|---|---|
| `Cart creation date` | 与购物车创建日期关联的时间戳。 通过连接计算 `quote_item.quote_id` to `quote.entity_id` 并返回 `created_at` timestamp |
| `Cart is active? (1/0)` | 布尔字段，用于在客户创建购物车且尚未转换为订单时返回“1”。 对于已转换的购物车或通过管理员创建的购物车，返回“0”。 通过连接计算 `quote_item.quote_id` to `quote.entity_id` 并返回 `is_active` 字段 |
| `Cart item total value (qty * base_price)` | 在将物料添加到购物车时，在 [目录价格规则、分层折扣和特价](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 在应用任何税、送货或购物车折扣之前应用。 计算方法是将 `qty` 按 `base_price` |
| `Seconds since cart creation` | 购物车创建日期与现在之间经过的时间。 通过连接计算 `quote_item.quote_id` to `quote.entity_id` 并返回 `Seconds since cart creation` 字段 |
| `Store name` | 与订单项目关联的商务商店的名称。 通过连接计算 `sales_order_item.store_id` to `store.store_id` 并返回 `name` 字段 |

{style=&quot;table-layout:auto&quot;}

## 常用量度

| **量度名称** | **描述** | **建筑** |
|---|---|---|
| `Number of abandoned cart items` | 添加到满足特定“放弃”条件的购物车的项目总数 | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>过滤器：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x，其中“x”对应于自购物车创建后经过的时间（以秒为单位），在创建购物车之后，购物车将被视为放弃 |
| `Abandoned cart item value` | 与满足特定“放弃”条件的购物车关联的总收入 | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>过滤器：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x，其中“x”对应于自购物车创建后经过的时间（以秒为单位），在创建购物车之后，购物车将被视为放弃 |

{style=&quot;table-layout:auto&quot;}

## 外键连接路径

`catalog_product_entity`

* 加入 `catalog_product_entity` 表格以创建新列，返回与购物车项目关联的产品属性。
   * 路径： `quote_item.product_id` （多个）=> `catalog_product_entity.entity_id` (1)

`quote`

* 加入 `quote` 用于创建与购物车项目关联的新购物车级别列的表。
   * 路径： `quote_item.quote_id` （多个）=> `quote.entity_id` (1)

`quote_item`

* 加入 `quote_item` 创建新列，以将父可配置或捆绑SKU的详细信息与简单产品相关联。 请注意，您需要 [联系支持](../../guide-overview.md) 如果是在Data warehouse管理器中构建，则可帮助配置这些计算。
   * 路径： `quote_item.parent_item_id` （多个）=> `quote_item.item_id` (1)

`store`

* 加入 `store` 用于创建新列，以返回与购物车项目关联的商店相关的详细信息。
   * 路径： `quote_item.store_id` （多个）=> `store.store_id` (1)
