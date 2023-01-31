---
title: 使用可视Report Builder
description: 了解如何分析报表中特定时间段的数据。
exl-id: da97b63d-63f0-4fd6-87e3-4cac49a42acc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 0%

---

# 使用 `Visual Report Builder`

的 [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md) 让您能够直观地浏览数据，以获得洞察并帮助推动业务决策。 本教程将指导您完成创建基本报告的过程。

>[!NOTE]
>
>要向功能板添加报表，您需要 `Standard` [用户权限](../administrator/user-management/user-management.md) 和 `Edit` 访问功能板。

## 步骤1:创建报表

要开始创建新报告，请单击 **[!UICONTROL Report Builder]** 在侧栏或 **[!UICONTROL Add Report]** 的双曲正切值。 当 `Report Builder` 选择页面，单击 **[!UICONTROL Visual Report Builder]** 选项。

编辑在 `Visual Report Builder`，单击任意图表右上角的齿轮（选项）图标，然后单击 **[!UICONTROL Edit]**.

## 步骤2:添加量度

创建分析的第一步是选择 [量度](../data-user/reports/ess-manage-data-metrics.md) 分析。 虽然量度默认按字母顺序列出，但您也可以按为量度提供支持的表格对它们进行分组。

您可以在选择初始量度后添加其他量度，并将所有量度叠加到单个报表上，或通过添加公式来执行多量度计算。

## 步骤3:添加 `Formulas`

`Formulas` 通过单击 **[!UICONTROL Add Formula]**，位于报表量度列表的上方。 在 [公式编辑器](../data-analyst/dev-reports/formulas-in-rpt-bldr.md)，报表中包含的任何量度均可用作输入。 基本数学运算符用于处理不同的量度。

假设我们想要创建一个报表来显示每次订购的平均收入。 在这种情况下，我们将 `Revenue` 量度 `Number of orders` 量度。

![](../assets/ave-rev-per-order.png)

## 步骤4:设置 `Time Period` 和 `Interval of Analysis` {#time}

若要将时间集中到特定时段，您可以设置分析的时间段。 您还可以选择时间间隔来对数据进行分段（例如，按年、按季度或按月）。 使用图表右上角的菜单设置时间段和间隔。

![](../assets/Time_Options_Report_Builder.png)

在设置时间段的特定日期范围时，请确保开始日期在间隔的开头，结束日期在间隔的结尾。

例如，设置 `January 1st to March 1st` 选择 `monthly` 显示间隔 `March` 作为数据点，但会在 `March` 除外 `March 1`. 在这种情况下，您应该 `Time Period` 从 `January 1 to March 31`.

## 步骤5: `Group by` / `Segmenting the Analysis` {#groupby}

[按数据维度对量度进行分段](../best-practices/segment-filter.md)，请单击 **[!UICONTROL Group by]** 菜单。 这将显示一个下拉列表，其中包含列表中第一个量度的所有可用维度。

您可以选择 `None` 来防止量度被分段。 例如，您可能希望某个量度在不进行分段的情况下返回总收入，而另一个收入量度则按区域进行分段。

返回到我们的每次订购平均收入示例，并将“分组依据”设置为促销代码。 这将显示包含和不包含促销代码的订单的每次平均收入。

![](../assets/Group_By_Report_Builder.png)

如果分析中包含的量度是基于不同的数据表构建的，则会显示一个弹出窗口，允许您在每个表中选择匹配的数据维度。 此处的目标是查找共享相同类型值的维度以进行分段：

![](../assets/Dimension_Editor.png)

## 步骤6:设置 `Metric Filters`, `Perspective`和 `Time Interval` {#metric-specific}

对于添加到分析的每个量度，您可以添加过滤器，选择相关数据透视，然后设置 `time interval` 选项。 要访问这些功能，请单击漏斗(`Filter`)，眼睛(`Perspective`)和时钟(`Time`)图标。

![](../assets/Filters_Perspective_Interval_Report_builder.png)

### `Filters`

`Filters` 限制分析中包含的数据集。 例如，在评估单个客户获取渠道和删除离群值时，过滤器非常有用。

