---
title: 格式化和导入电子商务数据
description: 了解用于上载电子商务数据的理想数据格式。
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 格式化和导入数据

如果您使用的集成当前不受 [!DNL MBI]，您仍可以使用 [文件上传功能](using-file-uploader.md) 将数据导入data warehouse。 在本文中，我们将介绍用于上载电子商务数据的理想数据格式。

## `Orders` 表

的 `orders` 表应包含业务已进行的每次交易的一行。 可能的列包括：

| 列名称 | 描述 |
|----|----|
| `Order ID` | 对于表中的每一行，顺序ID应该都是唯一的。 此外，它通常是表的主键。 |
| `Customer` | 下订单的客户。 |
| `Order total` | 订单的总数。 此列可能是基于计算的列，其他列（如小计和发运）中的值构成此列的总数。 |
| `Currency` | 订单支付的币种。 包括（如果相关）。 |
| ` Order status` | 订单的状态，如 `In Progress`, `Refunded`或 `Complete`. 此列的值可能会发生更改（如果未完成）。 可使用 [附加数据功能](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) 在 `File Uploads` 页面。 |
| `Acquisition/marketing channel` | 下订单的客户从中引荐的客户获取或营销渠道。 |
| `Order datetime` | 创建订单的日期和时间。 |
| `Order updated at` | 对订单记录进行上次修改的日期和时间。 |

{style=&quot;table-layout:auto&quot;}

## `Order detail/items` 表 {#itemstable}

的 `order_detail / items` 表应按每个顺序为每个不同项目包含一行。 可能的列包括：

| 列名称 | 描述 |
|----|----|
| `Order item ID` | 对于表中的每一行，订单项目ID都应是唯一的。 此外，通常是 `primary key` 的位置。 |
| `Order ID` | 订单的ID。 |
| `Product ID` | 产品的ID。 |
| `Product name` | 产品的名称。 |
| `Product's unit price` | 单件产品的价格。 |
| `Quantity` | 订单中产品的数量。 |

## `Customers` 表 {#customerstable}

的 `customers` 每个客户帐户应包含一行。 可能的列包括：

| 列名称 | 描述 |
|----|----|
| `Customer ID` | 表中每一行的客户ID都应是唯一的。 此外，它通常是表的主键。 |
| `Customer created at` | 客户帐户的创建日期和时间。 |
| `Customer modified at` | 上次修改客户帐户的日期和时间。 |
| `Acquisition/marketing channel source` | 客户从中引荐的客户获取或营销渠道。 |
| `Demographic info` | 人口统计信息（如年龄范围和性别）可用于对报表进行分段。 |
| `Acquisition/marketing channel` | 下订单的客户从中引荐的客户获取或营销渠道。 |

## `Subscription payments` 表

的 `subscriptions` 每个订阅付款应包含一行。 可能的列包括：

| 列名称 | 描述 |
|----|----|
| `Subscription ID` | 表中每一行的订阅ID都应是唯一的。 此外，它通常是表的主键。 |
| `Customer ID` | 付款的客户的ID。 |
| `Payment amount` | 订阅付款的金额。 |
| `Start date` | 付款涵盖的时段的开始日期时间。 |
| `End date` | 付款涵盖的时段的结束日期时间。 |
