---
title: 顺序比较计算列
description: 了解“顺序比较”计算列的用途和用法。
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 2%

---

# 顺序比较计算列

本主题概述了 `Sequential Comparison` 中可用的计算列 **[!DNL Manage Data > Data Warehouse]** 页面。 下面是它的作用解释，然后是一个示例以及创建它的机制。

**说明**

此 `Sequential Comparison` 列类型：查找连续事件之间的差异。 最常见的类型 `Sequential Comparison` 列是 `Seconds since previous order` 列。 此列需要三个输入：

1. `Event Owner`：此输入确定行要分组的实体。 例如，在 `Seconds since previous order` 列，则事件责任人是客户，因为您要查找自同一客户的上次订购以来的秒数。
1. `Event Date`：此输入强制执行事件的序列。 在下列情况下 `Seconds since previous order`，包含订单时间戳的列应为 `Event Date`. 此输入始终为时间戳。
1. `Value to Compare`：此输入是要比较的实际值。 它会从当前行的值中减去前一行的值。 因此，将调用一列来查找客户的连续订单之间的时间差 `Seconds since previous order`. 此输入不必为时间戳。 非时间戳示例用于查找客户的连续订单之间的订单值差异。

**示例**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 2015-01-01 00:00:00 | 空 |
| **`2`** | B | 2015-01-01 00:30:00 | 空 |
| **`3`** | A | 2015-01-01 02:00:00 | 7200 |
| **`4`** | A | 2015-01-02 13:00:00 | 126000 |
| **`5`** | B | 2015-01-03 13:00:00 | 217800 |

在上例中， `Seconds since owner's previous event` 是 `Sequential Comparison` 计算列。 对于 `owner_id = A`，首先根据序列的 `timestamp` 列，然后减去上一个事件的 `timestamp` 从当前事件的时间戳开始计算。 在表的第三行 — 的第二行 `owner_id A`  — 的值 `Seconds since owner's previous event` 是“2015-01-01 02:00”到“2015-01-01 00”之间的秒数:00:00&#39;。 这一差异等于两个小时= 7200秒。

对于此计算列类型，与拥有者的第一个事件对应的行具有 `NULL` 值。

**力学**

创建 **事件编号** 列：

1. 导航到 **[!DNL Manage Data > Data Warehouse]** 页面。

1. 导航到要在其上创建此列的表。

1. 单击 **[!UICONTROL Create New Column]** 在右上角。

1. 选择 `Same Table` 作为 `Definition Type` （如果要比较的列不在同一个表中，可能需要重新定位它们）。

1. 选择 `SEQUENTIAL_COMPARISON` 作为 `Column Definition Equation`.

1. 选择输入数据，如上文所述：
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`

1. 还可以添加过滤器以排除不考虑的行。 排除的行具有 `NULL` 此列的值。

1. 在页面顶部提供列的名称，然后单击 **[!UICONTROL Save]**.

1. 列可供使用 *立即*.

![秒](../../assets/SEC_new.png)
