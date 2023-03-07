---
title: 预期的Spree数据
description: 探索可从Spree导入的主要数据表 [!DNL MBI] 帐户。
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# 预期 [!DNL Spree] 数据

在您拥有 [已连接 [!DNL Spree] 存储](../../../data-analyst/importing-data/integrations/spree.md)，您可以使用 [data warehouse管理器](../../data-warehouse-mgr/tour-dwm.md) 轻松跟踪来自贵机构的 [!DNL Spree] 平台分析。

本文探讨可从其中导入的主要数据表 [!DNL Spree] 到您的 [!DNL MBI] 帐户，包括指向的链接 [其他文档](https://guides.spreecommerce.org/developer/addresses.html#address) 关于 [!DNL Spree] 数据。

| **表名** | **描述** |
|-----|-----|
| `Users` | 此 `users` 该表包括已注册客户的帐户详细信息，包括个人电子邮件、姓名和注册日期。 这允许您分析不同的客户区段及其购买行为。 |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | 此 `orders` 表是所有订单级别量度的基础。 此处记录的是从贵机构购买的所有订单详细信息。 [!DNL Spree] 商店，包括 `completed\_at` （订单的时间戳）， `user\_id` （下订单的注册用户的id）。 如果订单是由注册用户发出的， `user\_id` 链接回到 `users` 表格，用于分析用户购买行为。 |
| `Line items` | 此 `line\_items` 表是以下任一项的子项： `orders` 表或 `subscriptions`. 它记录订单或订阅的行项目详细信息。 对于具有多个产品的订单，每个产品在此表中都有各自的数据行，包括 `product\_id` 这样您就可以将其绑定到 `Products` 表格。 |
| `Products` | 此 `products` 此表记录了Spree目录中可销售项目的所有产品详细信息。 这样，您就可以按产品属性对行项目级别量度进行分段。 |
| `Subscriptions` | 如果您拥有 [!DNL Spree] 订阅扩展， `subscriptions` 此表包含每个单独订阅的信息，包括 `created\_at` （开始日期）， `cancelled\_at` （取消订阅的日期）及 `interval` 订阅的ID。 |

{style="table-layout:auto"}

## 相关：

* [正在连接 [!DNL Spree]](../integrations/spree.md)
* [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
