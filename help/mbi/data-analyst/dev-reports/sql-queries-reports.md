---
title: 将SQL查询转换为 [!DNL MBI] 报告
description: 了解SQL查询如何转换为您在 [!DNL MBI].
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 0%

---

# 在MBI中转换SQL查询

曾想知道SQL查询如何转换为 [计算列](../data-warehouse-mgr/creating-calculated-columns.md), [量度](../../data-user/reports/ess-manage-data-metrics.md)和 [报告](../../tutorials/using-visual-report-builder.md) 在 [!DNL MBI]？如果您是一个庞大的SQL用户，请了解SQL在中的转换方式 [!DNL MBI] 将使您在 [data warehouse管理器](../data-warehouse-mgr/tour-dwm.md) 从 [!DNL MBI] 平台。

在本文的末尾，我们提供了 **翻译矩阵** 用于SQL查询子句和 [!DNL MBI] 元素。

我们首先查看一个一般查询：

|  |  |
|--- |--- |
| `SELECT` |  |
| `a,` | 报表 `group by` |
| `SUM(b)` | `Aggregate function` (column) |
| `FROM c` | `Source` 表 |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | 报表 `time frame` |
| `GROUP BY a` | 报表 `group by` |

此示例涵盖大多数翻译案例，但也有一些例外。 让我们深入研究，从 `aggregate` 函数。

## 聚合函数

聚合函数(例如， `count`, `sum`, `average`, `max`, `min`)，可采用 **量度聚合** 或 **列聚合** in [!DNL MBI]. 区分因素是是否需要连接来执行聚合。

让我们看一下上述每个示例。

## 量度聚合 {#aggregate}

聚合时需要使用量度 `within a single table`. 例如， `SUM(b)` 上述查询中的聚合函数极有可能由对列求和的量度表示 `B`. 

让我们看一下 `Total Revenue` 量度可在 [!DNL MBI]. 请查看下面的查询，我们将尝试翻译该查询：

|  |  |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` (column) |
| `FROM orders` | `Metric source` 表 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 量度 `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | 量度 `timestamp` （和报告） `time range`) |

