---
title: 可视化Report Builder中的可视化选项
description: 了解如何使用可视化Report Builder中的可视化选项。
exl-id: e42a004e-28e3-4484-bb5a-b58c810b23e0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1823'
ht-degree: 0%

---

# 可视化选项

为给定数据集选择正确的可视化图表是分析过程中的关键部分。 每个数据集都有一个故事要讲述，但该故事的效果通过其视觉影响和可读性得到强调。

[!DNL Commerce Intelligence] [!DNL Visual Report Builder]提供了12个不同的可视化选项，每个选项都有各自的优势和用例。 本主题讨论[!DNL Commerce Intelligence]中的各种可视化选项，包括所需的报表配置（如果适用）以及用例示例。 以下可视化图表在[!DNL Commerce Intelligence]中可用：

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

`Scalar`个报告显示为单个数字值。 大多数情况下，它用于显示关键量度（如收入或订单）的“所有时间”值，或者使用两个单独的标量报表比较迄今的收入与预算。 在下面的示例中，它只显示给定报告时间间隔内的订单总数：

![标量报告，将订单总数显示为单个数值](../../assets/blobid0.png)

要将报表另存为标量，请配置您的筛选器和时间设置，然后单击报表右上角的&#x200B;**[!UICONTROL Save]**&#x200B;或&#x200B;**[!UICONTROL Update]**。 在`Type`下拉列表下，选择数字：量度名称，以将报表另存为左侧栏上显示的值。

![保存报告对话框，其中的“类型”下拉菜单显示“数量度量名称”选项](../../assets/blobid1.png)

**要求**：

* `Time interval`： `None`
* `Group by`： `None`
* 仅一个量度

## `Table`

顾名思义，`table`报告非常适合显示表格详细信息。 当需要在单个报表中按值或量度显示多个组时，表格通常是最好的方法。 例如，下方是“客户详细信息”表，其中显示了按客户电子邮件分组的订单和收入：

![表报告，按客户电子邮件显示订单和收入的客户详细信息](../../assets/blobid2.png)

与标量报表类似，您可以通过在报表生成器中单击&#x200B;**[!UICONTROL Save]**&#x200B;或&#x200B;**[!UICONTROL Update]**，然后选择`Type`下拉列表下的表选项来将报表另存为表。

![保存报告对话框，其中的“类型”下拉菜单显示选定的“表”选项](../../assets/blobid3.png)

**要求：**

* 尽管没有报告配置要求，但请务必注意，表限制为3500行。 如果数据集包含3500行以上，您需要筛选结果以缩小范围，或者将结果导出到`.csv`或`Excel`以查看完整数据集。

## `Line`

`Line`图表是比较类似量度同类群组性能的完美选择。 例如，分析两个地区在相同时段的收入，或比较已履行订单的逐年增长，如下所示：

![折线图将两个量度在一段时间内与多个折线进行比较](../../assets/blobid0.png)

添加到报表的每个量度和公式由其自身的行表示。 在比较具有相似单位和比例的量度时，不要忘记清除`Multiple Y-Axes`的复选框，以便在同一比例显示所有量度。

要将报表另存为折线图，请将报表`Type`调整为`Chart`，然后从Report Builder中选择适当的可视化图表，如下所示：

![选定了图表类型并突出显示折线图可视化选项的Report Builder](../../assets/blobid1.png)

**要求：**

* 无

## `Bar`

`Bar`图表将数据显示为一系列水平条，最适合显示有限量度或按值分组的整体性能。 例如，可以使用条形图来按商店比较收入：

![显示商店收入比较的水平条形图](../../assets/blobid2.png)

每个不同的量度、分组依据和时间间隔组合都显示为自己的栏。 如果您的两个量度具有一个`group by`，包含三个不同的`group by`值，则报表会显示六个单独的栏。

要将报告另存为条形图，请将报告`Type`调整为`Chart`并选择`Bar`选项，如下所示：

![Report Builder选定的图表类型并突出显示条形图可视化选项](../../assets/blobid3.png)

