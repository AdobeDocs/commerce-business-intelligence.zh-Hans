---
title: 事件编号计算列
description: 了解事件数计算列的用途和用途。
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# 事件编号计算列

本主题概述 `Event Number` 计算列在 **[!DNL Manage Data > Data Warehouse]** 页面。 下面是其功能的说明，后面是一个示例，以及创建该功能的机制。

**说明**

的 `Event Number` 列类型：标识特定事件发生的顺序 **事件所有者**，如 `customer` 或 `user`. 如果您熟悉SQL，则此列类型与 `RANK` 函数。 它可用于观察数据中首次事件、重复事件或nth事件之间的行为差异。

如果是关系，则此列包含相同的 **排名** ，并跳过后续的数字。 例如，如果对数字5,8,10,10,12进行排名，则排名为1,2,3,3,5。

本专栏最常见的用例是分析首次购买者和重复购买者。 首次通过在 `Customer's order number` = 1 `Customer's order number` 是类型的列 `Event Number`.

**示例**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

在上例中，列 `Owner's event number` 是 `Event Number` 列。 它会按事件发生的顺序(根据 `timestamp` 列)。

例如，请考虑 `owner_id = A`. 表中的第一行是此所有者的最早时间戳，后跟表中的第三行，后跟表中的第四行。

**力学**

以下是有关创建 `Event Number` 列：

1. 导航到 **[!UICONTROL Manage Data > Data Warehouse]** 页面。
1. 导航到要创建此列的表。
1. 单击 **[!UICONTROL Create a Column]** 然后选择 `EVENT_NUMBER (…)` 列类型：下 `Same Table` 中。
1. 第一个下拉菜单 `Event Owner` 指定要确定其排名的实体。 对于 `Customer's order number`，客户标识符，例如 `customer_id` 或 `customer_email` 会是 `Event Owner`.
1. 第二个下拉列表 `Event Rank` 指定强制执行确定行排名的序列的列。 对于 `Customer's order number`, `created_at` 时间戳为 `Event Rank`.
1. 在 `Options` 下拉列表中，您可以添加过滤器以排除考虑的行。 排除的行将具有 `NULL` 值。
1. 为列提供名称，然后单击 **[!UICONTROL Save]**.
1. 列将可供使用 _立即。_
