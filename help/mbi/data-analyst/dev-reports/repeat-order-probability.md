---
title: 重复订购概率报表
description: 了解并了解重复订购概率报表。
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# 重复订购概率报表

## `Incremental Event Probability`透视何时可用？

仅当过滤器使用的维度对所有订单（例如，用户的`gender`、用户的`age`或用户的`source`）均相等时，`incremental event probability`透视才可用。

这是因为此透视依赖于名为`User's order number`的维度来进行分段，该维度用于统计用户的购买量（例如，John的第一次、第二次和第三次订单）。

如果您添加的过滤器使用的维度不是对所有订单都相等（例如，`Order's Region`），`User's order number`维度将不再准确。 这是因为在为用户的订单编号时，它不考虑特定区域（例如，John的第1、2、3个订单仍然相同，无论其区域如何）。

## 将特定于订单的维度转换为特定于用户的维度

在某些情况下，您也许能够将`order-specific`维度转换为`user-specific`维度以添加为`Repeat Order Probability`图表中的筛选器。 在这些情况下，将返回用户第一订单或最新订单的订单属性（例如，用户的第一订单区域名称）。

如果要创建此类新维度，请[联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

## 不同属性订单重复概率的比较

要比较不同订单属性（例如，订单的`region`）的重复购买次数，Adobe建议创建类似于`Users by lifetime number of orders`的图表。 它显示发出1、2、3、...生命周期订单数并添加订单级别过滤器的用户数。 （换句话说，它可以向您显示用户是否在一个地区或另一个地区进行了多次重复购买。）

然后，可以将构成此类图表的数字导出到excel以计算重复顺序概率比率。 要查看客户发出`(x)`个订单以发出`(x+1)`个订单的概率，只需` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)`次购买。

### 示例：

| 类别 | 值 |
|---|---|
| 一生中购买过1次的客户的数量 | `90` |
| 一生中购买过2次的客户数 | `30` |
| 一生中购买过3次的客户的数量 | `10` |
| 已购买过一次的客户进行第二次购买的重复订购概率 | `(30 + 10) / (30+10+90) = 30.77%` |
