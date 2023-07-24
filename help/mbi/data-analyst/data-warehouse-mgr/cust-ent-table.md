---
title: customer_entity表
description: 了解如何访问所有已注册帐户的记录。
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# customer_entity表

此 `customer_entity` 表包含所有已注册帐户的记录。 无论客户是否完成购买，只要他们注册了一个帐户，该帐户即被视为已注册。 每一行对应于一个唯一的注册帐户，该帐户的 `entity_id`.

此表不包含通过访客结帐发出订单的客户记录。 如果您的商店接受访客结帐，请参阅 [如何记录访客订单](../data-warehouse-mgr/guest-orders.md) 为了那些订单。

## 公用列

| **列名称** | **描述** |
|---|---|
| `created_at` | 与帐户的注册日期对应的时间戳，以UTC本地存储。 取决于您在中的配置 [!DNL Commerce Intelligence]时，此时间戳可能会转换为中的报表时区 [!DNL Commerce Intelligence] 与您的数据库时区不同 |
| `email` | 与帐户关联的电子邮件地址 |
| `entity_id` (PK) | 表的唯一标识符，通常用于联接 `customer_id` 在实例中的其他表中 |
| `group_id` | 与关联的外键 `customer_group` 表格。 加入 `customer_group.customer_group_id` 确定与注册帐户关联的客户组 |
| `store_id` | 与关联的外键 `store` 表格。 加入 `store`.`store_id` 以确定哪个Commerce商店视图与注册的帐户关联 |

{style="table-layout:auto"}

## 通用计算列

| **列名称** | **描述** |
|---|---|
| `Customer's first 30 day revenue` | 该客户在首次订购日期后30天内下达的所有订单的收入总计。 通过加入计算 `customer_entity.entity_id` 到 `sales_order.customer_id` 并总结 `base_grand_total` 所有订单的字段，其中 `sales_order.Seconds between customer's first order date and this order` ≤ 2592000，即30天内的秒数 |
| `Customer's first order date` | 此客户下第一个订单的时间戳。 通过加入计算 `customer_entity.entity_id` 到 `sales_order.customer_id` 并返回最小值 `sales_order`.`created_at` 值 |
| `Customer's first order's billing region` | 与客户第一张订单关联的开单区域。 通过加入计算 `customer_entity.entity_id` 到 `sales_order.customer_id` 并返回 `Billing address region` 位置 `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | 与客户第一张订单关联的优惠券代码。 通过加入计算 `customer_entity.entity_id` 到 `sales_order.customer_id` 并返回 `sales_order.coupon_code` 位置 `sales_order.Customer's order number` = 1 |
| `Customer's group code` | 注册客户的组名称。 通过加入计算 `customer_entity.group_id` 到 `customer_group`.`customer_group_id` 并返回 `customer_group_code` 字段 |
| `Customer's lifetime number of coupons` | 应用于此客户所下所有订单的优惠券总数。 通过加入计算 `customer_entity.entity_id` 到 `sales_order.customer_id` 并计算订单数，其中 `sales_order.coupon_code` 不是 `NULL` |
| `Customer's lifetime number of orders` | 此客户下达的订单总数。 通过加入计算 `customer_entity.entity_id` 到 `sales_order.customer_id` 并计算 `sales_order` 表 |
| `Customer's lifetime revenue` | 此客户下达的所有订单的总收入。 通过加入计算 `customer_entity.entity_id` 到 `sales_order.customer_id` 并总结 `base_grand_total` 此客户下达的所有订单的字段 |
| `Seconds since customer's first order date` | 从客户的首次订购日期到现在之间的间隔时间。 通过减法计算 `Customer's first order date` 从执行查询时的服务器时间戳返回，以整数秒数形式返回 |
| `Store name` | 与此注册帐户关联的Commerce商店的名称。 通过加入计算 `customer_entity.store_id` 到 `store.store_id` 并返回 `name` 字段 |

{style="table-layout:auto"}

## 常用量度

| **量度名称** | **描述** | **构造** |
|---|---|---|
| `Avg first 30 day revenue` | 每个客户在客户首次订购后30天内下订单的平均收入 | 工序：平均<br/>操作数： `Customer's first 30 day revenue`<br/>时间戳： `created_at`<br/>过滤器：<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000（不包括自首次订购以来未满30天的客户） |
| `Avg lifetime coupons` | 每个客户在整个生命周期内应用于订单的平均优惠券数 | 工序：平均<br/>操作数： `Customer's lifetime number of coupons`<br/>时间戳： `created_at` |
| `Avg lifetime orders` | 每位客户在其生命周期内下达的平均订单数 | 工序：平均<br/>操作数： `Customer's lifetime number of orders`<br/>时间戳： `created_at` |
| `Avg lifetime revenue` | 所有订购在整个生命周期内每位客户的平均总收入 | 工序：平均<br/>操作数： `Customer's lifetime revenue`<br/>时间戳： `created_at` |
| `New customers` | 至少有一张订单的客户数，计算在其第一张订单的日期。 不包括注册但从未下订单的帐户 | 操作：计数<br/>操作数： `entity_id`<br/>时间戳： `Customer's first order date` |
| `Registered accounts` | 注册的帐户数。 包括所有已注册的帐户，无论该帐户是否下过订单 | 操作：计数<br/>操作数： `entity_id`<br/>时间戳： `created_at` |

{style="table-layout:auto"}

## 外键连接路径

`customer_group`

* 加入 `customer_group` 表，以创建返回已注册帐户的客户组名称的列。
   * 路径： `customer_entity.group_id` （许多） => `customer_group.customer_group_id` （一）

`store`

* 加入 `store` 表创建列，这些列返回与已注册帐户关联的商店相关的详细信息。
   * 路径： `customer_entity.store_id` （许多） => `store.store_id` （一）
