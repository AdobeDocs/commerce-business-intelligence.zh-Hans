---
title: 可视化Report Builder中的可视化选项
description: 了解如何使用可视化Report Builder中的可视化选项。
exl-id: e42a004e-28e3-4484-bb5a-b58c810b23e0
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 0%

---

# 可视化选项

为给定数据集选择正确的可视化是分析过程中的一个关键环节。 每个数据集都有一个故事要讲述，但故事的效果以其视觉冲击和可读性来强调。

的 [!DNL MBI] `Visual Report Builder` 提供了12个不同的可视化选项，每个选项都有各自的优势和用例。 本文介绍了 [!DNL MBI]，包括所需的报表配置（如果适用）以及用例示例。 MBI中提供了以下可视化图表：

* `Scalar`
* `Table`
* `Line`
* `Bar`
* `Stacked Bar`
* `Column`
* `Stacked Column`
* `Pie`
* `Area`
* `Funnel`
* `Scatter plot`
* `Bubble`
* `Heatmap`

## `Scalar`

`Scalar` 报表显示为单个数字值。 通常，它用于显示关键量度（如收入或订单）的“所有时间”值，或通过两个单独的标量报表来比较收入与预算的当前日期值。 在以下示例中，它只显示给定报表间隔的订单总数：

![](../../assets/blobid0.png)

要将报表另存为标量，请配置过滤器和时间设置，然后单击 **[!UICONTROL Save]** 或 **[!UICONTROL Update]** 报表右上方的。 在 `Type` 下拉列表中，选择“数字：用于将报表另存为左侧栏中显示的值的量度名称。

![](../../assets/blobid1.png)

**要求**:

* `Time interval`: `None`
* `Group by`: `None`
* 仅一个量度

## `Table`

正如名字所暗示的， `table` 报表非常适合显示表格详细信息。 当需要在单个报表中显示大量按值或量度划分的群组时，通常最好使用表格。 例如，下面是“客户详细信息”表，其中显示了按客户电子邮件分组的订单和收入：

![](../../assets/blobid2.png)

与标量报表类似，您可以通过单击 **[!UICONTROL Save]** 或 **[!UICONTROL Update]** ，然后选择 `Type` 下拉列表。

![](../../assets/blobid3.png)

**要求：**

* 尽管没有报表配置要求，但请务必注意，表的行数限制为3500。 如果数据集包含的行数超过3500，则需要筛选结果以缩小范围，或将结果导出到 `.csv` 或 `Excel` 以查看完整数据集。

## `Line`

`Line` 图表是比较相似量度同类群组性能的最佳选择。 例如，分析同一时间段内两个地区的收入，或比较已履行订单的年同比增长，如下所示：

![](../../assets/blobid0.png)

添加到报表的每个量度和公式由其自己的行表示。 在比较具有相似单位和缩放的量度时，请不要忘记清除 `Multiple Y-Axes` 以显示同一比例的所有量度。

要将报表另存为折线图，请调整报表 `Type` to `Chart`，然后从报表生成器中选择相应的可视化，如下所示：

![](../../assets/blobid1.png)

**要求：**

* 无

## `Bar`

`Bar` 图表以一系列水平条的形式显示您的数据，最适合显示有限数量的量度或按值分组的整体性能。 例如，可使用条形图来按商店比较收入：

![](../../assets/blobid2.png)

每个不同的量度、分组依据和时间间隔组合都显示为其自己的栏。 如果您有两个量度，其中一个 `group by`，包含三个不同的 `group by` 值时，您的报表将显示六个单独的栏。

要将报表另存为条形图，请调整报表 `Type` to `Chart` ，然后选择 `Bar` 选项，如下所示：

![](../../assets/blobid3.png)

**要求：**

* 无

## `Stacked Bar`

`Stacked bar` 图表与其条形图组相似，具有显示每个条形图按比例划分的额外功能。 大多数情况下，堆叠式条形图由两个或多个量度和单个分组依据设置，以便每个条形表示一个按值划分的唯一分组依据值，该分组依据其量度构成部分。

例如，以下报表具有两个相同的收入量度：一个是首次过滤订单，另一个是过滤重复订单。 在按商店进行分组后，您可以看到每个商店的总收入贡献（由条的总宽度表示）以及每个商店的收入第一次划分和重复划分：

![](../../assets/blobid4.png)

确保 `Multiple Y-Axes` 框中，此复选框将在设置类似上述报表时处于未选中状态。

要将报表另存为堆叠条形图，请调整报表 `Type` to `Chart` ，然后从报表生成器中选择堆叠条形图选项：

![](../../assets/blobid5.png)

**要求：**

* 无

## `Column`

`Column` 图表将每个数据点表示为垂直列，通常比水平条形图可视化图表更适合显示时间趋势数据。 由于每个独特量度和按组合分组在其自己的一系列栏中表示，因此列报表通常最适合具有三个或更少量度的报表，或者一个具有单个组的量度（通过按值包含1-3组）。

在以下示例中，我们显示了两个收入量度，一个是首次过滤收入，另一个是重复收入，按月显示一段时间的趋势：

![](../../assets/blobid6.png)

可通过更改报表来保存列报表 `Type` to `Chart`，然后选择列可视化选项：

![](../../assets/blobid7.png)

**要求：**

* 无

## `Stacked Column`

