---
title: customer_entity表
description: 了解如何访问所有注册帐户的记录。
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# customer_entity表

的 `customer_entity` 表包含所有注册帐户的记录。 无论客户是否完成购买，如果注册了帐户，则会认为已注册该帐户。 每一行都对应一个唯一的注册帐户，该帐户由 `entity_id`.

此表不包含通过来宾结帐下单的客户记录。 如果您的商店接受来宾结帐， [了解如何进行帐户管理](../data-warehouse-mgr/guest-orders.md) 为那些顾客。

## 常用列

| **列名称** | **描述** |
|---|---|
| `created_at` | 与帐户注册日期对应的时间戳，通常以UTC在本地存储。 根据您在 [!DNL MBI]，此时间戳可能会转换为 [!DNL MBI] 与数据库时区不同 |
| `email` | 与帐户关联的电子邮件地址 |
| `entity_id` (PK) | 表的唯一标识符，通常用于与 `customer_id` 在实例中的其他表中 |
| `group_id` | 与关联的外键 `customer_group` 表。 加入 `customer_group.customer_group_id` 确定与注册帐户关联的客户组 |
| `store_id` | 与关联的外键 `store` 表。 加入 `store`.`store_id` 确定与注册帐户关联的商务商店视图 |

{style=&quot;table-layout:auto&quot;}

## 常用计算列

| **列名称** | **描述** |
|---|---|
| `Customer's first 30 day revenue` | 此客户在客户首次订购日期后30天内所下订单的总收入。 通过连接计算 `customer_entity.entity_id` to `sales_order.customer_id` 并求和 `base_grand_total` 字段，其中 `sales_order.Seconds between customer's first order date and this order` ≤ 2592000,30天内的秒数 |
| `Customer's first order date` | 此客户下单的第一个订单的时间戳。 通过连接计算 `customer_entity.entity_id` to `sales_order.customer_id` 并返回最低值 `sales_order`.`created_at` 值 |
| `Customer's first order's billing region` | 与客户首次订购关联的账单区域。 通过连接计算 `customer_entity.entity_id` to `sales_order.customer_id` 并返回 `Billing address region` where `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | 与客户首次订购关联的优惠券代码。 通过连接计算 `customer_entity.entity_id` to `sales_order.customer_id` 并返回 `sales_order.coupon_code` where `sales_order.Customer's order number` = 1 |
| `Customer's group code` | 注册客户的组名称。 通过连接计算 `customer_entity.group_id` to `customer_group`.`customer_group_id` 并返回 `customer_group_code` 字段 |
| `Customer's lifetime number of coupons` | 应用于此客户下达的所有订单的优惠券总数。 通过连接计算 `customer_entity.entity_id` to `sales_order.customer_id` 和计数 `sales_order.coupon_code` 不是 `NULL` |
| `Customer's lifetime number of orders` | 此客户下达的订单总数。 通过连接计算 `customer_entity.entity_id` to `sales_order.customer_id` 和计数 `sales_order` 表 |
| `Customer's lifetime revenue` | 此客户下达的所有订单的总收入。 通过连接计算 `customer_entity.entity_id` to `sales_order.customer_id` 并求和 `base_grand_total` 字段，表示此客户下达的所有订单 |
| `Seconds since customer's first order date` | 客户首次订购日期与现在之间经过的时间。 通过减法计算 `Customer's first order date` 从执行查询时的服务器时间戳返回，以整数秒为单位 |
| `Store name` | 与此注册帐户关联的商务商店的名称。 通过连接计算 `customer_entity.store_id` to `store.store_id` 并返回 `name` 字段 |

{style=&quot;table-layout:auto&quot;}

## 常用量度

| **量度名称** | **描述** | **建筑** |
|---|---|---|
| `Avg first 30 day revenue` | 在客户首次订购后30天内下达的订单的每位客户平均收入 | 操作：平均<br/>操作数： `Customer's first 30 day revenue`<br/>时间戳： `created_at`<br/>过滤器：<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000（不包括自首次订购以来未达到30天的客户） |
| `Avg lifetime coupons` | 每个客户在其生命周期内对订单应用的平均优惠券数 | 操作：平均<br/>操作数： `Customer's lifetime number of coupons`<br/>时间戳： `created_at` |
| `Avg lifetime orders` | 每个客户在其生命周期内下达的平均订单数 | 操作：平均<br/>操作数： `Customer's lifetime number of orders`<br/>时间戳： `created_at` |
| `Avg lifetime revenue` | 在其生命周期内下达的所有订单的每位客户的平均总收入 | 操作：平均<br/>操作数： `Customer's lifetime revenue`<br/>时间戳： `created_at` |
| `New customers` | 在首次订购日期计数的至少一次订购的客户数量。 不包括注册但从未下订单的帐户 | 操作：计数<br/>操作数： `entity_id`<br/>时间戳： `Customer's first order date` |
| `Registered accounts` | 注册的帐户数。 包括所有注册帐户，无论帐户是否下订单 | 操作：计数<br/>操作数： `entity_id`<br/>时间戳： `created_at` |

{style=&quot;table-layout:auto&quot;}

## 外键连接路径

`customer_group`

* 加入 `customer_group` 表格，以创建新列，以返回注册帐户的客户组名称。
   * 路径： `customer_entity.group_id` （多个）=> `customer_group.customer_group_id` (1)

`store`

* 加入 `store` 表格，以创建新列，返回与已注册帐户关联的存储相关的详细信息。
   * 路径： `customer_entity.store_id` （多个）=> `store.store_id` (1)
