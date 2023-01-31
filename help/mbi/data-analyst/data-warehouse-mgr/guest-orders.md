---
title: 来宾订单
description: 了解来宾订单对您的数据的影响，以及您必须选择哪些选项才能正确考虑您的 [!DNL MBI] data warehouse。
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# 来宾订单

在审核订单时，如果您发现 `customer\_id` 值为null或没有值可连接回 `customers` 表格，这通常表示您的商店允许客人订购。 这表示您的 `customers` 表很可能不包含所有客户。

在本主题中，我们将讨论来宾订单对您的数据的影响，以及您在 [!DNL MBI] data warehouse。

## 来宾订单对数据的影响

在典型的商务数据库中， `orders` 连接到 `customers` 表。 在 `orders` 表具有 `customer\_id` 对于 `customers` 表。

* **如果所有客户都已注册** 不允许客人订单，这意味着 `orders` 表在 `customer\_id` 列。 因此，每个订单都会返回到 `customers` 表。 您可以在下图中看到此内容。

   ![](../../assets/guest-orders-4.png)

* **如果允许来宾订单**，这表示某些订单在 `customer\_id` 列。 只有已注册的客户才会为 `customer\_id` 列 `orders` 表。 未注册的客户将收到 `NULL` （或空白）值。 因此，并非所有订单记录在 `customers` 表。

   >[!NOTE]
   >
   >要识别下订单的独特用户，需要在 `customer\_id` 附加在订单上。 通常使用客户的电子邮件地址。

## 如何在data warehouse设置中考虑来宾订单

通常，实施您帐户的销售工程师在构建data warehouse基础时会考虑来宾订单。

考虑来宾订单的最佳方式是将所有客户级别的量度基于 `orders` 表。 此设置将使用所有客户都具有的唯一客户ID，包括来宾（通常使用客户电子邮件）。 这会忽略 `customers` 表。 使用此选项，只有至少购买过一次的客户才会包含在客户级别报表中。 尚未购买过商品的注册用户将不包括在内。 使用此选项， `New customer` 量度将基于 `orders` 表。

您可能会注意到 `Customers we count` 在此类型的设置中设置的过滤器具有 `Customer's order number = 1`. 让我们想想为什么会这样。

![](../../assets/guest-orders-filter-set.png)

在没有来宾订单的情况下，每个客户在客户表中都作为唯一行存在（请参阅图1）。 量度，例如 `New customers` 只需根据 `created\_at` 以了解基于注册日期的新客户的日期。

在来宾订单设置中，所有客户量度都基于 `orders` 表来考虑来宾订单，您需要确保 `not counting customers twice`. 如果计算订单表的ID，则将计算每个订单。 如果改为，您会在 `orders` 表格，使用过滤器， `Customer's order number = 1`，则您将对每个独特客户进行计数 `only one time`. 这适用于所有客户级别的量度，例如 `Customer's lifetime revenue` 或 `Customer's lifetime number of orders`.

在上图2中，您可以看到空值 `customer\_ids` 在 `orders` 表。 如果我们使用 `customer\_email` 要识别独特客户，您可以看到 `erin@test.com` 已经下了三(3)个订单。 因此，我们可以 `New customers` 量度 `orders` 表基于以下条件：

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
