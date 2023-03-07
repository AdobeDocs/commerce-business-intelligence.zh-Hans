---
title: 事件编号计算列
description: 了解事件编号计算列的用途和用法。
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 3%

---

# 事件编号计算列

本主题概述了 `Event Number` 中可用的计算列 **[!DNL Manage Data > Data Warehouse]** 页面。 下面是它的作用解释，然后是一个例子，以及创建它的机制。

**说明**

此 `Event Number` 列类型：标识特定事件发生的顺序 **事件所有者**，如 `customer` 或 `user`. 如果您熟悉SQL，则此列类型与 `RANK` 函数。 它可用于观察数据中首次事件、重复事件或n个事件之间的行为差异。

如果存在关联，则此列包含相同的 **排名** 对于已绑定的事件，将跳过后续编号。 例如，如果对数字5,8，10,10,12进行排序，则排名将为1,2，3,3，5。

本专栏最常见的使用案例是分析首次购买者和回头客。 首次通过添加过滤器（到指标或报表）来识别买家 `Customer's order number` = 1. `Customer's order number` 是类型的列 `Event Number`.

**示例**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

在上例中，列 `Owner's event number` 是 `Event Number` 列。 它会按照事件的发生顺序对所有者事件进行排名(根据 `timestamp` 列)。

例如，考虑所有行 `owner_id = A`. 表中的第一行是此所有者的最早时间戳，紧随其后的是表中的第三行，紧随其后的是表中的第四行。

**力学**

以下是关于创建 `Event Number` 列：

1. 导航到 **[!UICONTROL Manage Data > Data Warehouse]** 页面。
1. 导航到要在其上创建此列的表。
1. 单击 **[!UICONTROL Create a Column]** 并选择 `EVENT_NUMBER (…)` 列类型：在 `Same Table` 部分。
1. 第一个下拉列表 `Event Owner` 指定要确定其排名的实体。 如果是 `Customer's order number`，客户标识符，例如 `customer_id` 或 `customer_email` 将为 `Event Owner`.
1. 第二个下拉列表 `Event Rank` 指定强制实施用于确定行排名的序列的列。 如果是 `Customer's order number`，则 `created_at` 时间戳将为 `Event Rank`.
1. 在 `Options` 在下拉菜单中，您可以添加过滤器以排除不考虑的行。 排除的行具有 `NULL` 此列的值。
1. 为列提供一个名称，然后单击 **[!UICONTROL Save]**.
1. 列可供使用 _立即。_
