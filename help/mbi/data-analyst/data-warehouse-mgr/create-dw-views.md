---
title: 创建和使用Data Warehouse视图
description: 了解通过修改现有表或使用SQL将多个表连接或合并在一起来创建新的仓库表的方法。
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 6%

---

# 使用Data Warehouse视图

本文档概述了可通过导航到&#x200B;**[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**&#x200B;访问`Data Warehouse Views`的用途和用途。 以下是其作用以及如何创建视图的解释，以及如何使用`Data Warehouse Views`合并[!DNL Facebook]和[!DNL AdWords]支出数据的示例。

## 一般目的

`Data Warehouse Views`功能是通过修改现有表或使用SQL将多个表连接或合并在一起来创建新的仓储表的方法。 在更新周期创建`Data Warehouse View`并进行处理后，它会在您的Data Warehouse中作为`Data Warehouse Views`下拉菜单下的新表进行填充，如下所示：

![](../../assets/Data_Warehouse.png)

在此处，您的新视图函数与任何其他表类似，使您能够创建新的计算列或在其上构建量度和报表。

`Data Warehouse Views`主要用于将多个相似但不同的表合并在一起，以使所有报表都可以基于单个新表构建。 一些常见示例包括：合并旧数据库和实时数据库中的表以组合历史数据和当前数据，或将多个广告源(如Facebook和AdWords)组合到单个`Consolidated ad spend`表中。

如果您熟悉SQL，则这两个合并示例都使用`UNION`函数，但在构建新视图时，您可以使用任何PostgreSQL语法和函数。

## 创建和管理Data Warehouse视图

通过导航到&#x200B;**[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**，可以创建新`Data Warehouse Views`并删除现有视图，如下所示：

![](../../assets/Data_Warehouse_Views.png)

在此处，您可以按照以下示例说明创建视图：

1. 如果观察现有视图，请单击&#x200B;**[!UICONTROL New Data Warehouse View]**&#x200B;打开空白查询窗口。 如果已经打开了空白查询窗口，请继续执行下一步。
1. 通过在`View Name`字段中键入内容来为视图命名。 此处提供的名称可确定Data Warehouse中视图的显示名称。 `View names`仅限于小写字母、数字和下划线(_)。 所有其他字符都被禁止。
1. 使用标准PostgreSQL语法，在标题为`Select Query`的窗口中输入查询。

   >[!NOTE]
   >
   >您的查询必须引用特定的列名称。 不允许使用`*`字符选择所有列。

1. 完成后，单击&#x200B;**[!UICONTROL Save]**&#x200B;保存视图。 您的视图暂时处于`Pending`状态，直到下一次完整更新周期处理它为止，此时状态将更改为`Active`。 经过更新处理后，您的视图便可在报表中使用。

需要注意的是，保存后，无法编辑用于生成`Data Warehouse View`的基础查询。 如果需要调整`Data Warehouse View`的结构，则必须创建一个视图，并手动将任何计算列、量度或报表从原始视图迁移到新视图。 迁移完成后，您可以安全地删除原始视图。 由于`Data Warehouse Views`不可编辑，因此Adobe建议您在将查询另存为Data Warehouse视图之前，使用`SQL Report Builder`测试查询的输出。

## 示例： [!DNL Facebook]和[!DNL Google AdWords]数据

请仔细查看本文前面提到的示例之一：将[!DNL Facebook]和[!DNL AdWords]支出数据合并到新的合并广告表中。 大多数情况下涉及两个表的合并，其示例数据集如下：

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

要创建包含[!DNL Facebook]和[!DNL Google AdWords]营销活动的单个广告支出表，您必须编写SQL查询并使用`UNION ALL`函数。 `UNION ALL`语句最常用于组合多个不同的SQL查询，同时将每个查询的结果附加到单个输出。

`UNION`语句有一些要求值得一提，如PostgreSQL [文档](https://www.postgresql.org/docs/8.3/queries-union.html)中所述：

* 所有查询必须返回相同的列数
* 对应的列必须具有相同的数据类型

执行`UNION`或`UNION ALL`语句时，最终输出中的列名反映第一个查询中的列名。

通常，将您的[!DNL Facebook]和[!DNL Google AdWords]支出数据合并到`Data Warehouse View`中需要创建一个包含七列的表，其查询类似于以下内容：

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

关于上述几点要点：

* 为了清楚起见，所有列都使用上述别名，以使名称在所有查询中匹配。 不过，这不是一项要求。 在SELECT查询中调用列的顺序指示了它们的对齐方式。
* 已创建一个名为`ad_source`的新列，以便更轻松地筛选[!DNL AdWords]或[!DNL Facebook]数据。 请记住，此查询将来自两个表的所有数据组合在一起。 如果不创建类似`ad_source`的列，则无法轻松识别来自特定来源的支出。

将以上查询另存为`Data Warehouse View`将创建一个同时包含[!DNL Facebook]和[!DNL AdWords]支出的表，如下所示：

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

您可以利用上表创建一组单独的量度，以捕获您的所有广告，而不是为每个广告源创建一组单独的营销量度。

**正在寻找其他帮助吗？**

技术支持不包括编写SQL和创建`Data Warehouse Views`。 但是，[服务团队](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hans)确实为创建视图提供了帮助。 对于从使用新数据库迁移旧数据库到创建单个Data Warehouse视图以进行特定分析的所有内容，支持团队都可以提供帮助。

通常，为合并2-3个类似结构的表而创建新`Data Warehouse View`需要五小时的服务时间，相当于大约1,250美元的工作时间。 然而，以下是可增加所需预期投资的几个共同因素：

* 将三个以上的表合并到单个视图中
* 创建多个Data Warehouse视图
* 复杂的连接逻辑或过滤条件
* 两个或多个数据结构不同的表的合并
