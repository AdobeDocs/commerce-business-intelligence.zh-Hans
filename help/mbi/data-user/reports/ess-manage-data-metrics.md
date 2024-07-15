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
>需要[管理员权限](../../administrator/user-management/user-management.md)。

量度是衡量。 在SQL和数据库结构中，量度就像变量时段内的存储查询。

在[!DNL Commerce Intelligence]中，您可以使用量度[创建图表](../../data-user/reports/ess-rpt-build-visual.md)。 例如，量度`revenue`是订单总数。 量度`average customer revenue per order`是客户每次订购的平均花费。

在报表中使用时，可以在指定的时间段内分析量度，并按不同类别筛选或分段[](../../best-practices/segment-filter.md)。 考虑分析按性别分组的平均客户收入，在此例中，`average customer revenue per order`是指标，性别是分组。

## 定义量度 {#define}

1. 要创建指标，请单击&#x200B;**[!UICONTROL Data** > **Metrics]**。

1. 单击&#x200B;**[!UICONTROL Create New Metric]**。

1. 从下拉列表中，单击包含要用于量度的本机列或计算列的表。

1. 命名您的量度。

   Adobe推荐的名称，只需一眼即可告知您该指标是什么。 例如： `Average Order Revenue`。

1. 下一步是定义量度的用途。 使用下拉菜单，定义量度的操作、`operation`列和`date`维度：

   * 选择操作：
      * `Count` — 此操作计算数据表中的行数
      * `Max` — 最大值返回特定数据列的最大值
      * `Min` - Min返回特定数据列的最小值
      * `Sum` — 此操作对特定数据列的值进行求和
      * `Average` — 此操作计算数据列值的平均值
      * `Count Distinct Value` — 这将计算特定数据列中的唯一值数
      * `Median` — 此操作计算数据列值的中位数
      * `First and Third Quartiles` — 这些操作分别计算数据列值的第25个百分位和第75个百分位
      * `Tenth and Ninetieth Percentiles` — 这些操作分别计算数据列值的第10个百分位和第90个百分位

   * 选择要对其执行操作的列。 例如，如果要查找总收入，应对`order total`列执行sum操作。

     如果您正在编辑现有量度，则还可以在此部分中[更改该量度的操作表](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md)。

   * 选择可用于显示量度趋势的日期维度。 例如，`order date`。

## 添加筛选器 {#filters}

`Filter`部分允许您创建筛选器或将[保存的筛选器集](../../data-user/reports/ess-manage-data-filters.md)应用于您的量度。

对于`average order revenue`量度，您不希望包含设置商店时可能完成的任何测试订单 — 这会给我们带来不准确的结果。 可以应用过滤器集以从数据集中删除这些订单。 创建过滤器后，该过滤器将应用于使用此量度构建的所有图表。

在`Filter Logic`部分中，您可以进一步定义量度应如何表现。

* “\[`A`\]或\[`B`\]”允许满足筛选器\[`A`\]或\[`B`\]的任何数据
* “\[`A`\]和\[`B`\]”仅允许同时满足筛选器\[`A`\]和\[`B`\]的数据
* “（\[`A`\]和\[`B`\]）或\[`C`\]”仅允许同时满足筛选器\[`A`\]和\[`B`\]的数据，或者仅满足筛选器\[`C`\]的数据

## 添加Dimension {#dimensions}

[`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md)部分显示所有可用于筛选或分组的数据维度；默认情况下，所有可用数据列将作为维度列出。 继续此示例，如果您想按反向链接来源划分收入，可以在此处执行此操作。

除了将所有可用数据列作为维度列出外，[!DNL Commerce Intelligence]还猜测列可分组。 *要将报表*&#x200B;上的数据分段或分组，列必须标记为可分组。

## 正在完成 {#finish}

除了定义量度的行为方式之外，您还可以在`User Rights`部分中设置权限级别。 虽然`Admin`用户有权访问所有量度，但必须通过选中相应组旁边的框来指示可以使用此量度的用户。

如果您正在编辑现有量度，则可以在`Dependent Charts`部分中查看使用此量度的图表（以及这些图表的拥有者）的列表。

更改会自动保存，您的量度现已准备就绪。
