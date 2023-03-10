---
title: 将SQL查询转换为 [!DNL MBI] 报告
description: 了解如何将SQL查询转换为计算列以及您在中使用的量度 [!DNL MBI].
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# 在MBI中翻译SQL查询

曾经想知道如何将SQL查询转换为 [计算列](../data-warehouse-mgr/creating-calculated-columns.md)， [量度](../../data-user/reports/ess-manage-data-metrics.md)、和 [报告](../../tutorials/using-visual-report-builder.md) 您在中使用 [!DNL MBI]？ 如果您是重型SQL用户，请了解SQL在中如何翻译 [!DNL MBI] 使您能够在以下位置更智能地工作： [data warehouse管理器](../data-warehouse-mgr/tour-dwm.md) 并充分利用 [!DNL MBI] 平台。

在本文的最后，您会找到 **翻译矩阵** SQL查询子句和 [!DNL MBI] 元素。

首先查看常规查询：

|  |  |
|--- |--- |
| `SELECT` |  |
| `a,` | 报告 `group by` |
| `SUM(b)` | `Aggregate function` （列） |
| `FROM c` | `Source` 表 |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | 报告 `time frame` |
| `GROUP BY a` | 报告 `group by` |

此示例涵盖了大多数翻译案例，但有一些例外。 深入了解，从如何 `aggregate` 函数被转换。

## 集合函数

集合函数(例如， `count`， `sum`， `average`， `max`， `min`)在查询中，可以采用以下形式 **量度聚合** 或 **列聚合** 在 [!DNL MBI]. 区分因素是执行聚合是否需要连接。

查看以上每个方面的示例。

## 量度聚合 {#aggregate}

聚合时需要量度 `within a single table`. 例如， `SUM(b)` 来自上述查询的聚合函数极有可能由对列求和的量度表示 `B`. 

查看以下特定示例： `Total Revenue` 量度可在 [!DNL MBI]. 查看下面您尝试翻译的查询：

|  |  |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` （列） |
| `FROM orders` | `Metric source` 表 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 量度 `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | 量度 `timestamp` （和报表） `time range`) |