`Stacked column` 报表与柱状图几乎完全相同，只是相似的列彼此堆叠在一起，以使总高度代表值的总和。 堆叠的列同样最好以有限数量的量度或组行显示。

使用与 `Column` 在上面的部分中，包含两个收入量度（首次过滤并重复）的报表将类似于下面的堆叠列可视化图表：

![](../../assets/blobid8.png)

同样，重要的是 `Multiple Y-Axes` 当使用堆叠的列可视化显示多个量度时，复选框会被清除。

要将报表另存为堆叠列，请设置报表 `Type` to `Chart` ，然后选择 `stacked column` 选项：

![](../../assets/blobid9.png)

**要求：**

* 无

## `Pie`

`Pie` 图表最适合显示一个具有一个或多个组by的量度，或多个不具有组by的量度。 无论哪种情况，要在饼图中显示数据，必须将时间间隔设置为无。 在以下示例中，单个订单量度按商店名称分组，以显示按商店划分的订单数：

![](../../assets/blobid10.png)

要将报表另存为饼图，请设置报表 `Type` to `Chart` ，然后选择 `pie` 选项，如下所示：

![](../../assets/blobid11.png)

**要求：**

* `Time interval`: `None`
* 以下任一项：
   * `Single metric with one or more group bys`
   * `Multiple metrics with no group bys`

## `Area`

`Area` 图表与堆叠的柱状图几乎完全相同，只是列会连续显示。 与堆叠列类似，面积图最好以有限数量的组基准或量度来显示。

从 `stacked column` 区域图可视化图表显示了首次与重复收入的对比情况：

![](../../assets/blobid12.png)

要将报表另存为面积图，请调整 `Type` to `Chart` ，然后选择区域选项：

![](../../assets/blobid13.png)

**要求：**

* 无

## `Funnel`

`Funnel` 图表非常适合在预期事件序列中显示转化。 例如，分析销售漏斗中潜在的收入（从商机到完成交易），或测量客户在第一次和第二次订单、第二次和第三次订单之间的下降，等等。 后者的示例如下所示：

![](../../assets/blobid4.png)

在漏斗报表中，漏斗的给定步骤的相对值由步骤的高度反映，而步骤的显示顺序则由报表配置决定。 有两种方法可配置漏斗报表：

* `Single metric with one group by`: — 由组的“显示顶部/底部”设置确定的步骤顺序。 默认情况下，漏斗步骤按从最大值到最小值的顺序显示，但您也可以按名称按组的字母顺序进行排序。

* `Multiple metrics with no group by`: — 由量度添加到报表的顺序决定的步骤顺序。

要将报表另存为漏斗图，请调整报表 `Type` to `Chart` ，然后从报表生成器中选择相应的可视化。

![](../../assets/blobid5.png)

**要求：**

* `Time interval`: `None`
* 以下任一项：
   * `Single metric with one group by`
   * `Multiple metrics with no group by`

## `Scatter plot`

A `scatter plot` 用于检查量度与两个不同变量的关系，以便您能够轻松识别关联和离群值。 此类可视化图表最好仅用于数值维度 — 尝试使用订单量度和 `Customer's lifetime number of coupons` 和 `Customer's lifetime revenue` 维度以了解优惠券使用与收入的关系。 您可以在具有或没有趋势线的散点图之间进行选择：

![](../../assets/scatter-plot-1.png)

![没有趋势线](../../assets/scatter-plot-2.png)

![](../../assets/scatter-plot-3.png)

![使用趋势线](../../assets/scatter-plot-4.png)

**要求：**

选项1:

* 两个 `metrics`
* 一个 `group by`
* `Time interval`: `None`

选项2:

* 两个 `metrics`
* 否 `group by`
* 已设置 `time interval`

## `Bubble` 图表

A `bubble` 图表最多可显示四个维度的数据，其中 `X` 和 `Y` 轴指定气泡的位置， `Z` 轴是气泡的大小，通过包含两个组by，可以向气泡添加颜色。 当您想要在单个图表中绘制多个数据维度时，最好使用此类可视化。

例如，下图显示按特定客户获取源（气泡颜色）和状态（特定颜色的各种气泡）分组的客户数量（气泡大小），根据总收入和平均生命周期订单进行标绘。

![](../../assets/bubble-1.png)

下图显示按客户获取源（气泡颜色）和状态（特定颜色的各种气泡）分组的客户数量（气泡大小），根据平均生命周期值和总收入绘制。

![](../../assets/bubble-2.png)

**单系列泡泡图的要求：**

选项1

* 三 `metrics`
* 一个 `group by`
* `Time interval`: `None`

选项2

* 三 `metrics`
* 否 `group by`
* 已设置 `time interval`

**多系列泡泡图的要求：**

* 三 `metrics`
* 两个 `group by`
* `Time interval`: `None`

## `Heatmap`

使用 `heatmaps` 可视化数据中的热点。 例如，热图可指示您经常从何处获得较大音量。 显示此数据可帮助您调整库存水平，以确保在这些高峰时段满足需求。

以下热图按每周的某一天（每天的某一小时）总计显示几周内的订单。

![](../../assets/heat-map.png)<!--{: width="650"}-->

**要求：**

选项1

* 一个 `metric`
* 两个 `group by`
* `Time interval`: `None`

选项2

* 一个 `metric`
* 一个 `group by`
* 已设置 `time interval`
