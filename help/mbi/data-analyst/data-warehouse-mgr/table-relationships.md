---
title: 了解和评估表关系
description: 了解如何了解一个表格中可能出现的事件数量可能属于另一个表中的实体，反之亦然。
exl-id: e7256f46-879a-41da-9919-b700f2691013
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# 了解和评估表关系

在评估两个给定表之间的关系时，您需要了解一个表中可能出现的事件有多少属于另一个表中的实体，反之亦然。 例如，让我们使用 `users` 表和 `orders` 表。 在这种情况下，您想知道 **订购** 给予 **用户** 位置和可能的数量 **用户** an **订购** 可能属于。

了解关系对于维护数据完整性至关重要，因为它会影响您的 [计算列](../data-warehouse-mgr/creating-calculated-columns.md) 和 [维度](../data-warehouse-mgr/manage-data-dimensions-metrics.md). 要了解更多信息，请参阅 [关系类型](#types) 和 [如何评估Data warehouse中的表。](#eval)

## 关系类型 {#types}

两个表之间可以存在三种类型的关系：

* [“一对一”](#onetoone)
* [“一对多”](#onetomany)
* [“多对多”](#manytomany)

### `One-to-One` {#onetoone}

在 `one-to-one` 关系，表中的记录 `B` 在表中只属于一条记录 `A`. 和表格中的记录 `A` 在表中只属于一条记录 `B`.

例如，在人与驾照号之间的关系中，一个人只能拥有一个驾照号，而驾驶执照号属于一个人，而且只属于一个人。

![](../../assets/one-to-one.png)

### `One-to-Many` {#onetomany}

在 `one-to-many` 关系，表中的记录 `A` 可能属于表中的多个记录 `B`. 想想 `orders` 和 `items`  — 订单可以包含多个项目，但某个项目属于单个订单。 在本例中， `orders` 表格是单面， `items` 桌子是很多方面。

![](../../assets/one-to-many_001.png)

### `Many-to-Many` {#manytomany}

在 `many-to-many` 关系，表中的记录 `B` 可能属于表中的多个记录 `A`. 反之，表格中的记录 `A` 可能属于表中的多个记录 `B`.

想想 **产品** 和 **类别**:产品可以属于多个类别，而一个类别可以包含多个产品。

![](../../assets/many-to-many.png)

## 评估表 {#eval}

根据表之间存在的关系类型，您可以了解如何评估data warehouse中的表。 由于这些关系决定了多表计算列的定义方式，因此了解如何识别表关系和哪一方很重要 —  `one` 或 `many`  — 表属于。

可以使用两种方法来评估Data warehouse中给定一对表的关系。 第一种方法采用 [概念框架](#concept) 考虑表的实体如何彼此交互。 第二种方法利用 [表的模式](#schema).

### 使用概念框架 {#concept}

此方法使用概念框架来描述两个表中的实体如何能够相互交互。 必须理解，鉴于这种关系，这一框架评估了可能性。

例如，在考虑用户和订单时，会考虑关系中所有可能的内容。 注册用户在其生命周期内不能下订单、只能下单或下多个订单。 如果您刚刚启动了业务并且尚未下订单，则给定用户在其生命周期内仍可能会下许多订单，并且构建表以适应此情况。

要使用此方法，请执行以下操作：

1. 确定每个表中描述的实体。 **提示：通常是名词**. 例如， `user` 和 `orders` 表格明确描述了用户和订单。
1. 识别描述这些实体如何交互的动词。 例如，在比较用户和订单时，用户会“下”订单。 相反，订单“属于”用户。

此类框架可应用于Data warehouse中表的任意配对，从而使您能够轻松识别关系类型以及哪个表是一侧表和哪个表是多侧表。

确定描述两个表如何交互的术语后，考虑第一个实体的一个给定实例与第二个实例的关系，从而将交互框定为两个方向。 以下是每种关系的一些示例：

### `One-to-One`

一个指定人员只能有一个驾照号。 一个给定的驾驶执照号属于一个唯一的人。

这是 `one-to-one` 关系，其中每个表是一个侧。

![](../../assets/one-to-one3.png)

### `One-to-Many`

一个给定顺序可能包含许多项目。 一个给定项目只属于一个订单。

这是 `one-to-many` 其中，“订单”表为一侧，“项目”表为多侧。

![](../../assets/one-to-many3.png)

### `Many-to-Many`

一个给定的产品可能属于多个类别。 一个给定类别可能包含许多产品。

这是 `many-to-many` 关系，其中每个表是多边的。

![](../../assets/many-to-many3.png)

### 使用表的架构 {#schema}

第二种方法是利用表架构。 架构定义哪些列是 [`Primary`](http://en.wikipedia.org/wiki/Unique_key) 和 [`Foreign`](https://en.wikipedia.org/wiki/Foreign_key) 键。 您可以使用这些键将表链接在一起并帮助确定关系类型。

确定将两个表链接在一起的列后，使用列类型来评估表关系。 以下是一些示例：

### `One-to-one`

如果表使用 `primary key` ，则每个表中都描述了相同的唯一实体，并且关系是 `one-to-one`.

例如， `users` 表可以捕获大多数用户属性（如名称），而补充 `user_source` 表捕获用户注册源。 在每个表中，有一行表示一个用户。

![](../../assets/one-to-one1.png)

### `One-to-many`

>[!NOTE]
>
>你接受客人的命令吗？请参阅 [来宾订单](../data-warehouse-mgr/guest-orders.md) 以了解来宾订单如何影响您的表关系。

当使用 `Foreign key` 指向 `primary key`，此设置描述 `one-to-many` 关系。 一侧是包含 `primary key` 多边是包含 `foreign key`.

![](../../assets/one-to-many1.png)

### `Many-to-many`

如果以下任一情况为true，则关系为 `many-to-many`:

* `Non-primary key` 列用于链接两个表
   ![](../../assets/many-to-many1.png)
* 复合材料的一部分 `primary key` 用于链接两个表

![](../../assets/many-to-mnay2.png)

## 后续步骤

正确评估表关系对于准确建模数据至关重要。 现在，您已了解表如何彼此关联，请参阅 [使用Data warehouse管理器可以执行的操作](../data-warehouse-mgr/tour-dwm.md).
