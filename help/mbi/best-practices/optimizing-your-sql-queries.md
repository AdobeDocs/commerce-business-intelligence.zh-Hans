---
title: 优化SQL查询
description: 了解如何优化SQL查询。
exl-id: 2782c707-6a02-4e5d-bfbb-eff20659fbb2
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# 优化SQL查询

[!DNL SQL Report Builder]允许您在任何给定时间查询和迭代这些查询。 当需要修改查询而不必等待更新周期完成才实现您创建的列或报告需要更新时，这将很有用。

在执行查询之前，[[!DNL Commerce Intelligence] 估计其成本](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/sql-queries-explain-cost-errors.html)。 成本考虑执行查询所需的时间和资源数。 如果该成本过高，或者返回的行数超过[!DNL Commerce Intelligence]限制，则查询失败。 为了查询您的[Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md)（确保您编写的查询尽可能简化），Adobe建议执行以下操作。

## 使用SELECT或选择所有列

选择所有列并不能进行及时、易于执行的查询。 使用`SELECT *`的查询可能需要很长时间才能运行，尤其是在表具有许多列的情况下。

因此，Adobe建议您尽可能避免使用`SELECT *`，仅包括所需的列：

| **代替此……** | **尝试此操作！** |
|-----|-----|
| ![](../../mbi/assets/Select_all_1.png) | ![](../../mbi/assets/Select_all_2.png) |

{style="table-layout:auto"}

## 使用完全外连接

外连接选择所有要连接的两个表，这会增加查询的计算成本。 这意味着您的查询运行时间更长，并且更有可能失败，因为返回结果可能需要比执行限制更长的时间。

请考虑使用内部连接或左连接，而不使用这种类型的连接。 仅当表之间存在列匹配时（例如，典型`order_id`和`customers`表中都存在`orders`），内连接才会返回结果。 左连接会返回左表（第一个）中的所有结果以及右表（第二个）中的匹配结果。

查看如何重写FULL OUTER JOIN查询：

| **代替此……** | **尝试此操作！** |
|-----|-----|
| ![](../../mbi/assets/Full_Outer_Join_1.png) | ![](../../mbi/assets/Full_Outer_Join_2.png) |

{style="table-layout:auto"}

除了它们使用的JOIN类型外，这些查询在所有方面都是相同的。

## 使用多个联接

虽然您可以在查询中包含多个联接，但请记住，这可能会增加查询的开销。 为避免达到成本阈值，Adobe建议尽可能避免多个连接。

## 使用过滤器

尽量使用过滤器。 `WHERE`和`HAVING`子句将筛选您的结果，并仅提供您真正需要的数据。

## 在JOIN子句中使用筛选器

如果在执行连接时使用过滤器，请确保将其应用于连接中的两个表。 即使它是冗余的，也降低了查询的计算成本并减少了执行时间。

| **代替此……** | **尝试此操作！** |
|-----|-----|
| ![](../../mbi/assets/Join_filters_1.png) | ![](../../mbi/assets/Join_filters_2.png) |

{style="table-layout:auto"}

## 使用运算符

在编写查询时，请考虑使用尽可能便宜的运算符。 每个查询都有计算开销，计算开销由组成查询的函数、运算符和过滤器决定。 有些算子需要较少的计算量，因此与其他算子相比成本较低。

比较运算符（>、&lt;、=等）开销最小，其次是[LIKE。 SIMILAR TO和POSIX运算符](https://www.postgresql.org/docs/9.5/functions-matching.html)是最昂贵的运算符。

## 使用EXISTS与IN

使用`EXISTS`与`IN`取决于您尝试返回的结果类型。 如果您只对单个值感兴趣，请使用`EXISTS`子句而不是`IN`。 `IN`与逗号分隔值的列表一起使用，这会增加查询的计算成本。

运行`IN`查询时，系统必须首先处理子查询（`IN`语句），然后根据`IN`语句中指定的关系处理整个查询。 `EXISTS`效率更高，因为不必多次运行查询 — 检查查询中指定的关系时返回true/false值。

简单地说：使用`EXISTS`时，系统不必处理这么多的工作。

| **代替此……** | **尝试此操作！** |
|-----|-----|
| ![](../../mbi/assets/Exists_1.png) | ![](../../mbi/assets/Exists_2.png) |

{style="table-layout:auto"}

## 使用ORDER BY

`ORDER BY`在SQL中是一个昂贵的函数，它可能会显着增加查询的成本。 如果收到错误消息，指出查询的EXPLAIN成本过高，请尝试从查询中消除任何`ORDER BY`（除非有必要）。

这并不是说不能使用`ORDER BY`，只是说只能在必要时使用。

## 使用GROUP BY和ORDER BY

在少数情况下，此方法可能与您尝试执行的操作不符。 一般规则是，如果您使用`GROUP BY`和`ORDER BY`，则应将两个子句中的列放在相同的顺序中。 例如：

| **代替此……** | **尝试此操作！** |
|-----|-----|
| ![](../../mbi/assets/Group_by_2.png) | ![](../../mbi/assets/Group_by_1.png) |

{style="table-layout:auto"}

## 正在结束

学习编写SQL的最好方法（并且非常有效）是通过反复试验。 要找到最适合您的内容，请尝试仅使用SQL编辑器重新创建一些报告。
