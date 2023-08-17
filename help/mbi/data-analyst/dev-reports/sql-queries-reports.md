---
title: 将SQL查询转换为Commerce Intelligence报表
description: 了解如何将SQL查询转换为计算量度（您在Commerce Intelligence中使用的量度）。
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# 在Commerce Intelligence中翻译SQL查询

曾想过SQL查询如何转换为 [计算列](../data-warehouse-mgr/creating-calculated-columns.md)， [量度](../../data-user/reports/ess-manage-data-metrics.md)、和 [报表](../../tutorials/using-visual-report-builder.md) 您使用 [!DNL Commerce Intelligence]？ 如果您是重型SQL用户，请了解SQL在中如何转换 [!DNL Commerce Intelligence] 使您能够在以下位置更智能地工作： [Data Warehouse管理器](../data-warehouse-mgr/tour-dwm.md) 并充分利用 [!DNL Commerce Intelligence] 平台。

在本主题结束时，您会找到 **翻译矩阵** SQL查询子句和 [!DNL Commerce Intelligence] 元素。

首先查看常规查询：

| | |
|--- |--- |
| `SELECT` |  |
| `a,` | 报表 `group by` |
| `SUM(b)` | `Aggregate function` （列） |
| `FROM c` | `Source` 表 |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | 报表 `time frame` |
| `GROUP BY a` | 报表 `group by` |

此示例涵盖了大多数翻译案例，但有一些例外。 深入了解，从如何 `aggregate` 函数被转换。

## 集合函数

集合函数(例如， `count`， `sum`， `average`， `max`， `min`)在查询中，可以采用以下形式 **量度聚合** 或 **列聚合** 在 [!DNL Commerce Intelligence]. 差异因素在于是否需要连接以执行聚合。

查看以上每个内容的示例。

## 量度聚合 {#aggregate}

聚合时需要量度 `within a single table`. 例如， `SUM(b)` 上述查询中的聚合函数极有可能由对列求和的量度表示 `B`. 

查看以下特定示例： `Total Revenue` 量度可定义于 [!DNL Commerce Intelligence]. 查看下面您尝试翻译的查询：

| | |
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

聚合从另一个表连接的列时需要计算列。 例如，您可能在中内置了一列 `customer` 已调用的表 `Customer LTV`，合计中与该客户关联的所有订单的总值。 `orders` 表格。

此聚合的查询可能如下所示：

|  |  |
|--- |--- |
| `Select` | |
| `c.customer_id` | 聚合所有者 |
| `SUM(o.order_total) as "Customer LTV"` | 聚合操作（列） |
| `FROM customers c` | 聚合所有者表 |
| `JOIN orders o` | 聚合源表 |
| `ON c.customer_id = o.customer_id` | 路径 |
| `WHERE o.status = 'success'` | 聚合筛选器 |

在中设置 [!DNL Commerce Intelligence] 需要使用Data Warehouse管理器，在其中构建 `orders` 和 `customers` 表，然后创建一个名为的列 `Customer LTV` 在您客户的桌子上。