**要求：**

* 无

## `Stacked Bar`

`Stacked bar`图表与其条形图兄弟类似，还能够显示每个条形的比例细分。 大多数情况下，栈叠条形图使用两个或多个量度和单个分组依据进行设置，以便每个条形表示按值划分的唯一分组，该值在其量度组成中拆分。

例如，以下报表具有两个相同的收入量度，其中一个量度针对首次订购进行过滤，另一个量度针对重复订购进行过滤。 按商店进行分组后，您可以看到每个商店的总收入贡献（由栏的总宽度表示）以及每个商店的首次与重复收入细分。

![按商店显示首次收入和重复收入的栈叠水平条形图](../../assets/blobid4.png)

设置如上所述的报告时，请确保取消选中`Multiple Y-Axes`框。

要将报表另存为栈叠条形图，请将报表`Type`调整为`Chart`并从Report Builder中选择栈叠条形选项：

![选定了图表类型并突出显示栈叠条形可视化选项的Report Builder](../../assets/blobid5.png)

**要求：**

* 无

## `Column`

`Column`图表将每个数据点表示为垂直列，并且比水平条形图可视化图表更适合显示时间趋势数据。 每个唯一的量度和按组合分组都表示为各自的一系列条形。 列报表最适合那些具有三个或更少量度或一个量度（只有一个组）的报表，因为它包含1-3个按值分组。

在下面的示例中，您看到两个收入量度，一个针对首次收入进行过滤，另一个针对重复收入，按月显示一段时间内的趋势：

![按月份显示首次收入和重复收入的垂直柱状图](../../assets/blobid6.png)

列报表可通过以下方式保存：将报表`Type`更改为`Chart`，并选择列可视化选项：

![选定图表类型并突出显示列可视化选项的Report Builder](../../assets/blobid7.png)

**要求：**

* 无

## `Stacked Column`

`Stacked column`个报表与柱形图几乎完全相同，不同之处在于相似的列彼此栈叠在一起，因此总高度表示值的总和。 栈叠的列再次通过有限数量的量度或组框实现最佳可视化。

使用上面`Column`部分中描述的相同报表配置，具有两个收入量度（首次过滤并重复）的报表将类似于下面的栈叠列可视化图表：

![按月份显示首次收入和重复收入的栈叠垂直柱状图](../../assets/blobid8.png)

同样，在通过栈叠列可视化显示多个量度时，`Multiple Y-Axes`复选框被清除也很重要。

要将报表另存为栈叠列，请将报表`Type`设置为`Chart`并选择`stacked column`选项：

![选定了图表类型且突出显示了栈叠列可视化选项的Report Builder](../../assets/blobid9.png)

**要求：**

* 无

## `Pie`

`Pie`图表最适合显示具有一个或多个组框的单个量度，或者显示没有组框的多个量度。 在任一情况下，时间间隔必须设置为无，才能在饼图中显示数据。 在下面的示例中，单个订单量度按商店名称分组，以显示按商店划分的订单：

![饼图显示按商店名称排列的订单分布](../../assets/blobid10.png)

要将报告另存为饼图，请将报告`Type`设置为`Chart`并选择`pie`选项，如下所示：

![选定了图表类型的Report Builder和突出显示的饼图可视化选项](../../assets/blobid11.png)

**要求：**

* `Time interval`： `None`
* 以下任一选项：
   * `Single metric with one or more group bys`
   * `Multiple metrics with no group bys`

## `Area`

`Area`图表几乎与栈叠柱形图相同，只是列连续显示。 与栈叠列类似，面积图通过有限数量的组框或量度实现最佳可视化。

以`stacked column`部分中的相同示例为例，以下报表使用面积图可视化图表显示首次收入与重复收入：

![显示一段时间内首次和重复收入趋势的面积图](../../assets/blobid12.png)

要将报告另存为面积图，请将`Type`调整为`Chart`并选择面积图选项：

![选定了图表类型的Report Builder和突出显示的面积图可视化选项](../../assets/blobid13.png)

