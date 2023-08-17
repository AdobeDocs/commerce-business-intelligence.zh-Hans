---
title: 预期的Spree数据
description: 探索可从Spree导入的主要数据表 [!DNL Commerce Intelligence] 帐户。
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# 预期 [!DNL Spree] 数据

在您拥有 [已连接 [!DNL Spree] 存储](../../../data-analyst/importing-data/integrations/spree.md)，您可以使用 [Data Warehouse管理器](../../data-warehouse-mgr/tour-dwm.md) 以轻松地跟踪来自贵机构的 [!DNL Spree] 平台分析。

本主题探讨可从其中导入的主要数据表 [!DNL Spree] 到您的 [!DNL Commerce Intelligence] 帐户，包括指向的链接 [其他文档](https://guides.spreecommerce.org/developer/addresses.html#address) 关于 [!DNL Spree] 数据。

| **表名** | **描述** |
|-----|-----|
| `Users` | 此 `users` 该表包括已注册客户的帐户详细信息，包括个人的电子邮件、姓名和注册日期。 这允许您分析不同的客户区段及其购买行为。 |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | 此 `orders` 表将用作所有订单级量度的基础。 此处记录的是向贵机构购买的所有订单详细信息。 [!DNL Spree] 存储，包括 `completed\_at` （订单的时间戳）， `user\_id` （下订单的注册用户的id）。 如果订单是由注册用户发出的， `user\_id` 链接回到 `users` 此表允许对用户购买行为进行分析。 |
| `Line items` | 此 `line\_items` 表是以下任一对象的子项： `orders` 表或 `subscriptions`. 它记录订单或订阅的行项目详细信息。 对于具有多个产品的订单，此表中每个产品都有各自的数据行，包括 `product\_id` 这样您就可以将其绑定到 `Products` 表格。 |
| `Products` | 此 `products` 该表记录了Spree目录中可销售项目的所有产品详细信息。 这样，您就可以按产品属性对行项目级别量度进行分段。 |
| `Subscriptions` | 如果您拥有 [!DNL Spree] 订阅扩展， `subscriptions` 表格包含每个单独订阅的信息，包括 `created\_at` （开始日期）， `cancelled\_at` （取消订阅的日期）及 `interval` 订阅的ID。 |

{style="table-layout:auto"}

## 相关：

* [正在连接 [!DNL Spree]](../integrations/spree.md)
* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
