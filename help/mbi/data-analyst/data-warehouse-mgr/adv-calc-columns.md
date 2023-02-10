---
title: 高级计算列类型
description: 了解大多数使用列案例的基础知识 — 但您可能希望计算列比Data warehouse管理器可以创建的计算列更加复杂。
exl-id: 9871fa19-95b3-46e4-ae2d-bd7c524d12db
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 4%

---

# 高级计算列类型

您可能尝试创建的许多分析都涉及使用 **新列** 你想要的 `group by` 或 `filter by`. 的 [创建计算列](../data-warehouse-mgr/creating-calculated-columns.md) 本教程介绍了大多数用例的基础知识，但您可能希望计算列比Data warehouse管理器可以创建的计算列复杂得多。
{:#top}

这些类型的列可由我们的Data warehouse分析团队创建。 要定义新的计算列，请向我们提供以下信息：

1. 的 **`definition`** （包括输入、公式或格式）
1. 的 **`table`** 要在
1. 任意 **`example data points`** 描述列应包含的内容

以下是用户经常发现有用的一些高级计算列的常见示例：

* [按顺序排列（或排名）事件](#compareevents)
* [查找两个事件之间的时间](#twoevents)
* [比较顺序事件值](#sequence)
* [换算货币](#currency)
* [转换时区](#timezone)
* [其他内容](#else)

## 我试图按顺序排列事件 {#compareevents}

我们称之为 **事件数** 计算列。 这意味着我们正在尝试查找特定事件所有者（如客户或用户）发生事件的顺序。

示例如下：

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Owner's event number`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00:00:00 | 1 |
| 2 | `B` | 2015-01-01 00:30:00 | 1 |
| 3 | `A` | 2015-01-01 02:00:00 | 2 |
| 4 | `A` | 2015-01-02 13:00:00 | 3 |
| 5 | `B` | 2015-01-03 13:00:00 | 2 |

{style=&quot;table-layout:auto&quot;}

事件数计算列可用于观察数据中首次事件、重复事件或nth事件之间的行为差异。

想要查看客户的订单编号列是否在操作中？ 单击该图像可查看它在报表中用作分组依据维度的情况。

![使用事件编号计算列对按客户订单编号分组。](../../assets/EventNumber.gif)<!--{: style="max-width: 500px;"}-->

要创建此类型的计算列，我们需要知道：

* 要创建此列的表
* 用于标识事件所有者的字段(`owner\_id` 在此示例中)
* 要按哪个字段对事件进行排序(`timestamp` 在此示例中)

[返回页首](#top)

## 我在试图找到两件事之间的时间。 {#twoevents}

我们称之为 `date difference` 计算列。 这意味着我们正在尝试根据事件时间戳查找属于单个记录的两个事件之间的时间。

以下是一个示例：

| `id` | `timestamp\_1` | `timestamp\_2` | `Seconds between timestamp\_2 and timestamp\_1` |
|-----|-----|-----|-----|
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style=&quot;table-layout:auto&quot;}

日期差计算列可用于创建一个量度，用于计算两个事件之间的平均时间或中间时间。 单击下图可查看 `Average time to first order` 量度。

![使用日期差异计算列计算到第一顺序的平均时间。](../../assets/DateDifference.gif)<!--{: style="max-width: 500px;"}-->

要创建此类型的计算列，我们需要知道：

* 要创建此列的表
* 您想要了解两者区别的两个时间戳

[返回页首](#top)

## 我试图比较顺序事件值。 {#sequence}

我们称之为 **顺序事件比较**. 这意味着我们正在尝试查找值（货币、数字、时间戳）与所有者上一事件的相应值之间的增量。

示例如下：

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00:00:00 | NULL |
| 2 | `B` | 2015-01-01 00:30:00 | NULL |
| 3 | `A` | 2015-01-01 02:00:00 | 7720 |
| 4 | `A` | 2015-01-02 13:00:00 | 126000 |
| 5 | `B` | 2015-01-03 13:00:00 | 217800 |

{style=&quot;table-layout:auto&quot;}

顺序事件比较可用于查找每个顺序事件之间的平均时间或中值时间。 单击下图可查看 **订单间的平均时间和中间时间** 量度的实际操作情况。

=![使用顺序事件比较计算列来计算订单之间的平均时间和中间时间。](../../assets/SeqEventComp.gif)<!--{: style="max-width: 500px;"}-->

要创建此类型的计算列，我们需要知道：

* 要创建此列的表
* 用于标识事件所有者的字段(`owner\_id` )
* 要查看每个顺序事件之间差异的值字段(`timestamp` 在此示例中)

[返回页首](#top)

## 我试图兑换货币。 {#currency}

A **货币兑换** “计算”列根据事件时的汇率，将交易金额从记录的货币换算为报告货币。

示例如下：

| **`id`** | **`timestamp`** | **`transaction\_value\_EUR`** | **`transaction\_value\_USD`** |
|-----|-----|-----|-----|
| `1` | 2015-01-01 00:00:00 | 30 | 33.57 |
| `2` | 2015-01-02 00:00:00 | 50 | 55.93 |

{style=&quot;table-layout:auto&quot;}

要创建此类型的计算列，我们需要知道：

* 要创建此列的表
* 要转换的交易金额列
* 指示数据记录所用货币的列（通常为ISO代码）
* 首选报告货币

[返回页首](#top)

## 我正在尝试转换时区。 {#timezone}

A **时区转换** “计算”列将特定数据源的时间戳从其记录的时区转换为报表时区。

示例如下：

| **`id`** | **`timestamp\_UTC`** | **`timestamp\_ET`** |
|-----|-----|-----|
| `1` | 2015-01-01 00:00:00 | 2014-12-31 19:00:00 |
| `2` | 2015-01-01 12:00:00 | 2015-01-01 07:00:00 |

{style=&quot;table-layout:auto&quot;}

要创建此类型的计算列，我们需要知道：

* 要创建此列的表
* 要转换的时间戳列
* 记录数据的时区
* 首选报表时区

[返回页首](#top)

## 我想做一些不在这的事。 {#else}

别担心。 这里没有列出它，并不意味着它不可能。 我们的Data warehouse分析员团队已经为您提供了帮助。

要定义新的计算列，请 [提交支持票证](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) 包含您想要构建的内容的详细信息。

## 相关文档

* [创建计算列](../data-warehouse-mgr/creating-calculated-columns.md)
* [计算列类型](../data-warehouse-mgr/calc-column-types.md)
* [建筑 [!DNL Google ECommerce] 包含订单和客户数据的维度](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