了解如何在 `customers` 和 `orders`. 最终目标是在 `customers` 表格，因此首先导航到 `customers` Data Warehouse中的表，然后单击 **[!UICONTROL Create a Column** > **&#x200B;选择定义&#x200B;**> **SUM]**.

接下来，您需要选择源表。 如果存在指向您的目录的路径， `orders` 表，只需从下拉列表中选择它即可。 但是，如果要构建新路径，请单击 **[!UICONTROL Create new path]** 此时将显示以下屏幕：

![创建新路径](../../assets/Create_new_path.png)

在此，您需要仔细考虑您尝试连接的两个表之间的关系。 在这种情况下，有可能 `Many` 与关联的订单 `One` 客户，因此， `orders` 表格列于 `Many` 侧，而 `customers` 在上选择的表 `One` 侧面。

>[!NOTE]
>
>在 [!DNL Commerce Intelligence]， a `path` 等同于 `Join` 在SQL中。

保存路径后，您可以创建 `Customer LTV` 列！ 请参阅下文：

![](../../assets/Customer_LTV.gif)

您现在已经构建了 `Customer LTV` 列中的 `customers` 表，您已准备创建 [指标聚合](#aggregate) 使用此列（例如，查找每个客户的平均LTV）。 您还可以 `group by` 或 `filter` 的计算列（使用基于以下项构建的现有量度） `customers` 表格。

>[!NOTE]
>
>对于后者，无论何时构建新的计算列，您都必须 [将维度添加到现有量度](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 在它可用作 `filter` 或 `group by`.

请参阅 [创建计算列](../data-warehouse-mgr/creating-calculated-columns.md) 与您的Data Warehouse管理员合作。

## `Group By` 子句

`Group By` 查询中的函数通常表示为 [!DNL Commerce Intelligence] 用作列，用于对可视化报表进行分段或过滤。 例如，让我们重新访问 `Total Revenue` 您之前探索的查询，但这次按 `coupon\_code` 以更好地了解哪些优惠券产生的收入最多。

从下面的查询开始：

| | |
|--- |--- |
| `SELECT coupon_code,` | 报表 `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`（列） |
| `FROM orders` | `Metric source` 表 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 量度 `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | 量度 `timestamp` （和报表） `time range`) |
| `GROUP BY coupon_code` | 报表 `group by` |

>[!NOTE]
>
>与之前开始的查询唯一的区别是添加了“coupon\_code”作为分组依据。_

使用相同的 `Total Revenue` 您之前创建的量度，现在可以创建按优惠券代码分段的收入报表了！ 查看下面的gif，其中显示了如何设置此可视化报表，查看9月至11月的数据：

![按优惠券代码列出的收入](../../assets/Revenue_by_coupon_code.gif)

## 公式

有时，查询可能涉及多个聚合，以便计算单独列之间的关系。 例如，您可以通过以下两种方法之一计算查询中的平均订单值：

* `AVG('order\_total')` 或者
* `SUM('order\_total')/COUNT('order\_id')`

前者涉及创建新指标，此指标在 `order\_total` 列。 但是，如果已经设置了量度来计算，则可以直接在Report Builder中创建后一种方法 `Total Revenue` 和 `Number of orders`.

退一步，查看以下内容的整体查询： `Average order value`：

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | 量度 `operation` （列） |
| `COUNT(order_id) as "Number of orders"` | 量度 `operation` （列） |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | 量度 `operation` （列）/量度操作（列） |
| `FROM orders` | 量度 `source` 表 |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 量度 `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | 量度时间戳（和报表时间范围） |

现在，假定您已设置指标以计算 `Total Revenue` 和 `Number of orders`. 由于存在这些量度，因此您只需打开 `Report Builder` 并使用以下方式创建按需计算 `Formula` 功能：

![AOV公式](../../assets/AOV_forumula.gif)

## 正在结束

如果您是繁重的SQL用户，请考虑如何在中翻译查询 [!DNL Commerce Intelligence] 使您能够生成计算列、量度和报表。

如需快速参考，请查看下面的矩阵。 这显示了SQL子句的等效项 [!DNL Commerce Intelligence] 元素，以及它如何映射到多个元素，具体取决于它在查询中的使用方式。

## Commerce Intelligence元素

| **`SQL Clause`** | **`Metric`** | **`Filter`** | **`Report group by`** | **`Report time frame`** | **`Path`** | **`Calculated column inputs`** | **`Source table`** |
|---|---|---|---|---|---|---|---|
| `SELECT` | X | - | X | - | - | X | - |
| `FROM` | - | - | - | - | - | - | X |
| `WHERE` | - | X | - | - | - | - | - |
| `WHERE` （包含时间元素） | - | - | - | X | - | - | - |
| `JOIN...ON` | - | X | - | - | X | X | - |
| `GROUP BY` | - | - | X | - | - | - | - |
