---
title: 计算列类型
description: 了解如何创建列以扩充和优化数据以供分析。
exl-id: 1af79b9e-77ff-4fc6-917a-4e6743b95035
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 0%

---

# 计算列类型

* [相同的表计算](#sametable)
* [一对多计算](#onetomany)
* [多对一计算](#manytoone)
* [方便的参考地图](#map)
* [高级计算列](#advanced)

在 [data warehouse管理器](../data-warehouse-mgr/tour-dwm.md)，您可以创建列来扩充和优化数据以供分析。 [此功能](../data-warehouse-mgr/creating-calculated-columns.md) 可以通过在Data warehouse管理器中选择任意表并单击 **[!UICONTROL Create New Column]**.

本主题介绍可以使用Data warehouse管理器创建的列类型。 它还涵盖了描述、该列的视觉演练和 [参考图](#map) 创建列所需的所有输入。 有三种方法可创建计算列：

1. [相同表计算列](#sametable)
1. [一对多计算列](#onetomany)
1. [多对一计算列](#manytoone)

## 相同表计算列 {#sametable}

这些列是使用同一表中的输入列生成的。

### 年龄 {#age}

年龄计算列返回当前时间与某个输入时间之间的秒数。

下面的示例创建 `Seconds since customer's most recent order` 在 `customers` 表格。 这可用于构建尚未在中进行购买（有时称为流失）的客户的用户列表 `X days`.

![](../../assets/age.gif)

### 货币转换器

货币转换器计算列将列的本机货币转换为所需的新货币。

下面的示例创建 `base\_grand\_total In AED`，转换 `base\_grand\_total` 从本币到AED的 `sales\_flat\_order` 表格。 此列非常适用于具有多种货币、希望以其本地货币进行报告的商店。

对于Commerce客户， `base\_currency\_code` 字段通常存储本地货币。 此 `Spot Time` 字段应匹配量度中使用的日期。

![](../../assets/currency_converter.png)

## 一对多计算列 {#onetomany}

`One-to-Many` 列 [使用两个表之间的路径](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md). 此路径始终表示一个表（属性所在的位置）和多个表（属性会向下重定位到）。 路径可以描述为 `foreign key--primary key` 关系。

### 联接列 {#joined}

联结列在一个表上重新定位属性 *到* 多张桌子。 一个/多个的典型示例是客户（一个）和订单（多个）。

在以下示例中， `Customer's group\_id` 维度向下联接到 `orders` 表格。

![](../../assets/joined_column.gif)

## 多对一计算列 {#manytoone}

这些列使用与一对多列相同的路径，但它们将数据指向相反方向。 列是在路径的一侧（而不是多侧）创建的。 由于这种关系，列中的值需要是一个聚合，即对许多端的数据点执行的数学运算。 这方面的用例很多，下面列出了一些用例。

### 计数 {#count}

此类型的计算列返回许多表中的值的计数 *onto* 一张桌子。

在以下示例中，维度 `Customer's lifetime number of canceled orders` 创建于 `customers` 表（带有过滤器） `orders.status`)。

![](../../assets/many_to_one.gif){： width=&quot;699&quot; height=&quot;351&quot;}

### 总和 {#sum}

“总和”计算列是 `many` 放在一张桌子上。

这可用于创建客户级别的维度，例如 `Customer's lifetime revenue`.

### 最小值或最大值 {#minmax}

最小值或最大值计算列返回多面存在的最小或最大记录。

这可用于创建客户级别的维度，例如 `Customer's first order date`.

### 存在 {#exists}

计算列是一种二进制测试，用于确定记录在多方面的存在。 换言之，新列返回 `1` 如果路径连接了每个表中的至少一行，并且 `0` 如果无法建立连接。

例如，此类型的维度可以确定客户是否购买过特定产品。 使用之间的联接 `customers` 表格和 `orders` 表格、特定产品的过滤器、维度 `Customer has purchased Product X?` 可以构建。

## 方便的参考地图 {#map}

如果在创建计算列时记住所有输入内容时遇到问题，请在构建时方便使用此参考图：

![](../../assets/merged_reference_map.png)

## 高级计算列 {#advanced}

在寻求分析和回答有关您业务的问题时，您可能会遇到无法构建所需确切列的情况。

为确保快速回转，Adobe建议查看 [高级计算列类型](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) 指南以了解该Adobe支持团队可以构建哪种类型的列。 该主题还涵盖了创建列所需的信息 — 将其包含在您的请求中。

## 相关文档

* [创建计算列](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [为计算列创建/删除路径](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [了解和评估表关系](../../data-analyst/data-warehouse-mgr/table-relationships.md)
