---
title: 使用可视化Report Builder
description: 了解如何分析报表中特定时间段的数据。
exl-id: da97b63d-63f0-4fd6-87e3-4cac49a42acc
source-git-commit: df81d2b036d00cd53274ec1ae22031dbf06cc948
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# 使用 [!DNL Visual Report Builder]

此 [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) 允许您以可视方式浏览数据，从而获取见解并帮助制定业务决策。 本教程将指导您完成创建基本报表的过程。

>[!NOTE]
>
>要将报告添加到功能板，您需要 `Standard` [用户权限](../administrator/user-management/user-management.md) 和 `Edit` 对仪表板的访问权限。

## 步骤1：创建报告

要开始创建报告，请单击 **[!UICONTROL Report Builder]** 在侧栏上或 **[!UICONTROL Add Report]** 位于任何仪表板的顶部。 当 `Report Builder` 页面时，单击 **[!UICONTROL Visual Report Builder]** 选项。

编辑在中创建的报告 [!DNL Visual Report Builder]中，单击任意图表右上角的齿轮（选项）图标，然后单击 **[!UICONTROL Edit]**.

## 步骤2：添加量度

创建分析的第一步是选择 [量度](../data-user/reports/ess-manage-data-metrics.md) 以进行分析。 虽然量度默认按字母顺序列出，但您也可以按支持该量度的表对它们进行分组。

您可以在选择初始量度后添加其他量度，并将所有量度叠加在单个报表上，或通过添加公式执行多量度计算。

## 步骤3：添加 `Formulas`

`Formulas` 通过单击添加到报表 **[!UICONTROL Add Formula]**，位于报表中量度列表的正上方。 在 [公式编辑器](../data-analyst/dev-reports/formulas-in-rpt-bldr.md)，则报表中包含的任何指标都可用作输入。 基本数学运算符用于处理不同的量度。

假设您要创建一个报表，向我们显示每订单的平均收入。 在这种情况下，您将 `Revenue` 量度依据 `Number of orders` 量度。

![](../assets/ave-rev-per-order.png)

## 步骤4：设置 `Time Period` 和 `Interval of Analysis` {#time}

要将某个特定时间段的值设为0，则可以设置分析的时间段。 您还可以选择时间间隔来按数据分段（例如，按年、按季度或按月）。 使用图表右上角的菜单设置时段和间隔。

![](../assets/Time_Options_Report_Builder.png)

为时间段设置特定日期范围时，请确保开始日期在时间间隔的开始日期，结束日期在时间间隔的结束日期。

例如，设置时间段 `January 1st` 到 `March 1st` 并选择一个 `monthly` 间隔显示 `March` 作为数据点，但忽略中的每一天 `March` 排除 `March 1`. 在这种情况下，您应该将 `Time Period` 起始日期 `January 1 to March 31`.

## 步骤5： `Group by` / `Segmenting the Analysis` {#groupby}

[按数据维度划分量度](../best-practices/segment-filter.md)，单击 **[!UICONTROL Group by]** 菜单的位置。 这会显示一个下拉列表，其中包含列表中包含的第一个量度的所有可用维度。

您可以选择 `None` 以防止对量度进行分段。 例如，您可能希望有一个指标返回总收入但不进行分段，而让另一个收入指标按区域分段。

返回每个订单示例的平均收入，并将分组方式设置为促销代码。 这显示了使用和不使用促销代码的订单的每订单平均收入。

![](../assets/Group_By_Report_Builder.png)

如果分析中包含的量度基于不同的数据表构建，则通过弹出窗口可在每个表中选择匹配的数据维度。 此处的目标是找到共享分段值类型的维度：

![](../assets/Dimension_Editor.png)

## 步骤6：设置 `Metric Filters`， `Perspective`、和 `Time Interval` {#metric-specific}

对于添加到分析的每个量度，您可以添加过滤器，选择相关数据透视，然后设置 `time interval` 选项。 要访问这些功能，请单击漏斗(`Filter`)，眼睛(`Perspective`)和时钟(`Time`)图标，这些图标位于报表中包含的量度旁边。

![](../assets/Filters_Perspective_Interval_Report_builder.png)

### `Filters`

