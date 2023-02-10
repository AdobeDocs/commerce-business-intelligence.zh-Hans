---
title: 重复顺序概率报表
description: 了解并了解重复订单概率报表。
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# 重复顺序概率报表

## 何时为 `Incremental Event Probability` 透视图可用？

的 `incremental event probability` 仅当过滤器使用的维度与所有订单的维度相等时(例如，用户的 `gender`，用户的 `age` 或用户的 `source`)

这是因为此视角依赖于一个名为 `User's order number` 用于区段，用于为用户的购买次数（例如，John的第1次、第2次和第3次订购）计数。

如果要添加一个过滤器，该过滤器使用的维度对于所有订单来说并不等于(例如， `Order's Region`)、 `User's order number` 维度不再准确，因为它在为用户的订单编号时不考虑特定区域（例如，John的第1、第2、第3个订单仍然相同，无论其所在区域如何）。

## 将特定于订单的维度转换为特定于用户的维度

在某些情况下，我们可以 `order-specific` 维度 `user-specific` 要添加为过滤器的维度 `Repeat Order Probability` 图表。 在这些情况下，我们将返回用户的首次订购或最新订购的订单属性（例如，用户的首次订购区域名称）。

如果要创建此类新维度， [联系支持](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

## 不同属性下订单重复概率的比较

比较不同订单属性(例如，订单的 `region`)，我们建议创建类似于 `Users by lifetime number of orders` 它显示完成1、2、3、...生命周期订单数的用户数，并添加订单层过滤器。 （换言之，这可显示用户是在一个地区还是另一个地区重复购买的次数是否更多。）

然后，构成此图表的数字可导出到excel以计算重复顺序概率比。 查看客户完成 `(x)` 订单 `(x+1)` 订购，简单` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` 购买。

### 示例：

|  |  |
|---|---|
| 在其生命周期内购买1次产品的客户数量 | `90` |
| 在有生命周期内购买过2次产品的客户数量 | `30` |
| 在其生命周期内购买过3次产品的客户数量 | `10` |
| 在生命周期内购买过一次产品的客户再次购买产品的重复订单概率 | `(30 + 10) / (30+10+90) = 30.77%` |
