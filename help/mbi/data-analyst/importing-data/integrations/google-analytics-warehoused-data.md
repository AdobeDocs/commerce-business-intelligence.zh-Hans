---
title: 预期的Google Analytics仓库数据
description: 了解如何与您的Google Analytics存储数据交互。
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# 预期[!DNL Google Analytics Warehoused]数据

>[!NOTE]
>
>需要[管理员权限](../../../administrator/user-management/user-management.md)。

>[!NOTE]
>
>在[[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics)的朋友允许下使用了某些信息。

[!DNL Google Analytics Warehoused]中的[!DNL Commerce Intelligence]集成使用[!DNL Google Analytics] [核心报表API](https://developers.google.com/analytics/devguides/reporting/core/v3/)。

>[!NOTE]
>
>为避免出现意外或无意义的结果，请确认您使用的任何维度都与您在[中使用的一个或多个量度](https://ga-dev-tools.google/dimensions-metrics-explorer/)兼容。`Report Builder`

在您的Data Warehouse中创建一个名为`report`的表。

此表的架构由您在设置过程中选择的量度和维度以及另外两列组成：`start-date`和`end-date`。

例如，如果在设置期间选择了以下量度和维度：

* `Metrics`： `ga:users`
* `Dimensions`： `ga:month`

该表将类似于下面的示例。

| **列名称** | **描述** |
|-----|-----|
| `\_id` | 此列是`primary key`。 |
| `\_rjm\_record\_hash` | [!DNL Commerce Intelligence]唯一标识符。 此列由[!DNL Commerce Intelligence]创建。 |
| `\_updated\_at` | 此列包含上次更新数据行的时间。 此列由[!DNL Commerce Intelligence]创建。 |
| `start-date` | 行用于哪天的标识。 |
| `end-date` | 行用于哪天的标识。 |
| `month` | 所选维度：会话的月份，一个从01到12的两位整数。 |
| `users` | 所选度量：所请求时段内的用户总数。 |

{style="table-layout:auto"}

## [!DNL Google Analytics Warehoused]和[!DNL Live Integration]之间有何区别

主要区别在于存储了一个集成([!DNL Google Analytics Warehoused])，而另一个集成不是([!DNL Google Analytics Live])。 在[!DNL Google Analytics Warehoused]的情况下，这将允许处理您的[!DNL Google Analytics]数据，并使您能够组合[!DNL Google Analytics]和其他数据源以创建富有洞察力的报表。

查看[!DNL Google Analytics]广告营销活动以了解从操作角度可以做些什么的示例。 假设您在第四季度有多个名称不同的广告营销活动。 这些营销活动是特定营销计划的结果。 使用仓储数据，您可以创建一个列，以查找相关促销活动名称并返回`Operation Dumbo`的第4季度计划名称。

组合方面允许将[!DNL Google Analytics]数据与其他数据连接以进行分析。 例如，获取`Total Time On Site By Ad Campaign`中的[!DNL Google Analytics]数据，并将其与来自`Total Spent Per Campaign`的[!DNL Facebook Ads]数据联接，以完整了解参与度对您造成的成本。

另一方面，使用[!DNL Google Analytics Live]集成，每个[!DNL Google Analytics]图表都像一个未存储在[!DNL Commerce Intelligence] Data Warehouse中的小思洛存储器。

## 相关：

* [正在连接 [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