除了下拉菜单和文本框之外，您还可以使用特殊的过滤器运算符，例如 `LIKE` 或 `IN` 创建过滤器。

使用通配符(`%` 或 `_`)与 `LIKE` 支持语句。 的 `%` 通配符将匹配多个字符，而 `_` 将仅匹配任何单个字符。 例如：

- `affiliate's name Like B%` 将仅允许名称以开头的客户的数据 `B`.

- `affiliate's name Like _ake` 将仅允许名称类似于 `Jake`, `Rake`或 `Bake` 但不是 `Drake` 或 `Blake`.

添加多个过滤器可严格控制图表数据。 默认情况下，要包含一段数据，所有筛选条件都必须为true，但您可以通过编辑“筛选规则”文本框来创建OR关系。

![](../assets/edit-filter-rules.png)

### `Perspectives`

`Perspectives` 允许您轻松地在数据的不同视图之间切换。 让我们看一看可用的功能：

- `Standard perspective`:标准透视图显示x轴上匹配日期的结果（例如1月的收入）。 这是我们在每个订单的平均收入示例中所使用的视角。

![](../assets/Standard.png)

- `Amount` 或 `Percent Change` 与 `Previous Period` 透视：此透视图显示从一个间隔到下一个间隔的变化量或百分比，并且有助于测量快速变化量度的变化率。还有一个透视图将这一间隔与去年的同一时间段进行比较，以显示逐年增长。

![](../assets/Amt_or_Percent_Change.png)

- `Cumulative perspective`:的 `cumulative perspective` 显示该时间段内量度的持续或累计总和金额。 它通常用于分析总客户和规划未来容量。

![](../assets/Cumulative_Perspective.png)

- `Percent of First Value perspective`:此视角显示数据在分析中包含的第一个时间间隔的百分比。 这有助于衡量特定操作相对于第一周期性能的有效性。

![](../assets/Percent_of_First_Value.png)

- `Rolling averages window perspective`:滚动平均值窗口透视显示指定时间范围内量度的滚动平均值。 间隔必须与在报表级别设置的间隔相同。 例如，如果报表按周显示收入的最后一个完整季度，则可以将滚动平均窗口时间范围设置为4周，且前三个值将为null，而第四个值表示收入前4周的平均值。 为清楚起见，请确保关闭 `Multiple Y-Axes` 复选框。

![](../assets/rolling_avg_window.png)

### 量度特定的时间选项

报表中使用的量度有两个选项：它们可以根据全局时间选项（或不根据全局时间选项）随时间呈现趋势，这些选项将显示为标量数。

将量度时间间隔更改为 `None` 返回 `scalar` 数值，在创建涉及将时间趋势量度除以 `scalar` 数字。 此外，您还可以更改 `scalar` 量度与报表的时间范围无关。

例如，我们希望看到2019年月收入占2019年总收入的百分比。 我们可以添加 `Revenue` 量度，其全局时间范围为2019年1月1日至2019年12月31日，按月间隔分段。

>[!NOTE]
>
>如果添加 `group by` 维度，选择新的可视化，或调整时间间隔，然后只保存数字(`scalar`)，则下次从功能板打开该报表时，不会保留这些调整 — 只保留时间范围。

要了解有关在报表中使用时间选项的更多信息，请参阅此 [教程](../tutorials/time-options-visual-rpt-bldr.md).

## 步骤7:保存报表

创建新图表时，可通过单击 **[!UICONTROL Save]** 的右上角 `Visual Report Builder`.

您可以选择保存图表、表格或数字(`scalar`) `Type` 下拉菜单和应将报表保存到的功能板 `Location` 下拉列表。

然后，您可以通过单击 **[!UICONTROL Save to Dashboard]**.

![](../assets/save-to-dashboard.png)

## 报表输出

要帮助您确定要选择的报表输出，请参阅以下内容：

### 图表

![](../assets/RB_Chart.png)

### 表

![](../assets/RB_Table.png)

### 数字(`scalar`)

![](../assets/RB_Scalar.png)

恭喜！ 你完了。
