---
title: 格式化和导入电子商务数据
description: 了解上传电子商务数据所使用的理想数据格式。
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# 格式化和导入数据

如果您使用的集成当前不受支持 [!DNL MBI]，您仍然可以使用 [文件上传功能](using-file-uploader.md) 将数据导入Data warehouse。 本文介绍了上传电子商务数据时要使用的理想数据格式。

## `Orders` 表

此 `orders` 对于企业已执行的每项事务处理，表应包含一行。 可能的列包括：

| 列名称 | 描述 |
|----|----|
| `Order ID` | 表中的每一行的订单ID应该是唯一的。 此外，这通常是表的主键。 |
| `Customer` | 下订单的客户。 |
| `Order total` | 订单总计。 这可能是一个基于计算的列，其中其他列中的值（如小计和发运）构成此列的总计。 |
| `Currency` | 支付订单所用的货币。 包括相关内容。 |
| ` Order status` | 订单的状态，如 `In Progress`， `Refunded`，或 `Complete`. 此列的值会更改（如果不完整）。 新的和更新的数据可以使用导入 [附加数据功能](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) 在 `File Uploads` 页面。 |
| `Acquisition/marketing channel` | 下订单的客户引用的客户获取或营销渠道。 |
| `Order datetime` | 创建订单的日期和时间。 |
| `Order updated at` | 上次修改订单记录的日期和时间。 |

{style="table-layout:auto"}

## `Order detail/items` 表 {#itemstable}

此 `order_detail / items` 表格应包含每个顺序中每个不同项目的一行。 可能的列包括：

| 列名称 | 描述 |
|----|----|
| `Order item ID` | 订单项目ID对于表中的每一行都应是唯一的。 此外，这通常是 `primary key` 为表格创建。 |
| `Order ID` | 订单的ID。 |
| `Product ID` | 产品的ID。 |
| `Product name` | 产品的名称。 |
| `Product's unit price` | 产品的单件价格。 |
| `Quantity` | 订单中产品的数量。 |

## `Customers` 表 {#customerstable}

此 `customers` 表格应包含每个客户帐户的一行。 可能的列包括：

| 列名称 | 描述 |
|----|----|
| `Customer ID` | 表中的每一行的客户ID都应该是唯一的。 此外，这通常是表的主键。 |
| `Customer created at` | 创建客户帐户的日期和时间。 |
| `Customer modified at` | 上次修改客户帐户的日期和时间。 |
| `Acquisition/marketing channel source` | 客户引用的客户获取或营销渠道。 |
| `Demographic info` | 年龄范围和性别等人口统计信息可用于对报表进行分段。 |
| `Acquisition/marketing channel` | 下订单的客户引用的客户获取或营销渠道。 |

## `Subscription payments` 表

此 `subscriptions` 对于每次订阅付款，表格应包含一行。 可能的列包括：

| 列名称 | 描述 |
|----|----|
| `Subscription ID` | 表中每一行的订阅ID都应是唯一的。 此外，这通常是表的主键。 |
| `Customer ID` | 付款的客户的ID。 |
| `Payment amount` | 订阅付款的金额。 |
| `Start date` | 付款涵盖期间的开始日期时间。 |
| `End date` | 付款涵盖期间的结束日期时间。 |
