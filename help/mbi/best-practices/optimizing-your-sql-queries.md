---
title: 优化SQL查询
description: 了解如何优化SQL查询。
exl-id: 2782c707-6a02-4e5d-bfbb-eff20659fbb2
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# 优化SQL查询

SQLReport Builder允许您在任何给定时间查询和迭代这些查询。 当您需要修改查询，而无需等待更新周期完成，然后再实现您创建的列或报表，则需要进行更新时，此功能非常有用。

在执行查询之前， [[!DNL MBI] 估计成本](https://support.magento.com/hc/en-us/articles/360016730391). 成本考虑执行查询所需的时间长度和资源数。 如果该成本被认为过高或返回的行数超过我们的限制，则不会运行查询。 我们为data warehouse添加了一个推荐列表，以便您查询，这将确保您编写尽可能简化的查询。

## 使用“选择”或“选择所有列”

选择所有列不能及时、轻松地执行查询。 使用的查询 `SELECT *` 运行可能需要相当长的时间，尤其是当您的表具有大量列时。

因此，我们建议您避免使用 `SELECT *` 尽可能地，并仅包含您需要的列：

| **不是这个……** | **试试这个！** |
|-----|-----|
| ![](../../mbi/assets/Select_all_1.png) | ![](../../mbi/assets/Select_all_2.png) |

{style=&quot;table-layout:auto&quot;}

## 使用完全外连接

外连接选择要连接的两个表的全部，这将增加查询的计算成本。 这意味着查询需要较长的时间才能运行，并且失败的可能性更大，因为返回结果可能需要超过执行限制的时间。

请考虑使用内部连接或左侧连接，而不是使用此类连接。 内部连接仅返回表之间存在柱状匹配的结果(例如， `order_id` 都存在于 `customers` 和 `orders` 表);左连接将返回左（第一个）表中的所有结果以及右（第二个）表中的匹配结果。

了解如何重写FULL OUTER JOIN查询：

| **不是这个……** | **试试这个！** |
|-----|-----|
| ![](../../mbi/assets/Full_Outer_Join_1.png) | ![](../../mbi/assets/Full_Outer_Join_2.png) |

{style=&quot;table-layout:auto&quot;}

如您所见，除了查询所使用的JOIN类型之外，这些查询在所有方面都是相同的。

## 使用多个连接

虽然您可以在查询中包含多个连接，但请记住，这可能会增加查询的成本。 为避免达到成本阈值，我们建议尽量避免多个连接。

## 使用过滤器

尽可能使用过滤器。 `WHERE` 和 `HAVING` 子句将过滤结果，并仅提供您真正需要的数据。

## 在JOIN子句中使用过滤器

如果在执行连接时使用过滤器，请确保将其应用于连接中的两个表。 即使它是冗余的，这也会降低查询的计算成本并加快执行时间。

| **不是这个……** | **试试这个！** |
|-----|-----|
| ![](../../mbi/assets/Join_filters_1.png) | ![](../../mbi/assets/Join_filters_2.png) |

{style=&quot;table-layout:auto&quot;}

## 使用运算符

在编写查询时，请考虑使用“最便宜”的运算符。 每个查询都有计算成本，计算成本取决于构成查询的函数、运算符和过滤器。 一些运算符需要的计算量较少，这使得它们比其他运算符的成本更低。

比较运算符（>、&lt;、=等）最便宜，其次是 [比如。 与和POSIX运算符相似](https://www.postgresql.org/docs/9.5/functions-matching.html) 最贵的运营商。

## 使用EXISTS与IN

使用 `EXISTS` 与 `IN` 取决于您尝试返回的结果类型。 如果您只对单个值感兴趣，请使用 `EXISTS` 子句而不是 `IN`. `IN` 与逗号分隔值列表结合使用，这将增加查询的计算成本。

When `IN` 查询运行后，系统必须首先处理子查询( `IN` 语句)，则整个查询将基于 `IN` 语句。 `EXISTS` 效率要高得多，因为查询不必多次运行 — 在检查查询中指定的关系时，会返回true/false值。

简单地说：使用 `EXISTS`.

| **不是这个……** | **试试这个！** |
|-----|-----|
| ![](../../mbi/assets/Exists_1.png) | ![](../../mbi/assets/Exists_2.png) |

{style=&quot;table-layout:auto&quot;}

## 使用顺序依据

`ORDER BY` 是SQL中一个昂贵的函数，可以显着提高查询的成本。 如果您收到一条错误消息，指出查询的EXPLAIN成本过高，请尝试消除任何 `ORDER BY`，除非绝对需要。

这不是说 `ORDER BY` 不能使用 — 只是需要时才应使用。

## 使用分组依据和排序依据

虽然在少数情况下，此方法与您尝试执行的操作不一致，但一般规则是，如果您使用 `GROUP BY` 和 `ORDER BY`，则应按相同的顺序放置两个子句中的列。 例如：

| **不是这个……** | **试试这个！** |
|-----|-----|
| ![](../../mbi/assets/Group_by_2.png) | ![](../../mbi/assets/Group_by_1.png) |

{style=&quot;table-layout:auto&quot;}

## 包装

学习编写SQL（并且高效执行）的最佳方法是通过试用和错误。 要查找最适合您的报表，请尝试仅使用SQL编辑器重新创建一些报表。