`Filters` 限制分析中包含的数据集。 例如，在评估各个客户获取渠道和删除离群值时，过滤器非常有用。

除了下拉菜单和文本框之外，您还可以使用特殊的过滤器运算符，例如 `LIKE` 或 `IN` 以创建过滤器。

使用通配符(`%` 或 `_`)，替换为 `LIKE` 语句受支持。 此 `%` 通配符匹配多个字符，而 `_` 仅匹配任意单个字符。 例如：

- `affiliate's name Like B%` 仅允许来自名称以开头的客户的数据 `B`.

- `affiliate's name Like _ake` 仅允许来自名称类似于 `Jake`， `Rake`，或 `Bake` 但不是 `Drake` 或 `Blake`.

添加多个筛选器可严格控制图表数据。 默认情况下，对于要包含的数据段，所有筛选条件都必须为true，但您可以通过编辑“筛选规则”文本框来创建OR关系。

![](../assets/edit-filter-rules.png)

### `Perspectives`

`Perspectives` 允许您轻松地在不同的数据视图之间进行切换。 查看可用内容：

- `Standard perspective`：标准透视在x轴上显示匹配日期的结果（例如，一月收入）。 这是您在每个订单的平均收入示例中使用的透视。

![](../assets/Standard.png)

- `Amount` 或 `Percent Change` 对比 `Previous Period` 透视：此透视图显示从一个间隔到下一个间隔的更改量或更改百分比，可用于测量快速变化的量度中的更改率。 还有一种观点认为，应将这一时间间隔与去年同期进行比较，以显示年同比增长率。

![](../assets/Amt_or_Percent_Change.png)

- `Cumulative perspective`：此 `cumulative perspective` 显示指标在相应时段内的持续或累计总和。 这通常用于分析总客户并规划未来容量。

![](../assets/Cumulative_Perspective.png)

- `Percent of First Value perspective`：此透视以分析中包含的首次时间间隔的百分比显示数据。 这有助于衡量特定操作相对于第一期性能的有效性。

![](../assets/Percent_of_First_Value.png)

- `Rolling averages window perspective`：滚动平均窗口透视显示指定时间范围内量度的滚动平均值。 间隔必须与在报告级别设置的间隔相同。 例如，如果报表按周显示收入的最后一个完整季度，您可以将滚动平均窗口时间范围设置为四周。 这使得前三个值为空，第四个值表示收入前四周的平均值。 为清楚起见，请务必关闭 `Multiple Y-Axes` 复选框。

![](../assets/rolling_avg_window.png)

### 特定于指标的时间选项

报表中使用的量度有两个选项：它们可以根据全局时间选项随时间推移显示趋势，也可以不随时间推移显示趋势，这些选项会将它们显示为标量数字。

将量度时间间隔更改为 `None` 返回 `scalar` 数字，在创建涉及将时间趋势量度除以 `scalar` 数字。 此外，您还可以更改 `scalar` 量度到与报表的时间范围无关的时间范围。

例如，假设您希望看到2019年的月收入在2019年总收入中所占的百分比。 您可以添加两个 `Revenue` 全局时间范围为2019年1月1日至2019年12月31日的报表的量度，按月间隔分段。

>[!NOTE]
>
>如果添加 `group by` 维度、选择新可视化图表或调整时间间隔，然后仅保存数字(`scalar`)。 下次从仪表板打开该报表时，不会保留这些调整，而只会保留时间范围。

要了解有关在报表中使用时间选项的更多信息，请参阅此 [教程](../tutorials/time-options-visual-rpt-bldr.md).

## 步骤7：保存报表

创建图表时，可通过单击 **[!UICONTROL Save]** 位于的右上角 `Visual Report Builder`.

您可以选择保存图表、表或数字(`scalar`)使用 `Type` 下拉列表以及报告应保存到的功能板 `Location` 下拉菜单。

然后，您可以通过单击 **[!UICONTROL Save to Dashboard]**.

![](../assets/save-to-dashboard.png)

## 报告输出

要帮助您确定选择哪个报表输出，请参阅以下内容：

### 图表

![](../assets/RB_Chart.png)

### 表

![](../assets/RB_Table.png)

### 数字(`scalar`)

![](../assets/RB_Scalar.png)

恭喜！ 你完了。
