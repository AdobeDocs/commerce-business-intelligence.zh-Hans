---
title: 创建和使用Data warehouse视图
description: 了解通过修改现有表或使用SQL将多个表连接或合并在一起来创建新的仓库表的方法。
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 9%

---

# 使用Data warehouse视图

本文档概述了的用途和用途 `Data Warehouse Views` 可通过导航到 **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**. 以下解释了其作用以及如何创建视图，并举例说明如何使用 `Data Warehouse Views` 合并 [!DNL Facebook] 和 [!DNL AdWords] 支出数据。

## 一般用途

此 `Data Warehouse Views` 特征是一种方法，通过修改现有表或者使用SQL将多个表连接或合并在一起来创建新的仓库表。 一次 `Data Warehouse View` 已按照更新周期创建和处理，将在Data warehouse中作为新表填充到 `Data Warehouse Views` 下拉列表，如下所示：

![](../../assets/Data_Warehouse.png)

在此处，您的新视图功能与任何其他表类似，使您能够创建新计算列或在其上构建量度和报表。

`Data Warehouse Views` 主要用于将多个相似但不同的表整合在一起，以使所有报表都可以基于单个新表构建。 一些常见示例包括合并旧数据库和实时数据库中的表以组合历史数据和当前数据，或将多个广告源(如Facebook和AdWords)组合为一个广告源 `Consolidated ad spend` 表格。

如果您熟悉SQL ，则这两个合并示例都使用 `UNION` 函数，但在构建新视图时，可以使用任何PostgreSQL语法和函数。

## 创建和管理Data warehouse视图

新 `Data Warehouse Views` 通过导航到，可以创建并删除现有视图 **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**，如下所示：

![](../../assets/Data_Warehouse_Views.png)

在此处，您可以按照以下示例说明创建视图：

1. 如果观察现有视图，请单击 **[!UICONTROL New Data Warehouse View]** 以打开空白查询窗口。 如果已打开空白查询窗口，请继续执行下一步。
1. 通过键入视图名称 `View Name` 字段。 此处提供的名称确定Data warehouse中视图的显示名称。 `View names` 仅限使用小写字母、数字和下划线(_)。 禁止使用所有其他字符。
1. 在标题为的窗口中输入查询 `Select Query`，使用标准PostgreSQL语法。

   >[!NOTE]
   >
   >您的查询必须引用特定的列名称。 使用 `*`不允许使用字符选择所有列。

1. 完成后，单击 **[!UICONTROL Save]** 以保存视图。 您的视图暂时 `Pending` 状态，直到下一次完整更新周期处理该更新，此时状态将更改为 `Active`. 经过更新处理后，您的视图便可在报表中使用。

需要注意的是，在保存之后，用于生成 `Data Warehouse View` 无法编辑。 如果需要调整 `Data Warehouse View`，您必须创建一个视图，并手动将任何计算列、量度或报表从原始视图迁移到新视图。 迁移完成后，您可以安全地删除原始视图。 因为 `Data Warehouse Views` 不可编辑，Adobe建议您使用 `SQL Report Builder` 将查询另存为Data warehouse视图之前。

## 示例： [!DNL Facebook] 和 [!DNL Google AdWords] 数据

仔细看一下本文前面提到的示例之一：整合 [!DNL Facebook] 和 [!DNL AdWords] 将数据放入新的整合广告表中。 最常见的是涉及两个表的合并，其示例数据集如下：

`Ad source: Google AdWords`

`Table name: campaigns67890`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | eee | 60 | 2017-05-05 00:00:00 | 2000 | 10.2 |
| 2 | ggg | 40 | 2017-05-23 00:00:00 | 900 | 4.6 |
| 3 | aaa | 22 | 2017-06-12 00:00:00 | 400 | 2.5 |
| 4 | eee | 350 | 2017-06-30 00:00:00 | 14500 | 35 |
| 5 | fff | 280 | 2017-07-10 00:00:00 | 10200 | 28.5 |

`Ad source: Facebook`

`Table name: facebook_ads_insights_12345`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | aaa | 25 | 2017-05-01 00:00:00 | 1200 | 5 |
| 2 | ddd | 12 | 2017-05-15 00:00:00 | 800 | 2.5 |
| 3 | aaa | 40 | 2017-05-22 00:00:00 | 2000 | 7 |
| 4 | aaa | 110 | 2017-06-08 00:00:00 | 6000 | 10 |
| 5 | ccc | 5 | 2017-07-06 00:00:00 | 300 | 1.2 |

