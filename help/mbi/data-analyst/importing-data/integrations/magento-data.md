---
title: 预期商务数据
description: 浏览商务用户导入MBI的主要数据表
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# 预期商务数据

在 [连接了您的商务商店](../../../data-analyst/importing-data/integrations/magento.md)，则可以使用Data warehouse管理器轻松跟踪商务数据库中的相关数据字段进行分析。

在本文中，我们将探索商务用户导入的主要数据表 [!DNL MBI].

| **表名称** | **描述** |
|-----|-----|
| `Customers` | 的 `customer\_entity` 和相关表描述了与每个 *注册客户* ，如其电子邮件地址和注册日期。 根据此信息，您可以按客户级别属性和同类群组开始分段。 |
| `Orders` | 的 `sales\_flat\_order` 表记录所有订单，包括 `created\_at` 下单的时间戳和 `base\_grand\_total` 字段来计算收入。 这些字段将作为您的订单级别量度的基础。 如果订单是由 *注册客户*, `customer\_id` 字段将链接回  `customer\_entity` 表格，用于分析客户购买行为。 |
| `Order items` | 的 `sales\_flat\_order\_item` 表记录属于订单的每个项目。 这包括 `price` 和 `qty\_ordered` 字段 `order\_id` 连接到的字段 `sales\_flat\_order` 表。 此表为 `Item sold`，并允许您按 `product` 和 `product type`. |
| `Products` | 的 `catalog\_product\_entity` 表存储有关产品级别属性的信息，如类别、大小和颜色。 |
| `Categories` | 您的产品将属于一个或多个不同的产品 `product categories`，具体取决于商务内部版本的设置方式。 的 `catalog\_category\_entity` 表存储了这些类别的层次结构（例如，Apprarel > Tops > T恤），以及 `catalog\_category\_product` 表格记录您的产品与这些类别之间的连接。 |

{style=&quot;table-layout:auto&quot;}

## 相关

* [连接 [!DNL Adobe Commerce]](../integrations/magento.md)
* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
