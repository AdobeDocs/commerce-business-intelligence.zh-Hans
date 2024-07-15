---
title: 非基于日期的同类群组的同类群组Report Builder
description: 了解如何按相似的活动或属性对用户进行分组。
exl-id: c7b85ce9-113c-4ffc-855f-3d53fe2347d8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 76c5329c3f55570fa4e46601e902dc5a09e319e7
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# 非基于日期的同类群组的[!DNL Cohort Report Builder]

[`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md)非常有助于商家研究用户在不同时间内的行为方式。 过去，`Cohort Report Builder`已针对按公共`cohort date`对用户进行分组进行了优化（例如，在给定月份首次购买的所有客户集）。 `Non-Date Based Cohort`功能现在允许您按类似的活动或属性对用户进行分组。 查看此功能的几个用例。

## 用例

这不是一个全面的列表，但以下是使用此功能可以完成的一些潜在分析。

* 检查从[!DNL Google]获得的客户收入与[!DNL Facebook]的收入
* 分析首次购买地点在美国与加拿大的客户
* 查看从各种广告促销活动获得的客户行为

## 如何创建分析

1. 在左侧选项卡上单击&#x200B;**[!UICONTROL Report Builder]**，或在任意仪表板中单击&#x200B;**[!UICONTROL Add Report** > **Create Report]**。

1. 在`Report Builder Selection`屏幕中，单击`Visual Report Builder`选项旁边的&#x200B;**[!UICONTROL Create Report]**。

### 添加量度

现在您位于`Report Builder`中，添加要对其执行分析的量度（示例： `Revenue`或`Orders`）。

>[!NOTE]
>
>本机[!DNL Google Analytics]量度与`Cohort Report Builder`不兼容。 此示例的目标是查看通过不同[!DNL Google Analytics]来源获得的第一订单客户在一段时间内的收入。

### 将`Metric View`切换为`Cohort`

![1切换同类群组的量度视图](../../assets/1-toggle-metric-view-to-cohort.png)

该操作将打开一个新窗口，您可以在其中配置同类群组报表的详细信息。

构建同类群组报表需要五种规范：

1. 如何将同类群组分组
1. 选择同类群组
1. 操作时间戳
1. 同类群组首次操作时间范围
1. 同类群组发生后的时间范围

![同类群组](../../assets/2-cohort-groups.png)<!--{: width="200" height="224"}-->



#### 1.分组`cohorts`

`Cohorts`按行为特征分组，在本例中为`Customer's first order GA source`。 此处可用的选项是已指定为指标的`groupable`的列。

#### 2.选择同类群组

可以显示给定特征的所有结果。 由于这会产生多个`cohorts`，因此您可以选择所需的特定`cohorts` （对应于可用于`Customer's first order GA source`的各种值）。

![同类群组](../../assets/4-cohort-groups.png)<!--{: width="300" height="338"}-->

#### 3. `Action timestamp`

这允许您选择基于日期的列，而不是创建量度的列。 在下方，您会看到选择适用于给定`action timestamp`的时间范围。

#### 4. `Cohort first action time range`

在这里，您可以选择包含`cohorts action timestamp`的日期范围（例如，第一张订单介于2017年11月至2018年10月的客户）。 这可以是移动日期范围或固定日期范围。

#### 5. `Time range after cohort occurrence`

是否要按月、周或年查看`cohorts`随时间的变化？ 您可在以下位置进行这些选择。 在该部分下，您将在`cohort action timestamp`发生后选择`time range`。 例如，对于在操作时间范围内下达了第一笔订单的客户，这会向您显示12个月的数据。

![cohort-first-action-time-range](../../assets/5-cohort-first-action-time-range.png)<!--{: width="400" height="557"}-->

>[!NOTE]
>
>当您在`Standard`和`Cohort`视图之间切换时，应用于您的量度的[!UICONTROL Filters]将保持不变。

### 相关

请参阅[`Perspectives`](../../data-analyst/dev-reports/cohort-rpt-bldr.md)。
