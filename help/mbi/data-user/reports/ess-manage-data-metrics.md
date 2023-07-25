---
title: 创建量度
description: 了解如何使用量度创建图表。
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# 创建量度

>[!NOTE]
>
>需要 [管理员权限](../../administrator/user-management/user-management.md).

量度是一种度量。 在SQL和数据库结构中，量度就像变量时段内的存储查询。

In [!DNL Commerce Intelligence]，您可以使用量度来 [创建图表](../../data-user/reports/ess-rpt-build-visual.md). 例如，量度 `revenue` 是订单总数。 量度 `average customer revenue per order` 是客户每次订购的平均花费。

在报表中使用量度时，可以在指定的时间段内分析量度，并且 [过滤或分段](../../best-practices/segment-filter.md) 按不同类别分类。 考虑分析按性别分组的平均客户收入 — 在这种情况下， `average customer revenue per order` 是量度，性别是分组。

## 定义量度 {#define}

1. 要创建指标，请单击 **[!UICONTROL Data** > **Metrics]**.

1. 单击 **[!UICONTROL Create New Metric]**.

1. 从下拉菜单中，单击包含要用于量度的本机列或计算列的表。

1. 为您的量度命名。

   Adobe建议一个名称，只需一眼即可告知您该指标是什么。 例如： `Average Order Revenue`.

1. 下一步是定义量度的用途。 使用下拉菜单，定义量度的操作， `operation` 列，和 `date` 维度：

   * 选择操作：
      * `Count`  — 此操作计算数据表中的行数
      * `Max`  — 最大值返回特定数据列的最大值
      * `Min` - Min返回特定数据列的最小值
      * `Sum`  — 此操作对特定数据列的值进行求和
      * `Average`  — 此操作计算数据列值的平均值
      * `Count Distinct Value`  — 此值计算特定数据列中的唯一值数
      * `Median`  — 此操作计算数据列值的中位数
      * `First and Third Quartiles`  — 这些操作分别计算数据列值的第25个百分位和第75个百分位
      * `Tenth and Ninetieth Percentiles`  — 这些操作分别计算数据列值的第10个百分位和第90个百分位

   * 选择要对其执行操作的列。 例如，如果您要查找总收入，则可以对 `order total` 列。

     如果您正在编辑现有量度，还可以 [更改量度的操作表](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) 在本节中。

   * 选择可用于对指标进行趋势分析的日期维度。 例如， `order date`.

## 添加筛选器 {#filters}

此 `Filter` 部分允许您创建过滤器或应用 [保存的筛选器集](../../data-user/reports/ess-manage-data-filters.md) 到您的量度。

对于 `average order revenue` 量度时，您不希望包含设置商店时可能完成的任何测试订单 — 这样会得到不准确的结果。 可以应用过滤器集以从数据集中删除这些订单。 创建过滤器后，该过滤器将应用于使用此量度构建的所有图表。

此 `Filter Logic` 部分中，您可以进一步定义量度的行为方式。

* &quot;\[`A`\]或\[`B`“\]”允许满足筛选条件的任何数据\[`A`\]或\[`B`\]
* &quot;\[`A`\]和\[`B`“\]”仅允许同时满足两个筛选器的数据\[`A`\]和\[`B`\]
* &quot;(\[`A`\]和\[`B`\])或\[`C`“\]”仅允许满足这两个筛选器的数据\[`A`\]和\[`B`\]，或满足筛选条件\[`C`\]独自

## 添加Dimension {#dimensions}

此 [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 部分显示用于筛选或分组的所有可用数据维；默认情况下，所有可用数据列将作为维列出。 继续此示例，如果您要按反向链接来源划分收入，可以在此处执行此操作。

除了将所有可用数据列列为维度之外， [!DNL Commerce Intelligence] 猜测列可分组到哪个位置。 *要对报表中的数据划分区段或分组，请执行以下操作*，列必须标记为可分组。

## 正在完成 {#finish}

除了定义量度的行为方式外，您还可以在 `User Rights` 部分。 While `Admin` 用户有权访问所有量度，您必须通过选中相应组旁边的复选框来指示可以使用此量度的用户。

如果您正在编辑现有指标，则可以在中查看使用此指标的图表（以及图表的所有者）的列表。 `Dependent Charts` 部分。

更改会自动保存，您的量度现已准备就绪。