通过单击导航到量度生成器 **[!UICONTROL Manage Data** > **&#x200B;量度&#x200B;**> **创建新量度]**，您必须首先选择适当的 `source` 表，在此例中为 `orders` 表格。 然后，将设置量度，如下所示：

![指标聚合](../../assets/Metric_aggregation.png)

## 列聚合

在聚合从另一个表连接的列时，需要计算列。 例如，您可能有一个内置于 `customer` 已调用的表 `Customer LTV`，对以下位置中与该客户关联的所有订单的总值求和： `orders` 表格。

此聚合的查询可能如下所示：

|  |  |
|--- |--- |
| `Select` |  |
| `c.customer_id` | 聚合所有者 |
| `SUM(o.order_total) as "Customer LTV"` | 聚合操作（列） |
| `FROM customers c` | 聚合所有者表 |
| `JOIN orders o` | 聚合源表 |
| `ON c.customer_id = o.customer_id` | 路径 |
| `WHERE o.status = 'success'` | 聚合筛选器 |

在中设置 [!DNL MBI] 需要使用Data warehouse管理器，在其中构建 `orders` 和 `customers` 表，然后创建一个名为的列 `Customer LTV` 在您客户的桌子上。

了解如何在 `customers` 和 `orders`. 最终目标是在 `customers` 表，因此首先导航到 `customers` data warehouse表格，然后单击 **[!UICONTROL Create a Column** > **&#x200B;选择定义&#x200B;**> **SUM]**.

接下来，您需要选择源表。 如果存在指向您的页面的路径， `orders` 表，只需从下拉菜单中选择它即可。 但是，如果要构建新路径，请单击 **[!UICONTROL Create new path]** 此时将显示以下屏幕：

![创建新路径](../../assets/Create_new_path.png)

在此，您需要仔细考虑您尝试连接的两个表之间的关系。 在这种情况下，可能会出现 `Many` 与关联的订单 `One` 客户，因此 `orders` 表格列于 `Many` 侧，而 `customers` 表已选择 `One` 侧面。

>[!NOTE]
>
>In [!DNL MBI]， a *路径* 等同于 `Join` 在SQL中。

保存路径后，您便可以创建 `Customer LTV` 列！ 请看以下内容：

![](../../assets/Customer_LTV.gif)

现在您已构建新的 `Customer LTV` 中的列 `customers` 表，您已准备好创建 [指标聚合](#aggregate) 使用此列（例如，查找每个客户的平均LTV）。 您还可以 `group by` 或 `filter` 的计算列（使用基于以下项构建的现有指标） `customers` 表格。

>[!NOTE]
>
>对于后者，无论何时构建新的计算列，您都必须 [将维度添加到现有量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 在它作为 `filter` 或 `group by`.

参见 [创建计算列](../data-warehouse-mgr/creating-calculated-columns.md) 与您的Data warehouse经理联系。

## `Group By` 子句

`Group By` 查询中的函数通常表示为 [!DNL MBI] 用作对可视化报表进行分段或过滤的列。 例如，让我们重新访问 `Total Revenue` 您之前探索的查询，但这次按 `coupon\_code` 以更好地了解哪些优惠券产生的收入最多。

从下面的查询开始：

|  |  |
|--- |--- |
| `SELECT coupon_code,` | 报告 `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`（列） |
| `FROM orders` | `Metric source` 表 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 量度 `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | 量度 `timestamp` （和报表） `time range`) |
| `GROUP BY coupon_code` | 报告 `group by` |

>[!NOTE]
>
>与之前开始的查询的唯一区别是添加了“coupon\_code”作为分组依据。_

使用相同的 `Total Revenue` 您之前创建的量度，现在可以创建按优惠券代码分段的收入报表了！ 查看下面的gif，其中显示了如何设置此可视化报表，查看9月至11月的数据：

![按优惠券代码列出的收入](../../assets/Revenue_by_coupon_code.gif)

## 公式

有时，查询可能涉及多个聚合，以便计算单独列之间的关系。 例如，您可以通过以下两种方法之一计算查询中的平均订单值：

* `AVG('order\_total')` 或
* `SUM('order\_total')/COUNT('order\_id')`

前一种方法涉及创建一个新量度，该量度对 `order\_total` 列。 但是，后一种方法可以直接在Report Builder中创建，前提是您已设置指标以计算 `Total Revenue` 和 `Number of orders`.

退一步看一下针对以下项的整体查询： `Average order value`：

|  |  |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | 量度 `operation` （列） |
| `COUNT(order_id) as "Number of orders"` | 量度 `operation` （列） |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | 量度 `operation` （列）/量度操作（列） |
| `FROM orders` | 量度 `source` 表 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 量度 `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | 量度时间戳（和报告时间范围） |

现在，假定您已设置指标以计算 `Total Revenue` 和 `Number of orders`. 由于存在这些量度，因此您只需打开 `Report Builder` 并使用创建按需计算 `Formula` 功能：

![AOV公式](../../assets/AOV_forumula.gif)

## 总结

如果您是繁重的SQL用户，请考虑查询在中如何翻译 [!DNL MBI] 使您能够构建计算列、量度和报表。

如需快速参考，请查看下面的矩阵。 这显示了SQL子句的等效项 [!DNL MBI] 元素以及它如何映射到多个元素，具体取决于它在查询中的使用方式。

## MBI元素

|**`SQL Clause`**|**`Metric`**|**`Filter`**|**`Report group by`**|**`Report time frame`**|**`Path`**|**`Calculated column inputs`**|**`Source table`**| 
|--|--|--|--|--|--|--|--|
|`SELECT`|X|-|X|-|-|X|-|
|`FROM`|-|-|-|-|-|-|X|
|`WHERE`|-|X|-|-|-|-|-|
|`WHERE` （含时间元素）|-|-|-|X|-|-|-|
|`JOIN...ON`|-|X|-|-|X|X|-|
|`GROUP BY`|-|-|X|-|-|-|-|
