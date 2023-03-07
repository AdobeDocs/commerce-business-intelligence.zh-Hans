---
title: 预期的Commerce数据
description: 探索Commerce用户导入MBI的主要数据表
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# 预期的Commerce数据

在您拥有 [已连接您的Commerce商店](../../../data-analyst/importing-data/integrations/magento.md)，您可以使用Data warehouse管理器轻松地跟踪Commerce数据库中的相关数据字段以供分析。

本文探索Commerce用户导入的主要数据表 [!DNL MBI].

| **表名** | **描述** |
|-----|-----|
| `Customers` | 此 `customer\_entity` 和相关的表描述与每个报表包关联的信息 *注册客户* ，如电子邮件地址和注册日期。 利用此信息，您可以开始按客户级别的属性和同类群组进行分段。 |
| `Orders` | 此 `sales\_flat\_order` 表格记录所有订单，包括 `created\_at` 下订单的时间戳以及 `base\_grand\_total` 汇总收入的字段。 这些字段是订单级别量度的基础。 如果订单是由 *注册客户*，则 `customer\_id` 字段链接回到  `customer\_entity` 表，以允许分析客户购买行为。 |
| `Order items` | 此 `sales\_flat\_order\_item` 表记录属于订单的每个项目。 这包括 `price` 和 `qty\_ordered` 字段，以及 `order\_id` 连接到以下项的字段： `sales\_flat\_order` 表格。 此表是以下指标的基础 `Item sold`，并允许您按以下方式分段： `product` 和 `product type`. |
| `Products` | 此 `catalog\_product\_entity` 表格存储有关产品级别属性的信息，如类别、大小和颜色。 |
| `Categories` | 您的产品属于一个或多个不同的产品 `product categories`，具体取决于Commerce内部版本的设置方式。 此 `catalog\_category\_entity` 此表存储了这些类别的层次结构（例如，服装>上衣> T恤），以及 `catalog\_category\_product` 该表记录您的产品与这些类别之间的连接。 |

{style="table-layout:auto"}

## 相关

* [正在连接 [!DNL Adobe Commerce]](../integrations/magento.md)
* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
