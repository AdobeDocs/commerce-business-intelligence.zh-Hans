---
title: 顺序比较计算列
description: 了解“顺序比较”计算列的用途和用法。
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 2433a614e9858684842804a0ae29fb67f0d41ead
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# 顺序比较计算列

本主题概述了&#x200B;**[!DNL Manage Data > Data Warehouse]**&#x200B;页面中可用的`Sequential Comparison`计算列的用途和用途。 下面是它的作用解释，然后是一个示例以及创建它的机制。

**解释**

`Sequential Comparison`列类型：查找连续事件之间的差异。 最常见的`Sequential Comparison`列类型是`Seconds since previous order`列。 此列需要三个输入：

1. `Event Owner`：此输入确定行分组所在的实体。 例如，在`Seconds since previous order`列中，事件所有者是客户，因为您希望查找自同一客户的上次订购以来的秒数。
1. `Event Date`：此输入强制事件序列。 在`Seconds since previous order`的情况下，包含订单时间戳的列应为`Event Date`。 此输入始终为时间戳。
1. `Value to Compare`：此输入是要比较的实际值。 它从当前行的值中减去前一行的值。 因此，查找客户连续订单之间时间差的列称为`Seconds since previous order`。 此输入不必为时间戳。 非时间戳示例用于查找客户的连续订单之间的订单值差异。

**示例**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 2015-01-01 00:00:00 | NULL |
| **`2`** | B | 2015-01-01 00:30:00 | NULL |
| **`3`** | A | 2015-01-01 02:00:00 | 7200 |
| **`4`** | A | 2015-01-02 13:00:00 | 126000 |
| **`5`** | B | 2015-01-03 13:00:00 | 217800 |

在上例中，`Seconds since owner's previous event`是`Sequential Comparison`计算列。 对于`owner_id = A`，它首先基于`timestamp`列标识一个序列，然后从当前事件的时间戳中减去上一个事件的`timestamp`。 在表的第三行 — `owner_id A`的第二行 — `Seconds since owner's previous event`的值是&#39;2015-01-01 02:00&#39;和&#39;2015-01-01 00:00:00&#39;之间的秒数。 这一差等于两小时= 7200秒。

对于此计算列类型，对应于所有者第一个事件的行具有`NULL`值。

**机械**

要创建&#x200B;**事件编号**&#x200B;列，请执行以下操作：

1. 导航到&#x200B;**[!DNL Manage Data > Data Warehouse]**&#x200B;页面。

1. 导航到要在其上创建此列的表。

1. 单击右上角的&#x200B;**[!UICONTROL Create New Column]**。

1. 选择`Same Table`作为`Definition Type`（如果要比较的列不在同一个表中，您可能需要重新定位它们）。

1. 选择`SEQUENTIAL_COMPARISON`作为`Column Definition Equation`。

1. 选择输入值，如上文所述：
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`

1. 还可以添加过滤器以排除不考虑的行。 排除的行具有此列的`NULL`值。

1. 为页面顶部的列提供一个名称，然后单击&#x200B;**[!UICONTROL Save]**。

1. 该列可立即使用&#x200B;*1}。*

![秒](../../assets/SEC_new.png)
