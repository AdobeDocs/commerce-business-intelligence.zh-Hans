---
title: 事件编号计算列
description: 了解事件编号计算列的用途和用法。
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# 事件编号计算列

本主题概述了&#x200B;**[!DNL Manage Data > Data Warehouse]**&#x200B;页面中可用的`Event Number`计算列的用途和用途。 下面是它的作用解释，然后是一个示例，以及创建它的机制。

**解释**

`Event Number`列类型标识特定&#x200B;**事件所有者**（如`customer`或`user`）发生事件的顺序。 如果您熟悉SQL，则此列类型与`RANK`函数相同。 它可用于观察数据中首次事件、重复事件或第n个事件之间的行为差异。

如果存在关联，则此列包含与关联事件相同的&#x200B;**排名**，并跳过后续的数字。 例如，如果对数字5,8，10,10,12进行排序，则排名将为1,2，3,3，5。

本专栏最常见的使用案例是分析首次购买者和重复购买者。 首次通过在`Customer's order number` = 1上添加过滤器（到量度或报表）来识别购买者。 `Customer's order number`是`Event Number`类型的列。

**示例**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

在上述示例中，列`Owner's event number`是`Event Number`列。 它根据所有者事件的发生顺序（基于`timestamp`列）对所有者事件进行排名。

例如，考虑`owner_id = A`的所有行。 表中的第一行是此所有者的最早时间戳，紧随其后的是表中的第三行，紧随其后的是表中的第四行。

**机械**

以下是有关创建`Event Number`列的一些说明：

1. 导航到&#x200B;**[!UICONTROL Manage Data > Data Warehouse]**&#x200B;页面。

1. 导航到要在其上创建此列的表。

1. 单击&#x200B;**[!UICONTROL Create a Column]**&#x200B;并选择`Same Table`部分下的`EVENT_NUMBER (…)`列类型。

1. 第一个下拉列表`Event Owner`指定要确定其排名的实体。 在`Customer's order number`的情况下，客户标识符（如`customer_id`或`customer_email`）将是`Event Owner`。

1. 第二个下拉列表`Event Rank`指定强制执行确定行排名的序列的列。 在`Customer's order number`的情况下，`created_at`时间戳将为`Event Rank`。

1. 在`Options`下拉列表下，您可以添加过滤器以排除不考虑的行。 排除的行具有此列的`NULL`值。

1. 提供列的名称并单击&#x200B;**[!UICONTROL Save]**。

1. 该列可以立即使用&#x200B;_。_
