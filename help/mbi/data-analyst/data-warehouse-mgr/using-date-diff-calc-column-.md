---
title: 使用“日期差异”计算列
description: 了解“日期差异”计算列的用途和用途。
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 2%

---

# 日期差异计算列

本主题概述 `Date Difference` 计算列在 **[!DNL Manage Data > Data Warehouse]** 页面。 下面是其功能的说明，后面是一个示例，以及创建该功能的机制。

**说明**

的 `Date Difference` 列类型：根据事件时间戳，查找属于单个记录的两个事件之间的时间。 此列中计算的原始值以秒为单位，但会自动转换为分钟、小时、天等，以便在报表中显示。 但是，当用作过滤器/组时，您将需要以秒为单位使用该值。

A `date difference` “计算”列可用于创建一个量度，用于计算两个事件之间的平均时间或中间时间，例如客户注册与其首次订购之间的平均时间。

**示例**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style=&quot;table-layout:auto&quot;}


在上例中， `Date Difference` 列是 `Seconds between timestamp_2 and timestamp_1` 列。 它执行计算 `timestamp_2 minus timestamp_1`.

**力学**

以下步骤描述如何创建 `Date Difference` 列。

1. 导航到 **[!DNL Manage Data > Data Warehouse]** 页面。
1. 导航到要创建此列的表。
1. 单击 **[!UICONTROL Create a Column]** 并按如下方式配置列：
   * 选择 `Column Definition Type` > `Same Table`
   * 选择 `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * 选择 `Ending DATETIME` column >选择结束日期时间字段，该字段通常是稍后发生的事件
   * 选择 `Starting DATETIME` column** >选择开始日期时间字段，该字段通常是之前发生的事件

1. 为列提供名称，然后单击 **[!UICONTROL Save]**.
1. 列将可供使用 *立即*.

例如，以下示例配置为计算 `Seconds between order date and customer's creation date`:

![](../../assets/date_diff.png)
