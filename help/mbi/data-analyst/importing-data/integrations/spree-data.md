---
title: 预期Spree数据
description: 浏览可从Spree导入到 [!DNL MBI] 帐户。
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# 预期 [!DNL Spree] 数据

在 [已连接 [!DNL Spree] 商店](../../../data-analyst/importing-data/integrations/spree.md)，则可以使用 [data warehouse管理器](../../data-warehouse-mgr/tour-dwm.md) 轻松跟踪 [!DNL Spree] 分析平台。

在本文中，我们将探索可从中导入的主要数据表 [!DNL Spree] 到 [!DNL MBI] 帐户，包括指向的链接 [其他文档](https://guides.spreecommerce.org/developer/addresses.html#address) 关于 [!DNL Spree] 数据。

| **表名称** | **描述** |
|-----|-----|
| `Users` | 的 `users` 表格包括注册客户的帐户详细信息，包括个人的电子邮件、姓名和注册日期。 这允许您分析不同的客户区段及其购买行为。 |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | 的 `orders` 表用作所有订单级别量度的基础。 此处记录了您的 [!DNL Spree] 商店，包括 `completed\_at` （订单的时间戳）， `user\_id` （下订单的注册用户的id）。 如果订单是由注册用户下达，则 `user\_id` 将链接回 `users` 表格，用于分析用户购买行为。 |
| `Line items` | 的 `line\_items` 表是任一表的子项 `orders` 表或 `subscriptions`. 它记录订单或订阅的行项目详细信息。 对于具有多个产品的订单，每个产品在此表中都有其自己的数据行，包括 `product\_id` 这样你就能把它绑在 `Products` 表。 |
| [`Products`](https://guides.spreecommerce.com/developer/products.html#overview) | 的 `products` 表格在Spree目录中记录可销售项目的所有产品详细信息。 这允许您按产品属性对行项目级别量度进行分段。 |
| `Subscriptions` | 如果您有 [!DNL Spree] 订阅扩展， `subscriptions` 表格包含每个订阅的信息，包括 `created\_at` （开始日期）、 `cancelled\_at` （取消订阅的日期）， `interval` 订购。 |

{style=&quot;table-layout:auto&quot;}

## 相关：

* [连接 [!DNL Spree]](../integrations/spree.md)
* [重新验证集成](https://support.magento.com/hc/en-us/articles/360016733151)
