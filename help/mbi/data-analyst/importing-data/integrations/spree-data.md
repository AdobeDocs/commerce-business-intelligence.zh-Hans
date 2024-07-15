---
title: 预期的Spree数据
description: 浏览可从Spree导入到 [!DNL Commerce Intelligence] 帐户中的主数据表。
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 预期[!DNL Spree]数据

在您[连接 [!DNL Spree] 存储](../../../data-analyst/importing-data/integrations/spree.md)后，您可以使用[Data Warehouse管理器](../../data-warehouse-mgr/tour-dwm.md)轻松地跟踪来自[!DNL Spree]平台的相关数据字段以供分析。

本主题探索可从[!DNL Spree]导入到[!DNL Commerce Intelligence]帐户的主要数据表，包括指向[其他文档](https://guides.spreecommerce.org/developer/addresses.html#address)有关[!DNL Spree]数据的链接。

| **表名** | **描述** |
|-----|-----|
| `Users` | `users`表包括已注册客户的帐户详细信息，包括个人电子邮件、姓名和注册日期。 这允许您分析不同的客户区段及其购买行为。 |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | `orders`表用作所有订单级量度的基础。 此处记录的是从您的[!DNL Spree]商店购买的所有订单详细信息，包括`completed\_at`（订单的时间戳）、`user\_id`（下订单的注册用户的ID）。 如果订单是由注册用户发出的，则`user\_id`将链接回`users`表，以便分析用户购买行为。 |
| `Line items` | `line\_items`表是`orders`表或`subscriptions`的子表。 它记录订单或订阅的行项目详细信息。 对于具有多个产品的订单，此表中每个产品都有各自的数据行，包括允许您将它绑定到`Products`表的`product\_id`。 |
| `Products` | `products`表在您的Spree目录中记录可销售项目的所有产品详细信息。 这样，您就可以按产品属性对行项目级别量度进行分段。 |
| `Subscriptions` | 如果您有[!DNL Spree]订阅扩展，则`subscriptions`表将保留每个单独订阅的信息，包括`created\_at` （开始日期）、`cancelled\_at` （取消订阅的日期）和订阅的`interval`。 |

{style="table-layout:auto"}

## 相关：

* [正在连接 [!DNL Spree]](../integrations/spree.md)
* [正在重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