**要求：**

* 无

## `Funnel`

`Funnel`图表非常适合用于可视化预期事件序列中的转化。 一些示例包括分析销售funnel中从商机到成交的潜在收入，或衡量客户在第一和第二订单、第二和第三订单之间的减少情况，等等。 后者的示例如下所示：

![Funnel图表，显示客户在顺序订单中的转化](../../assets/blobid4.png)

在funnel报表中，funnel给定步骤的相对值由步骤的高度反映。 报告配置确定步骤的显示顺序。 可通过两种方式配置funnel报表：

* `Single metric with one group by`： — 由分组依据的“显示顶部/底部”设置确定的步骤顺序。 默认情况下，funnel步骤按从最大值到最小值的顺序显示，但您也可以按名称的组按字母顺序对它们进行排序。

* `Multiple metrics with no group by`： — 步骤的顺序，由量度添加到报表的顺序决定。

要将报表另存为funnel图表，请将报表`Type`调整为`Chart`，然后从Report Builder中选择适当的可视化图表。

![选定图表类型并突出显示funnel可视化选项的Report Builder](../../assets/blobid5.png)

**要求：**

* `Time interval`： `None`
* 以下任一选项：
   * `Single metric with one group by`
   * `Multiple metrics with no group by`

## `Scatter plot`

`scatter plot`用于检查量度与两个不同变量的关系，以便轻松识别关联和离群值。 此类可视化图表最好仅与数值维度一起使用 — 尝试与订单量度以及`Customer's lifetime number of coupons`和`Customer's lifetime revenue`维度一起使用，以了解优惠券使用与收入的关系。 您可以选择使用或不使用趋势线的散点图：

![散点图显示客户量度之间的关系](../../assets/scatter-plot-1.png)

![无趋势线的散点图显示数据点分布](../../assets/scatter-plot-2.png)

![包含数据点和关联模式的散点图](../../assets/scatter-plot-3.png)

![趋势线散点图显示量度之间的相关性](../../assets/scatter-plot-4.png)

**要求：**

选项1：

* 两个`metrics`
* 一个`group by`
* `Time interval`： `None`

选项2：

* 两个`metrics`
* 无`group by`
* 设置`time interval`

## `Bubble`图表

`bubble`图表最多可显示四个维度的数据，其中`X`和`Y`轴指定气泡的位置。 `Z`轴是气泡的大小，通过包含两个组框，可以向气泡中添加颜色。 当要在单个图表中绘制多个数据维度时，最好使用此类型的可视化图表。

例如，下图显示了按特定客户获取源（气泡颜色）和状态（特定颜色的各种气泡）分组的客户数量（气泡大小），并按总收入和平均存留期订单绘制。

![气泡图，显示客户计数（按客户获取来源和状态）与收入和订单](../../assets/bubble-1.png)

下图显示了按客户获取源（气泡颜色）和状态（特定颜色的各种气泡）分组的客户数量（气泡大小），并根据平均生命周期值和总收入绘制。

![气泡图显示按客户获取来源和状态划分的客户量度](../../assets/bubble-2.png)

**单系列泡泡图的要求：**

选项1

* 三个`metrics`
* 一个`group by`
* `Time interval`： `None`

选项2

* 三个`metrics`
* 无`group by`
* 设置`time interval`

**多系列泡泡图的要求：**

* 三个`metrics`
* 两个`group by`
* `Time interval`： `None`

## `Heatmap`

使用`heatmaps`可视化数据中的热点。 例如，热图可指示您通常在何处获得更高的热量。 通过将此数据可视化，可以帮助您调整库存水平，确保满足高峰期需求。

以下热图显示几周内按星期几、按小时划分的订单总数。

![按星期和小时显示订单强度的热图](../../assets/heat-map.png)<!--{: width="650"}-->

**要求：**

选项1

* 一个`metric`
* 两个`group by`
* `Time interval`： `None`

选项2

* 一个`metric`
* 一个`group by`
* 设置`time interval`
