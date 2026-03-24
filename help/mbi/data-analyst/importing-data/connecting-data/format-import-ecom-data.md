---
title: 格式化和导入电子商务数据
description: 了解用于上传电子商务数据的理想数据格式。
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/3Aa9DgQL0H9cNeJOJ7-qHkROOkphjzpQkDvJ0KwOIwY
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 459
ht-degree: 0%

---

# 格式化和导入数据

如果您使用的集成当前不受[!DNL Adobe Commerce Intelligence]支持，您仍可以使用[文件上传功能](using-file-uploader.md)将数据导入Data Warehouse。 本主题介绍用于上传电子商务数据的理想数据格式。

## `Orders`表

对于业务已执行的每个事务，`orders`表应包含一行。 可能的列包括：

| 列名称 | 描述 |
|----|----|
| `Order ID` | 表中的每一行的订单ID应该是唯一的。 此外，这通常是表的主键。 |
| `Customer` | 下订单的客户。 |
| `Order total` | 订单总计。 这可能是基于计算的列，其中其他列中的值（如小计和运费）构成此列的总数。 |
| `Currency` | 订单付款币种。 包括（如果相关）。 |
| ` Order status` | 订单的状态，如`In Progress`、`Refunded`或`Complete`。 此列的值会更改（如果不完整）。 可以使用[页面上的](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md)附加数据功能`File Uploads`导入新的和更新的数据。 |
| `Acquisition/marketing channel` | 下订单的客户引用的客户获取或营销渠道。 |
| `Order datetime` | 创建订单的日期和时间。 |
| `Order updated at` | 上次修改订单记录的日期和时间。 |

{style="table-layout:auto"}

## `Order detail/items`表 {#itemstable}

`order_detail / items`表应按每个顺序为每个不同的项包含一行。 可能的列包括：

| 列名称 | 描述 |
|----|----|
| `Order item ID` | 订单项目ID对于表中的每一行都应是唯一的。 此外，这通常是表的`primary key`。 |
| `Order ID` | 订单的ID。 |
| `Product ID` | 产品的ID。 |
| `Product name` | 产品的名称。 |
| `Product's unit price` | 产品的单件价格。 |
| `Quantity` | 订单中产品的数量。 |

## `Customers`表 {#customerstable}

`customers`表应包含每个客户帐户的一行。 可能的列包括：

| 列名称 | 描述 |
|----|----|
| `Customer ID` | 表中的每一行的客户ID都应该是唯一的。 此外，这通常是表的主键。 |
| `Customer created at` | 客户帐户的创建日期和时间。 |
| `Customer modified at` | 上次修改客户帐户的日期和时间。 |
| `Acquisition/marketing channel source` | 客户引用的客户获取或营销渠道。 |
| `Demographic info` | 年龄范围和性别等人口统计信息可用于对报表进行分段。 |
| `Acquisition/marketing channel` | 下订单的客户引用的客户获取或营销渠道。 |

## `Subscription payments`表

`subscriptions`表应包含每个订阅付款的一行。 可能的列包括：

| 列名称 | 描述 |
|----|----|
| `Subscription ID` | 表中每一行的订阅ID都应是唯一的。 此外，这通常是表的主键。 |
| `Customer ID` | 进行付款的客户的ID。 |
| `Payment amount` | 订阅付款的金额。 |
| `Start date` | 付款涵盖期间的开始日期时间。 |
| `End date` | 付款涵盖期间的结束日期时间。 |
