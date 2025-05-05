---
title: quote_item表
description: 了解如何使用quote_item表。
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# quote_item表

`quote_item`表（ M1上的`sales_flat_quote_item`）包含添加到购物车的每个项目的记录，无论购物车是放弃还是转换为购买。 每一行表示一个购物车项目。 由于此表可能的大小问题，Adobe建议您在满足某些条件时定期删除记录，例如，如果有任何超过60天的未转换购物车。

>[!NOTE]
>
>仅当不从`quote`和`quote_item`表中删除记录时，才可能分析已放弃的历史购物车。 如果确实删除了记录，则只能看到尚未从数据库中删除的购物车。

## 通用本机列

| **列名称** | **描述** |
|---|---|
| `base_price` | 在应用了[目录价格规则、分层折扣和特殊定价](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=zh-Hans)之后以及在应用任何税、运费或购物车折扣之前，将产品添加到购物车时产品的单件价格。 以存储的基本货币表示。 |
| `created_at` | 购物车项目的创建时间戳，以UTC本地存储。 根据[!DNL Commerce Intelligence]中的配置，此时间戳可能会转换为[!DNL Commerce Intelligence]中与数据库时区不同的报表时区 |
| `item_id` (PK) | 表的唯一标识符 |
| `name` | 订单项的文本名称 |
| `parent_item_id` | 将简单产品与其父捆绑包或可配置产品相关联的`Foreign key`。 加入`quote_item.item_id`以确定与简单产品关联的父产品属性。 对于父购物车项目（即捆绑包或可配置产品类型），`parent_item_id`为`NULL` |
| `product_id` | 与`catalog_product_entity`表关联的`Foreign key`。 加入`catalog_product_entity.entity_id`以确定与订单项关联的产品属性 |
| `product_type` | 添加到购物车的产品的类型。 潜在的[产品类型](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html?lang=zh-Hans#product-types)包括：简单、可配置、已分组、虚拟、捆绑和可下载 |
| `qty` | 特定购物车项目的购物车中包含的单位数量 |
| `quote_id` | 与`quote`表关联的`Foreign key`。 加入`quote.entity_id`以确定与购物车项目关联的购物车属性 |
| `sku` | 购物车项目的唯一标识符 |
| `store_id` | 与`store`表关联的外键。 加入`store.store_id`以确定哪个Commerce商店视图与购物车项目关联 |

{style="table-layout:auto"}

## 通用计算列

| **列名称** | **描述** |
|---|---|
| `Cart creation date` | 与购物车创建日期关联的时间戳。 通过将`quote_item.quote_id`加入`quote.entity_id`并返回`created_at`时间戳进行计算 |
| `Cart is active? (1/0)` | 如果购物车由客户创建且尚未转换为订单，则返回值为“1”的布尔字段。 对于已转换的购物车或通过管理员创建的购物车，返回“0”。 通过将`quote_item.quote_id`加入`quote.entity_id`并返回`is_active`字段进行计算 |
| `Cart item total value (qty * base_price)` | 在应用了[目录价格规则、分层折扣和特殊定价](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=zh-Hans)之后且未应用任何税、运费或购物车折扣的情况下，将项目添加到购物车时的项目总值。 通过`qty`乘以`base_price`计算 |
| `Seconds since cart creation` | 从购物车创建日期到现在之间经过的时间。 通过将`quote_item.quote_id`加入`quote.entity_id`并返回`Seconds since cart creation`字段进行计算 |
| `Store name` | 与订单项目关联的Commerce商店的名称。 通过将`sales_order_item.store_id`加入`store.store_id`并返回`name`字段进行计算 |

{style="table-layout:auto"}

## 常用量度

| **量度名称** | **描述** | **构造** |
|---|---|---|
| `Number of abandoned cart items` | 添加到购物车且满足特定“放弃”条件的项目总数 | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>过滤器：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x，其中“x”对应于自创建购物车以来经过的时间（以秒为单位），超过该时间，购物车将被放弃 |
| `Abandoned cart item value` | 与满足特定“放弃”条件的购物车关联的总收入 | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>过滤器：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x，其中“x”对应于自创建购物车以来经过的时间（以秒为单位），超过该时间，购物车将被放弃 |

{style="table-layout:auto"}

## 外键连接路径

`catalog_product_entity`

* 加入`catalog_product_entity`表以创建返回与购物车项目关联的产品属性的列。
   * 路径： `quote_item.product_id` （多个） => `catalog_product_entity.entity_id` （一个）

`quote`

* 加入`quote`表以创建与购物车项目关联的新购物车级别列。
   * 路径： `quote_item.quote_id` （多个） => `quote.entity_id` （一个）

`quote_item`

* 加入`quote_item`以创建将父可配置或捆绑SKU的详细信息与简单产品关联的列。 在Data Warehouse管理器中构建时，[联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hans)以获得配置这些计算的帮助。
   * 路径： `quote_item.parent_item_id` （多个） => `quote_item.item_id` （一个）

`store`

* 加入`store`表以创建列，这些列返回与购物车项目关联的Commerce商店相关的详细信息。
   * 路径： `quote_item.store_id` （多个） => `store.store_id` （一个）
