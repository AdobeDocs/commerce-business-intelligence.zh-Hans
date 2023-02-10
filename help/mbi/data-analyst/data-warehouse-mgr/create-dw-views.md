---
title: 创建和使用Data warehouse视图
description: 了解通过修改现有表创建新仓库存储表的方法，或通过使用SQL将多个表连接或合并在一起的方法。
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 9%

---

# 使用Data warehouse视图

本文档概述了的用途和用途 `Data Warehouse Views` 可通过导航访问 **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**. 以下是其功能以及如何创建新视图的说明，以及如何使用示例 `Data Warehouse Views` 整合 [!DNL Facebook] 和 [!DNL AdWords] 支出数据。

## 一般用途

的 `Data Warehouse Views` 功能是一种通过修改现有表或通过使用SQL将多个表连接或合并在一起来创建新仓库存储表的方法。 一次 `Data Warehouse View` 已由更新周期创建和处理，它将作为新表填充在Data warehouse中，位于 `Data Warehouse Views` 下拉列表，如下所示：

![](../../assets/Data_Warehouse.png)

在此处，新视图的功能与任何其他表一样，让您能够创建新的计算列或在其上构建量度和报表。

`Data Warehouse Views` 主要用于将多个相似但不同的表合并在一起，以便所有报表都可以基于一个新表构建。 一些常见示例包括从旧版数据库和实时数据库合并表以合并历史和当前数据，或将多个广告源(如Facebook和AdWords)合并为单数 `Consolidated ad spend` 表。

如果您熟悉SQL，则这两个整合示例都将利用 `UNION` 函数，但在构建新视图时，可以使用任何PostgreSQL语法和函数。

## 创建和管理Data warehouse视图

新建 `Data Warehouse Views` 可以通过导航到 **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**，如下所示：

![](../../assets/Data_Warehouse_Views.png)

在此，您可以按照以下示例说明创建新视图：

1. 如果观察现有视图，请单击 **[!UICONTROL New Data Warehouse View]** 打开空白查询窗口。 如果已打开空白查询窗口，请继续执行下一步。
1. 通过在 `View Name` 字段。 此处提供的名称将确定Data warehouse中视图的显示名称。 `View names` 限于小写字母、数字和下划线(_)。 所有其他字符都禁止使用。
1. 在标题为的窗口中输入查询 `Select Query`，使用标准PostgreSQL语法。
   >[!NOTE]
   >
   >查询必须引用特定的列名称。 使用 `*`不允许使用字符选择所有列。

1. 完成后，单击 **[!UICONTROL Save]** 以保存视图。 请注意，您的视图将暂时包含 `Pending` 状态，直到下一个完整更新周期处理它，此时状态将更改为 `Active`. 更新处理后，您的视图即可在报表中使用。

请务必提及，在保存后，用于生成 `Data Warehouse View` 无法编辑。 如果出于某些原因，您需要调整 `Data Warehouse View`，则需要创建一个新视图，并手动将任何计算列、量度或报表从原始视图迁移到新视图。 迁移完成后，您可以安全地删除原始视图。 因为 `Data Warehouse Views` 不可编辑，我们强烈建议您使用 `SQL Report Builder` 将查询另存为“Data warehouse视图”之前，请执行以下操作：

## 示例： [!DNL Facebook] 和 [!DNL Google AdWords] 数据

让我们更仔细地查看本文前面提到的一个示例：合并 [!DNL Facebook] 和 [!DNL AdWords] 将数据花费到新的整合广告表中。 通常，这涉及合并两个表，并在下面显示示例数据集：

`Ad source: Google AdWords`

`Table name: campaigns67890`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | eee | 60 | 2017-05-05 00:00:00 | 2000 | 10.2 |
| 2 | gg | 40 | 2017-05-23 00:00:00 | 900 | 4.6 |
| 3 | aa | 22 | 2017-06-12 00:00:00 | 400 | 2.5 |
| 4 | eee | 350 | 2017-06-30 00:00:00 | 14500 | 35 |
| 5 | ff | 280 | 2017-07-10 00:00:00 | 10200 | 28.5 |

`Ad source: Facebook`

