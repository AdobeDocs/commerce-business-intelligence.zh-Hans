---
title: customer_entity表
description: 了解如何访问所有已注册帐户的记录。
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# customer_entity表

`customer_entity`表包含所有已注册帐户的记录。 无论客户是否完成购买，只要他们注册了一个帐户，该帐户即被视为已注册。 每一行对应于一个唯一的注册帐户，由该帐户的`entity_id`标识。

此表不包含通过访客结帐下订单的客户记录。 如果您的商店接受访客结帐，请参阅[如何对这些订单进行记帐](../data-warehouse-mgr/guest-orders.md)。

## 公用列

| **列名称** | **描述** |
|---|---|
| `created_at` | 与帐户的注册日期对应的时间戳，以UTC本地存储。 根据[!DNL Commerce Intelligence]中的配置，此时间戳可能会转换为[!DNL Commerce Intelligence]中与数据库时区不同的报表时区 |
| `email` | 与帐户关联的电子邮件地址 |
| `entity_id` (PK) | 表的唯一标识符，通常用于实例内其他表中与`customer_id`的联接 |
| `group_id` | 与`customer_group`表关联的外键。 加入`customer_group.customer_group_id`以确定与注册帐户关联的客户组 |
| `store_id` | 与`store`表关联的外键。 加入`store`。`store_id`以确定哪个Commerce商店视图与注册的帐户关联 |

{style="table-layout:auto"}

## 通用计算列

| **列名称** | **描述** |
|---|---|
| `Customer's first 30 day revenue` | 此客户在第一个订单日期后30天内下达的所有订单的总收入。 通过将`customer_entity.entity_id`加入`sales_order.customer_id`并累加`sales_order.Seconds between customer's first order date and this order`≤2592000的所有订单的`base_grand_total`字段进行计算，即30天内的秒数 |
| `Customer's first order date` | 此客户下第一个订单的时间戳。 通过将`customer_entity.entity_id`加入`sales_order.customer_id`并返回最小值`sales_order`进行计算。`created_at`值 |
| `Customer's first order's billing region` | 与客户第一张订单关联的帐单区域。 通过将`customer_entity.entity_id`加入`sales_order.customer_id`并返回`sales_order.Customer's order number` = 1的`Billing address region`进行计算 |
| `Customer's first order's coupon_code` | 与客户第一张订单关联的优惠券代码。 通过将`customer_entity.entity_id`加入`sales_order.customer_id`并返回`sales_order.Customer's order number` = 1的`sales_order.coupon_code`进行计算 |
| `Customer's group code` | 已注册客户的组名称。 通过将`customer_entity.group_id`加入`customer_group`进行计算。`customer_group_id`并返回`customer_group_code`字段 |
| `Customer's lifetime number of coupons` | 应用于此客户下达的所有订单的优惠券总数。 通过将`customer_entity.entity_id`加入`sales_order.customer_id`并计算`sales_order.coupon_code`不是`NULL`的订单数进行计算 |
| `Customer's lifetime number of orders` | 此客户下达的订单总数。 通过将`customer_entity.entity_id`加入`sales_order.customer_id`并计数`sales_order`表中的行数进行计算 |
| `Customer's lifetime revenue` | 此客户下达的所有订单的总收入。 通过将`customer_entity.entity_id`加入`sales_order.customer_id`并汇总该客户下达的所有订单的`base_grand_total`字段进行计算 |
| `Seconds since customer's first order date` | 从客户的首次订购日期到现在之间的间隔时间。 通过执行查询时从服务器时间戳中减去`Customer's first order date`计算，以整数秒数返回 |
| `Store name` | 与此注册帐户关联的Commerce存储区的名称。 通过将`customer_entity.store_id`加入`store.store_id`并返回`name`字段进行计算 |

{style="table-layout:auto"}

## 常用量度

| **量度名称** | **描述** | **构造** |
|---|---|---|
| `Avg first 30 day revenue` | 每个客户在客户首次订购后30天内下订单的平均收入 | 操作： Average<br/>操作数： `Customer's first 30 day revenue`<br/>时间戳： `created_at`<br/>筛选器：<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000 （不包括从第一次订购起尚未达到30天的客户） |
| `Avg lifetime coupons` | 每个客户在整个生命周期内应用于订单的平均优惠券数 | 操作：平均<br/>操作数： `Customer's lifetime number of coupons`<br/>时间戳： `created_at` |
| `Avg lifetime orders` | 每位客户在其生命周期内下达的平均订单数 | 操作：平均<br/>操作数： `Customer's lifetime number of orders`<br/>时间戳： `created_at` |
| `Avg lifetime revenue` | 每个客户在其整个生命周期内下达的所有订单的平均总收入 | 操作：平均<br/>操作数： `Customer's lifetime revenue`<br/>时间戳： `created_at` |
| `New customers` | 至少有一张订单的客户数，计算在其第一张订单的日期。 不包括注册但从未下订单的帐户 | 操作： Count<br/>操作数： `entity_id`<br/>时间戳： `Customer's first order date` |
| `Registered accounts` | 注册的帐户数。 包括所有已注册的帐户，无论该帐户是否下过订单 | 操作： Count<br/>操作数： `entity_id`<br/>时间戳： `created_at` |

{style="table-layout:auto"}

## 外键连接路径

`customer_group`

* 加入`customer_group`表以创建返回注册帐户的客户组名称的列。
   * 路径： `customer_entity.group_id` （多个） => `customer_group.customer_group_id` （一个）

`store`

* 加入`store`表以创建列，这些列返回与已注册帐户关联的存储相关的详细信息。
   * 路径： `customer_entity.store_id` （多个） => `store.store_id` （一个）
