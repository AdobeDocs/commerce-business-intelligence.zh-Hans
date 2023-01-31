---
title: 计算列类型
description: 了解如何创建列以扩充和优化数据以进行分析。
exl-id: 1af79b9e-77ff-4fc6-917a-4e6743b95035
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 0%

---

# 计算列类型

* [相同的表计算](#sametable)
* [一对多计算](#onetomany)
* [多对一计算](#manytoone)
* [方便的参考图](#map)
* [高级计算列](#advanced)

在 [data warehouse管理器](../data-warehouse-mgr/tour-dwm.md)，您便能够创建列以扩充和优化数据以供分析。 [此功能](../data-warehouse-mgr/creating-calculated-columns.md) 可通过选择“Data warehouse管理器”中的任意表并单击 **[!UICONTROL Create New Column]**.

本文介绍了可通过Data warehouse管理器创建的列类型，以及该列的描述、可视演示以及 [参考图](#map) 创建列所需的所有输入。 有三种方法可创建计算列：

* [相同的表计算列](#sametable)
* [一对多计算列](#onetomany)
* [多对一计算列](#manytoone)

## 相同的表计算列 {#sametable}

这些列是使用同一表中的输入列构建的。

### 年龄 {#age}

年龄计算列返回当前时间与某些输入时间之间的秒数。

在以下示例中，我们创建了 `Seconds since customer's most recent order` 在 `customers` 表。 利用此功能，可构建用户列表，其中列出了未在 `X days`.

![](../../assets/age.gif)

### 货币转换器

货币转换器计算列将列的本机货币转换为所需的新货币。

在以下示例中，我们创建了 `base\_grand\_total In AED`，转换 `base\_grand\_total` 从本币到AED(在 `sales\_flat\_order` 表。 此列非常适用于具有多个要报告其当地货币的货币的商店。

对于商务客户， `base\_currency\_code` 字段通常存储本地货币。 的 `Spot Time` 字段应与量度中使用的日期匹配。

![](../../assets/currency_converter.png)

## 一对多计算列 {#onetomany}

`One-to-Many` 列 [利用两个表之间的路径](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md). 此路径始终包含一个表（属性位于其中）和许多表（该属性将“重新定位”到中）。 路径可以描述为 `foreign key--primary key` 关系。

### 联接列 {#joined}

连接列在一个表中重新定位属性 *to* 很多桌子。 一个/多的典型示例是客户（一个）和订单（多个）。

在以下示例中， `Customer's group\_id` 维度会向下联接到 `orders` 表。

![](../../assets/joined_column.gif)

## 多对一计算列 {#manytoone}

这些列使用的路径与一对多列的路径相同，但它们将数据指向相反的方向。 在路径的一侧创建列，而不是在多侧创建列。 由于这种关系，列中的值需要是聚合，即对数据点在多边执行的数学运算。 此功能有许多用例，下面列出了一些用例。

### 计数 {#count}

此类型的计算列返回许多表中的值计数 *onto* 一张桌子。

在以下示例中，维度 `Customer's lifetime number of canceled orders` 创建于 `customers` 表格(带过滤器 `orders.status`)。

![](../../assets/many_to_one.gif){:width=&quot;699&quot; height=&quot;351&quot;}

### 总和 {#sum}

“求和”计算列是 `many` 一张桌子上。

这可用于创建客户级别的维度，例如 `Customer's lifetime revenue`.

### 最小或最大 {#minmax}

最小或最大计算列返回多边存在的最小或最大记录。

这可用于创建客户级别的维度，例如 `Customer's first order date`.

### 存在 {#exists}

存在的计算列是一个二进制测试，用于确定记录在多边的存在。 换言之，新列将返回 `1` 如果路径连接每个表中的至少一行，则 `0` 如果无法建立连接。

此类型的维度可能会确定，例如，客户是否购买过特定产品。 在 `customers` 表格和 `orders` 表，特定产品的过滤器，维度 `Customer has purchased Product X?` 可以构建。

## 方便的参考图 {#map}

如果您在创建计算列时记住所有输入内容时遇到问题，请在构建时尽量保持此参考映射方便：

![](../../assets/merged_reference_map.png)

## 高级计算列 {#advanced}

在分析和回答有关您业务的问题时，您可能会遇到无法构建所需的确切列的情况。 在这些情况下，我们掩护你！

为确保快速周转，我们建议查看 [高级计算列类型](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) 指南，以了解我们的支持团队可以构建哪种类型的列。 在该文章中，我们还将介绍创建列所需的信息 — 请将其包含在您的请求中。

## 相关文档

* [创建计算列](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [为计算列创建/删除路径](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [了解和评估表关系](../../data-analyst/data-warehouse-mgr/table-relationships.md)
