---
title: 访客订单
description: 了解访客订单对您数据的影响，以及对于您的中的访客订单，您必须正确考虑哪些选项 [!DNL Commerce Intelligence] Data Warehouse。
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# 访客订单

在复查订单时，如果您注意到 `customer\_id` 值为null或没有要连接回的值 `customers` 表格，这表示您的商店允许访客订购。 这意味着您的 `customers` 表很可能未包含您的所有客户。

本主题讨论访客订单对您的数据的影响，以及对于贵机构的访客订单，您必须正确考虑哪些选项。 [!DNL Commerce Intelligence] Data Warehouse。

## 访客订单对数据的影响

在典型的商务数据库中， `orders` 连接到的表 `customers` 表格。 上的每一行 `orders` 表格具有 `customer\_id` 列上的一行所独有的 `customers` 表格。

* **如果所有客户都已注册** 客服订单是不被允许的，这意味着 `orders` 表中有一个值 `customer\_id` 列。 因此，每个订单都会重新加入 `customers` 表格。

  ![](../../assets/guest-orders-4.png)

* **如果允许来宾订单**，这表示某些订单在 `customer\_id` 列。 只有注册客户会获得 `customer\_id` 上的列 `orders` 表格。 未注册的客户将获得 `NULL` （或空白）值。 因此，并非所有订单记录在 `customers` 表格。

  >[!NOTE]
  >
  >要确定发出订单的唯一个人，需要在旁边添加另一个唯一用户属性 `customer\_id` 已附加到订单。 通常使用客户的电子邮件地址。

## 如何在Data Warehouse设置中考虑来宾订单

通常，实施您的帐户的销售工程师在建立Data Warehouse的基础时会考虑来宾订单。

考虑访客订单的最佳方法是将所有客户级别的量度都基于 `orders` 表格。 此设置使用所有客户拥有的唯一客户ID，包括来宾（通常使用客户电子邮件）。 这将忽略来自的注册数据 `customers` 表格。 利用此选项，客户级别报表中只会包含至少购买过一次的客户。 尚未购买一次的注册用户不包括在内。 通过此选项，您的 `New customer` 量度基于客户在 `orders` 表格。

您可能会注意到 `Customers we count` 在此类型的设置中设置的过滤器具有针对以下项的过滤器 `Customer's order number = 1`.

![](../../assets/guest-orders-filter-set.png)

在没有访客订单的情况下，每个客户在客户表中都作为唯一行存在（请参阅图1）。 量度，例如 `New customers` 可以简单地根据以下条件计数此表的ID： `created\_at` 基于注册日期了解新客户的日期。

在访客订单设置中，所有客户量度均基于 `orders` 要考虑来宾订单的表，您必须确保 `not counting customers twice`. 如果计算订单表的ID，则计算每个订单。 如果您将id计入 `orders` 表格并使用过滤器， `Customer's order number = 1`，然后您将计算每个独特客户 `only one time`. 这适用于所有客户级别的量度，例如 `Customer's lifetime revenue` 或 `Customer's lifetime number of orders`.

您可以看到上面有空值 `customer\_ids` 在 `orders` 表格。 如果您使用 `customer\_email` 要识别独特客户，您可以看到 `erin@test.com` 下了三(3)份订单。 因此，您可以构建 `New customers` 量度 `orders` 表，该表基于以下条件：

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