通过单击 **[!UICONTROL Manage Data** > **&#x200B;量度&#x200B;**> **新建量度]**，则必须首先选择适当的 `source` 表，在本例中为 `orders` 表。 然后，将设置量度，如下所示：

![量度聚合](../../assets/Metric_aggregation.png)

## 列聚合

从另一个表中合并的列聚合时，需要计算列。 例如，您可能在 `customer` 表已调用 `Customer LTV`，用于计算与该客户关联的所有订单在 `orders` 表。

此聚合的查询可能如下所示：

|  |  |
|--- |--- |
| `Select` |  |
| `c.customer_id` | 总所有者 |
| `SUM(o.order_total) as "Customer LTV"` | 聚合运算（列） |
| `FROM customers c` | 聚合所有者表 |
| `JOIN orders o` | 聚合源表 |
| `ON c.customer_id = o.customer_id` | 路径 |
| `WHERE o.status = 'success'` | 聚合过滤器 |

在 [!DNL MBI] 需要使用Data warehouse管理器，以便在 `orders` 和 `customers` 然后，创建名为 `Customer LTV` 在客户的桌子上。

让我们首先看一看如何在 `customers` 和 `orders`. 我们的最终目标是在 `customers` 表，因此首先导航到 `customers` 表格，然后单击 **[!UICONTROL Create a Column** > **&#x200B;选择定义&#x200B;**> **SUM]**.

接下来，您需要选择源表。 如果 `orders` 表格，只需从下拉菜单中选择它即可。 但是，如果要构建新路径，请单击 **[!UICONTROL Create new path]** 此时，您将看到以下屏幕：

![创建新路径](../../assets/Create_new_path.png)

在此，您需要仔细考虑要连接在一起的两个表之间的关系。 在这种情况下，可能 `Many` 与 `One` 客户，因此 `orders` 表列于 `Many` 侧，而 `customers` 在 `One` 侧。

>[!NOTE]
>
>在 [!DNL MBI], a *路径* 等同于 `Join` 在SQL中。

保存路径后，所有人都将设置为创建新路径 `Customer LTV` 柱子！ 请查看以下内容：

![](../../assets/Customer_LTV.gif)

现在你已经建了 `Customer LTV` 列 `customers` 表格，您可以创建 [量度聚合](#aggregate) 使用此列（例如，查找每位客户的平均LTV），或者 `group by` 或 `filter` 按报表中的计算列(使用 `customers` 表。

>[!NOTE]
>
>对于后者，每当您构建新的计算列时，都需要 [将维度添加到现有量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 之前，它将作为 `filter` 或 `group by`.

请参阅 [创建计算列](../data-warehouse-mgr/creating-calculated-columns.md) data warehouse管理器。

## `Group By` 子句

`Group By` 查询中的函数通常表示在 [!DNL MBI] 作为用于划分或过滤可视化报表的列。 例如，让我们重新访问 `Total Revenue` 查询，但此次让我们按 `coupon\_code` 以更好地了解哪些优惠券能产生最大收入。

首先，我们从以下查询开始：

|  |  |
|--- |--- |
| `SELECT coupon_code,` | 报表 `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`(column) |
| `FROM orders` | `Metric source` 表 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 量度 `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | 量度 `timestamp` （和报告） `time range`) |
| `GROUP BY coupon_code` | 报表 `group by` |

>[!NOTE]
>
>与我们之前开始使用的查询唯一的区别是，将“coupon\_code”作为组添加者。_

使用相同 `Total Revenue` 我们之前创建的量度，现在可以创建按优惠券代码划分的收入报表！ 请查看下面的gif动图，其中显示如何设置此可视报表，查看9月至11月的数据：

![按优惠券代码划分的收入](../../assets/Revenue_by_coupon_code.gif)

## 公式

在某些情况下，查询可能涉及多个聚合以计算单独列之间的关系。 例如，您可以通过以下两种方式之一计算查询中的平均订单值：

* `AVG('order\_total')` 或
* `SUM('order\_total')/COUNT('order\_id')`

前一种方法将涉及创建新量度，该量度在 `order\_total` 列。 但是，后一种方法可以在报表生成器中直接创建(假定您已经设置了计算 `Total Revenue` 和 `Number of orders`.

让我们退一步，查看 `Average order value`:

|  |  |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | 量度 `operation` (column) |
| `COUNT(order_id) as "Number of orders"` | 量度 `operation` (column) |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | 量度 `operation` （列）/量度操作（列） |
| `FROM orders` | 量度 `source` 表 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 量度 `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | 量度时间戳（和报表时间范围） |

此外，我们还假定已设置量度来计算 `Total Revenue` 和 `Number of orders`. 由于这些量度已存在，因此我们只需打开 `Report Builder` 和使用 `Formula` 功能：

![AOV公式](../../assets/AOV_forumula.gif)

## 包装

正如本文开头所述，如果您是一个庞大的SQL用户，请考虑如何在中转换查询 [!DNL MBI] 将允许您生成计算列、量度和报表。

要快速参考，请查看下面的矩阵。 这显示SQL子句的等效项 [!DNL MBI] 元素以及元素如何映射到多个元素，具体取决于该元素在查询中的使用方式。

## MBI元素

|**`SQL Clause`**|**`Metric`**|**`Filter`**|**`Report group by`**|**`Report time frame`**|**`Path`**|**`Calculated column inputs`**|**`Source table`**| |—|—|—|—|—|—|—| |`SELECT`|X|-|X|-|-|X|-| |`FROM`|-|-|-|-|-|-|-|-|X| |`WHERE`|-|X|-|-|-|-|-|-| |`WHERE` （包含时间元素）|-|-|-|-|X|-|-|-|-| |`JOIN...ON`|-|X|-|-|X|X|-| |`GROUP BY`|-|-|X|-|-|-|-|-|
