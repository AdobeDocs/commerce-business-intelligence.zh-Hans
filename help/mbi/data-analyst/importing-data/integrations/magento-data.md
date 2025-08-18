---
title: 预期Commerce数据
description: 浏览Commerce用户导入Commerce Intelligence的主要数据表
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 预期[!DNL Adobe Commerce]数据

在您[连接 [!DNL Adobe Commerce] 存储区](../../../data-analyst/importing-data/integrations/magento.md)后，您可以使用Data Warehouse Manager轻松地跟踪Commerce数据库中的相关数据字段以供分析。

本主题探讨Commerce用户导入到[!DNL Commerce Intelligence]中的主要数据表。

| **表名** | **描述** |
|-----|-----|
| `Customers` | `customer\_entity`和相关表描述了与数据库中的每个&#x200B;*注册客户*&#x200B;相关联的信息，如其电子邮件地址和注册日期。 利用这些信息，您可以开始按客户级别的属性和同类群组进行分段。 |
| `Orders` | `sales\_flat\_order`表记录所有订单，包括发出订单的`created\_at`时间戳和汇总收入的`base\_grand\_total`字段。 这些字段是订单级别量度的基础。 如果订单是由&#x200B;*注册客户*&#x200B;发出的，`customer\_id`字段将链接回`customer\_entity`表，以便分析客户的购买行为。 |
| `Order items` | `sales\_flat\_order\_item`表记录每个属于订单的项目。 这包括`price`和`qty\_ordered`字段以及连接到`order\_id`表的`sales\_flat\_order`字段。 此表是`Item sold`等量度的基础，允许您按`product`和`product type`进行分段。 |
| `Products` | `catalog\_product\_entity`表存储有关产品级属性的信息，如类别、大小和颜色。 |
| `Categories` | 您的产品属于一个或多个不同的`product categories`，具体取决于您的Commerce内部版本的设置方式。 `catalog\_category\_entity`表存储这些类别的层次结构（例如，服装>上衣> T恤），`catalog\_category\_product`表记录您的产品与这些类别之间的连接。 |

{style="table-layout:auto"}

## 相关

* [正在连接 [!DNL Adobe Commerce]](../integrations/magento.md)
* [正在重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
