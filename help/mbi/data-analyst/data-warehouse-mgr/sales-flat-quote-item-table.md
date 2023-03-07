---
title: quote_item表
description: 了解如何使用quote_item表。
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---

# quote_item表

此 `quote_item` 表(`sales_flat_quote_item` (M1) 1)包含添加到购物车的每个项目的记录，无论购物车是放弃还是转换为购买。 每一行表示一个购物车项目。 由于此表可能很大，因此Adobe建议您在满足某些条件时定期删除记录，例如，如果有任何超过60天的未转换购物车。

>[!NOTE]
>
>只有当您不从以下位置删除记录时，才可能分析历史、放弃的购物车 `quote` 和 `quote_item` 表格。 如果确实删除了记录，则只能查看尚未从数据库中删除的购物车。

## 通用本机列

| **列名称** | **描述** |
|---|---|
| `base_price` | 将产品添加到购物车时，产品在之后的单个单位的价格 [目录价格规则、分层折扣和特殊定价](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) ，且未应用任何税费、运费或购物车折扣。 以存储的基本货币表示。 |
| `created_at` | 购物车项目的创建时间戳，以UTC本地存储。 取决于您在中的配置 [!DNL MBI]时，此时间戳可能会转换为中的报表时区 [!DNL MBI] 与您的数据库时区不同 |
| `item_id` (PK) | 表的唯一标识符 |
| `name` | 订单项的文本名称 |
| `parent_item_id` | `Foreign key` 将简单产品与其父捆绑包或可配置产品相关联。 加入 `quote_item.item_id` 以确定与简单产品相关的父产品属性。 对于父购物车项目（即捆绑包或可配置产品类型）， `parent_item_id` 是 `NULL` |
| `product_id` | `Foreign key` 与 `catalog_product_entity` 表格。 加入 `catalog_product_entity.entity_id` 确定与订单项目关联的产品属性 |
| `product_type` | 添加到购物车的产品类型。 潜在 [产品类型](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 包括：简单、可配置、分组、虚拟、捆绑和可下载 |
| `qty` | 特定购物车项目的购物车中包含的单位数量 |
| `quote_id` | `Foreign key` 与 `quote` 表格。 加入 `quote.entity_id` 确定与购物车项目关联的购物车属性 |
| `sku` | 购物车项目的唯一标识符 |
| `store_id` | 与关联的外键 `store` 表格。 加入 `store.store_id` 以确定哪个Commerce商店视图与购物车项目关联 |

{style="table-layout:auto"}

## 通用计算列

| **列名称** | **描述** |
|---|---|
| `Cart creation date` | 与购物车创建日期关联的时间戳。 通过加入计算 `quote_item.quote_id` 到 `quote.entity_id` 并返回 `created_at` 时间戳 |
| `Cart is active? (1/0)` | 布尔字段，如果购物车由客户创建且尚未转换为订单，则返回“1”。 对于已转换的购物车或通过管理员创建的购物车，返回“0”。 通过加入计算 `quote_item.quote_id` 到 `quote.entity_id` 并返回 `is_active` 字段 |
| `Cart item total value (qty * base_price)` | 将项目添加到购物车时，项目在之后的总值 [目录价格规则、分层折扣和特殊定价](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) ，且未应用任何税费、运费或购物车折扣。 计算方法为： `qty` 按 `base_price` |
| `Seconds since cart creation` | 从购物车的创建日期到现在之间经过的时间。 通过加入计算 `quote_item.quote_id` 到 `quote.entity_id` 并返回 `Seconds since cart creation` 字段 |
| `Store name` | 与订单项目关联的Commerce商店的名称。 通过加入计算 `sales_order_item.store_id` 到 `store.store_id` 并返回 `name` 字段 |

{style="table-layout:auto"}

## 常用量度

| **量度名称** | **描述** | **构造** |
|---|---|---|
| `Number of abandoned cart items` | 添加到符合特定“放弃”条件的购物车中的物料总数 | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>过滤器：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x，其中“x”对应于自创建购物车以来经过的时间（以秒为单位），超过该时间，购物车将被视为放弃 |
| `Abandoned cart item value` | 与满足特定“放弃”条件的购物车关联的总收入 | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>过滤器：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x，其中“x”对应于自创建购物车以来经过的时间（以秒为单位），超过该时间，购物车将被视为放弃 |

{style="table-layout:auto"}

## 外键连接路径

`catalog_product_entity`

* 加入 `catalog_product_entity` 表，用于创建返回与购物车项目关联的产品属性的列。
   * 路径： `quote_item.product_id` （许多） => `catalog_product_entity.entity_id` （一）

`quote`

* 加入 `quote` 表，用于创建与购物车项目关联的新购物车级别列。
   * 路径： `quote_item.quote_id` （许多） => `quote.entity_id` （一）

`quote_item`

* 加入 `quote_item` 创建将父可配置或捆绑SKU的详细信息与简单产品关联的列。 [联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) 以获取配置这些计算的帮助(如果在Data warehouse管理器中生成)。
   * 路径： `quote_item.parent_item_id` （许多） => `quote_item.item_id` （一）

`store`

* 加入 `store` 表以创建列，这些列返回与购物车项目关联的Commerce商店相关的详细信息。
   * 路径： `quote_item.store_id` （许多） => `store.store_id` （一）