`Table name: facebook_ads_insights_12345`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | aa | 25 | 2017-05-01 00:00:00 | 1200 | 5 |
| 2 | dd | 12 | 2017-05-15 00:00:00 | 800 | 2.5 |
| 3 | aa | 40 | 2017-05-22 00:00:00 | 2000 | 7 |
| 4 | aa | 110 | 2017-06-08 00:00:00 | 6000 | 10 |
| 5 | cc | 5 | 2017-07-06 00:00:00 | 300 | 1.2 |

创建包含这两者的单个广告支出表 [!DNL Facebook] 和 [!DNL AdWords] 营销活动，我们需要编写一个SQL查询并利用 `UNION ALL` 函数。 A `UNION ALL` 语句通常用于合并多个不同的SQL查询，同时将每个查询的结果附加到单个输出。

对 `UNION` 值得一提的语句，如PostgreSQL中所述 [文档](https://www.postgresql.org/docs/8.3/queries-union.html):

* 所有查询必须返回相同数量的列
* 相应列必须具有相同的数据类型

执行 `UNION` 或 `UNION ALL` 语句中，最终输出中列的名称反映了第一个查询中列的命名。

在大多数情况下，整合 [!DNL Facebook] 和 [!DNL Google AdWords] 在 `Data Warehouse View` 将需要创建一个包含七列的表，并且其查询类似于以下内容：

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

关于上述几点重要信息：

* 为清楚起见，上面所有列都具有别名，以便名称在所有查询中都匹配。 但是，这不是要求。 在SELECT查询中调用列的顺序指示列的排列方式。
* 名为的新列 `ad_source` 是为了便于筛选 [!DNL AdWords] 或 [!DNL Facebook] 数据。 请记住，此查询将合并两个表中的所有数据。 如果不创建类似 `ad_source`，识别特定来源的支出将不是易事的方法。

将上述查询另存为 `Data Warehouse View` 将使用两者创建新表 [!DNL Facebook] 和 [!DNL AdWords] 支出，与以下内容类似：

| **`id`** | **`ad_source`** | **`date`** | **`campaign`** | **`spend`** | **`impressions`** | **`clicks`** |
|--- |--- |--- |--- |--- |--- |--- |
| **1** | [!DNL Facebook] | 2017-05-01 00:00:00 | aa | 5 | 1200 | 25 |
| **1** | [!DNL Google AdWords] | 2017-05-05 00:00:00 | eee | 10.2 | 2000 | 60 |
| **2** | [!DNL Facebook] | 2017-05-15 00:00:00 | dd | 2.5 | 800 | 12 |
| **2** | [!DNL Google AdWords] | 2017-05-23 00:00:00 | gg | 4.6 | 900 | 40 |
| **3** | [!DNL Facebook] | 2017-05-22 00:00:00 | aa | 7 | 2000 | 40 |
| **3** | [!DNL Google AdWords] | 2017-06-12 00:00:00 | aa | 2.5 | 400 | 22 |
| **4** | [!DNL Facebook] | 2017-06-08 00:00:00 | aa | 10 | 6000 | 110 |
| **4** | [!DNL Google AdWords] | 2017-06-30 00:00:00 | eee | 35 | 14500 | 350 |
| **5** | [!DNL Facebook] | 2017-07-06 00:00:00 | cc | 1.2 | 300 | 5 |
| **5** | [!DNL Google AdWords] | 2017-07-10 00:00:00 | ff | 28.5 | 10200 | 280 |

现在，您无需为每个广告源单独创建一组营销量度，而只需使用上表创建一组量度，即可捕获所有广告。

**寻求其他帮助？**

编写SQL并创建 `Data Warehouse Views` 不包含在技术支持中。  但是，服务团队在创建视图方面提供帮助。 从使用新数据库迁移和整合旧版数据库到创建用于特定分析的单个Data warehouse视图，所有方面他们都擅长针对所有数据结构难题策划基于SQL的解决方案。

在大多数情况下，创建新 `Data Warehouse View` 为了合并2-3个结构类似的表，需要5个小时的服务时间，也就是大约1250美元的工作量。 但以下是一些可增加预期所需投资的常见因素：

* 将3个以上的表合并到单个视图中
* 创建多个data warehouse视图
* 复杂的连接逻辑或筛选条件
* 合并2个或2个以上具有不相似数据结构的表