要创建包含两者的单个广告支出表，请执行以下操作 [!DNL Facebook] 和 [!DNL Google AdWords] 营销活动，您必须编写SQL查询并使用 `UNION ALL` 函数。 A `UNION ALL` 语句通常用于组合多个不同的SQL查询，同时将每个查询的结果附加到单个输出。

有一些要求 `UNION` 值得一提的语句，如PostgreSQL中所述 [文档](https://www.postgresql.org/docs/8.3/queries-union.html)：

* 所有查询必须返回相同的列数
* 对应的列必须具有相同的数据类型

执行时 `UNION` 或 `UNION ALL` 语句中，最终输出中列的名称反映了第一个查询中列的命名。

通常，整合您的 [!DNL Facebook] 和 [!DNL Google AdWords] 将数据放入 `Data Warehouse View` 需要创建一个包含七列的表，其查询类似于以下内容：

```sql
    SELECT
        "_id" as id,
        'AdWords' as ad_source,
        "date",
        "campaign",
        "adCost" as spend,
        "impressions",
        "adClicks" as clicks
    FROM campaigns67890
    UNION
    SELECT
        "_id" as id,
        'Facebook' as ad_source,
        "date_start" as date,
        "campaign_name" as campaign,
        "spend",
        "impressions",
        "clicks"
    FROM facebook_ads_insights_12345
```

关于以上几点：

* 为了清楚起见，所有列都使用上面的别名，以便名称在所有查询中匹配。 但是，这不是一项要求。 在SELECT查询中调用列的顺序指示了列的排列方式。
* 名为的新列 `ad_source` 创建以便于筛选 [!DNL AdWords] 或 [!DNL Facebook] 数据。 请记住，此查询组合来自两个表的所有数据。 如果您不创建列，例如 `ad_source`，要识别来自特定来源的支出，没有简单的方法。

将以上查询另存为 `Data Warehouse View` 创建同时包含两者的表 [!DNL Facebook] 和 [!DNL AdWords] 支出，类似于以下内容：

| **`id`** | **`ad_source`** | **`date`** | **`campaign`** | **`spend`** | **`impressions`** | **`clicks`** |
|--- |--- |--- |--- |--- |--- |--- |
| **1** | [!DNL Facebook] | 2017-05-01 00:00:00 | aaa | 5 | 1200 | 25 |
| **1** | [!DNL Google AdWords] | 2017-05-05 00:00:00 | eee | 10.2 | 2000 | 60 |
| **2** | [!DNL Facebook] | 2017-05-15 00:00:00 | ddd | 2.5 | 800 | 12 |
| **2** | [!DNL Google AdWords] | 2017-05-23 00:00:00 | ggg | 4.6 | 900 | 40 |
| **3** | [!DNL Facebook] | 2017-05-22 00:00:00 | aaa | 7 | 2000 | 40 |
| **3** | [!DNL Google AdWords] | 2017-06-12 00:00:00 | aaa | 2.5 | 400 | 22 |
| **4** | [!DNL Facebook] | 2017-06-08 00:00:00 | aaa | 10 | 6000 | 110 |
| **4** | [!DNL Google AdWords] | 2017-06-30 00:00:00 | eee | 35 | 14500 | 350 |
| **5** | [!DNL Facebook] | 2017-07-06 00:00:00 | ccc | 1.2 | 300 | 5 |
| **5** | [!DNL Google AdWords] | 2017-07-10 00:00:00 | fff | 28.5 | 10200 | 280 |

您无需为每个广告源创建单独的营销量度集，而是可以使用上表只创建一组量度来捕获您的所有广告。

**正在寻求其他帮助？**

编写SQL和创建 `Data Warehouse Views` 技术支持中未提供。 但是， [服务团队](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 确实有助于创建视图。 对于从使用新数据库迁移旧数据库到创建单个Data warehouse视图以进行特定分析的所有内容，支持团队都可以提供帮助。

通常，创建新的 `Data Warehouse View` 为了合并2-3个类似结构的表，需要五小时的服务时间，这相当于大约1,250美元的工作。 然而，以下是可增加所需预期投资的几个常见因素：

* 将三个以上的表合并到单个视图中
* 创建多个Data warehouse视图
* 复杂的连接逻辑或筛选条件
* 数据结构不同的两个或多个表的合并
