---
title: 为计算列创建或删除路径
description: 了解如何定义一个路径，以描述您在上创建列的表如何与您从中提取信息的表相关。
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# 为计算列创建或删除路径

## 计算列刷新器

When [创建计算列](../data-warehouse-mgr/creating-calculated-columns.md) 在您的Data warehouse中，将要求您定义一个路径，以描述您在上创建列的表如何与您从中提取信息的表相关。 要成功创建路径，您需要了解两件事：

1. 数据库中的表如何彼此关联
1. 定义此关系的主键和外键

如果您知道此信息，将能够按照本文中的说明轻松创建路径。 如果您有点不确定，我们提供了这些概念的概述，但您可能希望咨询贵组织的技术专家或联系我们的支持团队。

## 刷新表关系和键类型 {#refresher}

### 表关系 {#relationships}

我们在 [了解和评估表关系文章](../../data-analyst/data-warehouse-mgr/table-relationships.md)但简短的总结从不伤害任何人，对吧？

表可通过以下三种方式之一相互关联：

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | 人与驾照号的关系。 一个人只能拥有一个驾照号，一个驾照号属于一个人。 |
| **`one-to-many`** | 订单与项目之间的关系 — 订单可以包含许多项目，但项目属于单个订单。 在这种情况下，订单表是一侧，项目表是多侧。 |
| **`many-to-many`** | 产品与类别之间的关系：产品可以属于多个类别，而一个类别可以包含多个产品。 |

{style=&quot;table-layout:auto&quot;}

了解两个表之间的关系后，即可使用该关系来确定应创建什么路径来将信息从一个表引到另一个表。 下一步需要了解有助于建立表关系的主键和外键。

### 主键和外键 {#keys}

A `Primary Key` 是一个不改变的列或一组在表中生成唯一值的列。 例如，当客户在网站上下订单时，会在 `orders` 购物车中的表格，新 `order_id`. 此 `order_id` 允许客户和企业跟踪特定订单的进度。 由于订单ID是唯一的，因此它通常是 `Primary Key` a `orders` 表。

A `Foreign Key` 是在链接到 `Primary Key` 列。 外键可在表之间创建引用，使分析人员能够轻松查找记录并将记录链接在一起。 假设我们想知道哪些订单属于我们的每位客户。 的 `customer id` 列(`Primary Key` 的 `customers` 表)和 `order_id` 列(`Foreign Key` 在 `customers` 表，引用 `Primary Key` 的 `orders` 表)，以便我们链接和分析此信息。 创建路径时，将要求您定义 `Primary Key` 和 `Foreign Key`.

## 创建路径 {#createpath}

在data warehouse中创建列时，您需要定义将信息从一个表引入另一个表的路径。 有时，由于表之间已存在路径，因此会预填充路径，但如果没有预填充路径，则需要创建一个路径。

我们利用 **客户** 和 **订购** 来向你展示它是如何完成的。 划分：

* 这种关系 `one-to-many`  — 客户可以拥有多个订单，但订单只能拥有一个客户。 这可告知我们关系的方向或应创建计算列的位置。 在这种情况下，它表示 `orders` 可以将表格放入 `customers` 表。
* 的 `primary key` 我们想用的是 `customers.customerid`，或 `customer ID` 列 `customers` 表。
* 的 `foreign key` 我们想用的是 `orders.customerid`，或 `customer ID` 列 `orders` 表。

现在，我们带你们走完这条道路。

1. 单击 **[!UICONTROL Data > Data Warehouse]**.
1. 在表列表中，单击要在中创建列的表。 在本例中，它是 `customers` 表。
1. 将显示表模式。 单击 **[!UICONTROL Create New Column]**.
1. 为列指定名称 — 例如， `Customer's orders`.
1. 选择列的定义。 查看 [Calculated Column Guide](../data-warehouse-mgr/creating-calculated-columns.md) 一张方便的备忘录。
1. 在 [!UICONTROL Select table and column] 下拉菜单，单击 **[!UICONTROL Create new path]** 选项。

   ![为计算列模式窗口创建路径](../../assets/Creating_Paths_modal.png)

1. 使用下拉列表，为每个表选择主键和外键。

   在 `Many` 侧，我们选择 `orders.customerid`  — 请记住，客户可能有许多订单。

   在 `One` 侧，我们选择 `customers.customerid`  — 订单只能有一个客户。

1. 单击 **[!UICONTROL Save]** 以保存路径并完成列的创建。

### 创建路径的限制 {#limits}

* **[!DNL MBI]无法猜测主键/外键关系**. 我们不希望在您的帐户中引入错误的数据，因此必须手动创建路径。
* **目前，只能在两个不同的表之间指定路径**. 您尝试重新创建的逻辑是否涉及两个以上的表？ 然后，(1)先将列加入中间表格，然后进入“最终目的地”表格，或(2)与我们的团队协商，以找到实现您目标的最佳方法，这可能会有意义。
* **列一次只能是ONE路径的外键引用**. 例如，如果 `order_items.order_id` 指向 `orders.id`，则 `order_items.order_id` 不能指向其他任何内容。
* **`Many-to-many`路径可以在技术上创建，但通常会产生错误数据，因为两者都不是真的 `one-to-many` 外键**. 接近这些路径的最佳方式始终取决于特定的所需分析。 请咨询RJ分析团队，了解最佳解决方案。

如果由于上述一个或多个限制而阻止您创建计算列，请联系支持人员以提供您所在列的说明

## 删除计算列路径 {#delete}

在您的Data warehouse中创建了错误路径？ 或者你在做春洗，想收拾一下？ 如果需要从帐户中删除路径，您可以 [向我们的支持分析人员发送票证](../../guide-overview.md). **确保包含路径的名称！**

## 包装 {#wrapup}

现在，您应该可以轻松地在Data warehouse中为计算列创建路径。 如果您仍不确定特定路径，请记住，您始终可以单击 **[!UICONTROL Support]** 在 [!DNL MBI] 帐户以获取帮助。

## 相关

* [了解和评估表关系](../data-warehouse-mgr/table-relationships.md)
* [为计算列创建路径](../data-warehouse-mgr/create-paths-calc-columns.md)
* [计算列类型](../data-warehouse-mgr/calc-column-types.md) 尝试创建。
