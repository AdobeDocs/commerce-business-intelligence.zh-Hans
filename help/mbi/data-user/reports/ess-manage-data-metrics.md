---
title: 创建量度
description: 了解如何使用量度创建图表。
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# 创建量度

>[!NOTE]
>
>需要 [管理员权限](../../administrator/user-management/user-management.md).

简而言之，量度就是一种测量。 在SQL和数据库结构中，量度与在变量时间段内的存储查询类似。

在 [!DNL MBI]，则可以将量度用于 [创建图表](../../data-user/reports/ess-rpt-build-visual.md). 例如，量度 `revenue` 是订单总额。 量度 `average customer revenue per order` 是客户每次订购的平均花费。

在报表中使用时，可以在指定的时间段内分析量度，并 [已过滤或已分段](../../best-practices/segment-filter.md) 不同类别。 考虑分析按性别划分的平均客户收入，在本例中， `average customer revenue per order` 是量度，性别是分组。

## 定义量度 {#define}

1. 要创建新量度，请单击 **[!UICONTROL Data** > **Metrics]**.

1. 单击 **[!UICONTROL Create New Metric]**.

1. 从下拉菜单中，单击包含要用于量度的本机或计算列的表。

1. 命名您的量度。

   我们建议您使用一个名称，以便一目了然地了解量度的含义。 例如： `Average Order Revenue`.

1. 下一步是定义量度的用途。 使用下拉菜单，定义量度的操作， `operation` 列和 `date` 维度：

   * 选择一个工序：
      * `Count`  — 此操作计算数据表的行数
      * `Max` - Max返回特定数据列的最大值
      * `Min` - Min返回特定数据列的最小值
      * `Sum`  — 此操作对特定数据列的值求和
      * `Average`  — 此操作计算数据列值的平均值
      * `Count Distinct Value`  — 此值计算特定数据列中唯一值的数量
      * `Median`  — 此操作计算数据列值的中值
      * `First and Third Quartiles`  — 这些运算分别计算数据列值的第25和第75个百分比
      * `Tenth and Ninetieth Percentiles`  — 这些操作分别计算数据列值的第10和第90个百分位值
   * 选择要对其执行操作的列。 例如，如果要查找总收入，则对 `order total` 列。

      如果您正在编辑现有量度，则还可以 [更改量度的操作表](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) 在此部分中。

   * 选择可用于趋势化量度的日期维度。 例如， `order date`.


## 添加过滤器 {#filters}

的 `Filter` 部分，以创建新过滤器或应用 [保存的过滤集](../../data-user/reports/ess-manage-data-filters.md) 到您的量度。

对于我们的 `average order revenue` 量度中，我们不希望包含在设置商店时可能已执行的任何测试订单 — 这会给我们带来不准确的结果。 我们可以应用过滤器集以从数据集中删除这些订单。 创建过滤器后，该过滤器将应用于使用此量度构建的所有图表。

的 `Filter Logic` 部分中，您可以进一步定义量度的行为方式。

* &quot;\[&quot;`A`\]或\[`B`“ \]”将允许满足过滤器\[的任何数据`A`\]或\[`B`\]
* &quot;\[&quot;`A`\]和\[`B`“ \]”将仅允许满足两个过滤器的数据\[`A`\]和\[`B`\]
* &quot;(\[`A`\]和\[`B`\])或\[`C`“ \]”将仅允许满足两个过滤器的数据\[`A`\]和\[`B`\]或满足筛选器\[`C`\]单独

## 添加Dimension {#dimensions}

的 [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 部分显示所有可用数据维度，以便进行筛选或分组；默认情况下，所有可用数据列都将作为维度列出。 继续我们的示例，如果我们想要按推荐来源划分收入，我们可以在此处这样做。

除了将所有可用数据列作为维度列出外， [!DNL MBI] 还会猜测哪些列可分组。 *对报表数据进行分段或分组*，列必须标记为可分组。

## 完成 {#finish}

除了定义量度的行为方式之外，您还可以在 `User Rights` 中。 While `Admin` 用户有权访问所有量度，您必须通过选中相应群组旁边的复选框来指示可以使用此量度的用户。

如果您正在编辑现有量度，则可以在 `Dependent Charts` 中。

更改会自动保存，您的量度现已准备就绪。
