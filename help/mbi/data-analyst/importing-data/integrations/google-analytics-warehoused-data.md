---
title: 预期Google Analytics仓库数据
description: 了解如何与Google Analytics仓库数据进行交互。
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# 预期 [!DNL Google Analytics] 仓库数据

>[!NOTE]
>
>需要 [管理员权限](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>有些信息是经我们朋友的许可，在 [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] 集成 [!DNL MBI] 利用 [!DNL Google Analytics] [核心报表API](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>要避免出现意外或无意义的结果，请确认您使用的任何维度均为 [与量度兼容](https://developers.google.com/analytics/devguides/reporting/core/dimsmets) 在 `Report Builder`.

一个表 — 称为 `report`  — 将在您的Data warehouse中创建。

此表的架构将由您在设置过程中选择的量度和Dimension以及另外两列组成： `start-date` 和 `end-date`.

例如，如果您在设置过程中选择了以下量度和Dimension:

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

该表将类似于以下示例。

| **列名称** | **描述** |
|-----|-----|
| `\_id` | 此列是 `primary key`. |
| `\_rjm\_record\_hash` | [!DNL MBI] 唯一标识符。 此列由 [!DNL MBI]. |
| `\_updated\_at` | 此列包含数据行上次更新的时间。 此列由 [!DNL MBI]. |
| `start-date` | 行用于哪一天的标识。 |
| `end-date` | 行用于哪一天的标识。 |
| `month` | 所选维度：会话月份，一个01到12之间的两位数整数。 |
| `users` | 选定量度：请求的时间段内的用户总数。 |

{style=&quot;table-layout:auto&quot;}

## 提醒：Google Analytics仓库与实时集成之间的差异

主要区别在于存储了一个集成([!DNL Google Analytics Warehoused])，而另一个则不是([!DNL Google Analytics Live])。 对于 [!DNL Google Analytics Warehoused]，这允许对 [!DNL Google Analytics] 数据，并让您能够 [!DNL Google Analytics] 和其他数据源，以创建有洞察力的报表。

让我们看看 [!DNL Google Analytics] 广告营销活动，以展示从操作角度可以执行的操作。 假设您有多个不同名称的第4季度广告营销活动。 营销活动是特定营销计划的结果。 利用仓库数据，我们可以创建一个新列，以查找相关促销活动名称并返回 `Operation Dumbo`.

组合方面允许 [!DNL Google Analytics] 要连接到其他数据以进行分析的数据。 例如， `Total Time On Site By Ad Campaign` 数据 [!DNL Google Analytics] 加入到 `Total Spent Per Campaign` 数据 [!DNL Facebook Ads] 全面了解您的参与度花费。

使用 [!DNL Google Analytics Live] 另一方面， [!DNL Google Analytics] 图表就像一个小接收器，不会存储在您的 [!DNL MBI] data warehouse。

## 相关：

* [连接 [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
