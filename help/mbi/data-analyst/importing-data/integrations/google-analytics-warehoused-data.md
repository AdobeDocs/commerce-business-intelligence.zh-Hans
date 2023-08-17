---
title: 预期的Google Analytics仓库数据
description: 了解如何与您的Google Analytics仓库数据交互。
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# 预期 [!DNL Google Analytics Warehoused] 数据

>[!NOTE]
>
>需要 [管理员权限](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>在朋友允许下使用了一些信息 [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] 集成 [!DNL Commerce Intelligence] 使用 [!DNL Google Analytics] [核心报表API](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>要避免出现意外或无意义的结果，请确认您使用的任何维度是 [与一个或多个量度兼容](https://ga-dev-tools.google/dimensions-metrics-explorer/) 您可在 `Report Builder`.

单个表 — 称为 `report`  — 在您的Data Warehouse中创建。

此表的方案由您在设置过程中选择的度量和Dimension以及另外两列组成： `start-date` 和 `end-date`.

例如，如果在设置期间选择了以下指标和Dimension：

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

该表将类似于下面的示例。

| **列名称** | **描述** |
|-----|-----|
| `\_id` | 此列是 `primary key`. |
| `\_rjm\_record\_hash` | [!DNL Commerce Intelligence] 唯一标识符。 此列的创建者 [!DNL Commerce Intelligence]. |
| `\_updated\_at` | 此列包含上次更新数据行的时间。 此列的创建者 [!DNL Commerce Intelligence]. |
| `start-date` | 行用于哪天的标识。 |
| `end-date` | 行用于哪天的标识。 |
| `month` | 所选维度：会话的月份，一个从01到12的两位整数。 |
| `users` | 所选度量：所请求时段内的用户总数。 |

{style="table-layout:auto"}

## 两者之间有何区别 [!DNL Google Analytics Warehoused] 和 [!DNL Live Integration]

主要区别在于存储了一个集成([!DNL Google Analytics Warehoused])，而另一个不是([!DNL Google Analytics Live])。 在以下情况下 [!DNL Google Analytics Warehoused]，这允许对您的 [!DNL Google Analytics] 数据，并让您能够合并 [!DNL Google Analytics] 和其他数据源，以创建有见地的报表。

查看 [!DNL Google Analytics] 广告营销活动，以从操作角度说明可执行的操作。 假设您在第四季度有多个名称不同的广告营销活动。 这些营销活动是特定营销计划的结果。 利用已存储的数据，您可以创建一个列，以查找相关促销活动名称并返回第4季度计划名称为 `Operation Dumbo`.

组合方面允许 [!DNL Google Analytics] 数据，为了进行分析。 例如，采用 `Total Time On Site By Ad Campaign` 数据来源 [!DNL Google Analytics] 并加入进来 `Total Spent Per Campaign` 数据来源 [!DNL Facebook Ads] 全面了解参与成本是多少。

使用 [!DNL Google Analytics Live] 另一方面，集成，每 [!DNL Google Analytics] 图表就像一个小筒仓，不会存储在 [!DNL Commerce Intelligence] Data Warehouse。

## 相关：

* [正在连接 [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
