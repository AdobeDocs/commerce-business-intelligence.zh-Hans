---
title: 使用可视化Report Builder
description: 了解如何分析报告中特定时间段的数据。
exl-id: da97b63d-63f0-4fd6-87e3-4cac49a42acc
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# 使用[!DNL Visual Report Builder]

[[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md)允许您直观地浏览数据，以得出见解并帮助制定业务决策。 本教程将指导您完成创建基本报表的过程。

>[!NOTE]
>
>要将报告添加到仪表板，您需要`Standard` [用户权限](../administrator/user-management/user-management.md)和`Edit`对仪表板的访问权限。

## 步骤1：创建报告

要开始创建报告，请单击侧边栏上的&#x200B;**[!UICONTROL Report Builder]**&#x200B;或任何仪表板顶部的&#x200B;**[!UICONTROL Add Report]**。 显示`Report Builder`页时，单击&#x200B;**[!UICONTROL Visual Report Builder]**&#x200B;选项。

要编辑在[!DNL Visual Report Builder]中创建的报表，请单击任意图表右上角的齿轮（选项）图标，然后单击&#x200B;**[!UICONTROL Edit]**。

## 步骤2：添加量度

创建分析的第一步是选择要分析的[指标](../data-user/reports/ess-manage-data-metrics.md)。 虽然量度默认按字母顺序列出，但您也可以按照支持该量度的表对它们进行分组。

选择初始量度后，您可以添加其他量度，并将所有量度叠加在单个报表中，或通过添加公式来执行多量度计算。

## 步骤3：添加`Formulas`

通过单击位于报表中量度列表正上方的&#x200B;**[!UICONTROL Add Formula]**，可将`Formulas`添加到报表中。 在[公式编辑器](../data-analyst/dev-reports/formulas-in-rpt-bldr.md)中，报表中包含的任何量度都可用作输入。 基本数学运算符用于处理不同的量度。

假设您要创建一个报表，向我们显示每订单的平均收入。 在这种情况下，您应该将`Revenue`指标除以`Number of orders`指标。

![](../assets/ave-rev-per-order.png)

## 步骤4：设置`Time Period`和`Interval of Analysis` {#time}

要针对特定的时间段设置零值，可以设置分析的时间段。 您还可以选择时间间隔以分段数据（例如，按年、按季度或按月）。 使用图表右上角的菜单设置时间段和间隔。

![](../assets/Time_Options_Report_Builder.png)

在为时间段设置特定日期范围时，请确保开始日期位于间隔的开始日期，结束日期位于间隔的结束日期。

例如，设置从`January 1st`到`March 1st`的时间段并选择`monthly`间隔会将`March`显示为数据点，但在`March`中忽略除`March 1`之外的每一天。 在这种情况下，您应该从`January 1 to March 31`中生成您的`Time Period`。

## 步骤5：`Group by` / `Segmenting the Analysis` {#groupby}

[要按数据维度对量度进行分段](../best-practices/segment-filter.md)，请单击图表左上角的&#x200B;**[!UICONTROL Group by]**&#x200B;菜单。 这会显示一个下拉列表，其中包含列表中包含的第一个量度的所有可用维度。

您可以选择`None`以防止对量度进行分段。 例如，您可能希望有一个量度在返回总收入时不被分段，同时让另一个收入量度按区域分段。

返回每个订单的平均收入，并将分组依据设置为促销代码。 这显示了使用和不使用促销代码的订单的每订单平均收入。

![](../assets/Group_By_Report_Builder.png)

如果分析中包含的量度基于不同的数据表构建，则通过弹出窗口可在每个表中选择匹配的数据维度。 此处的目标是查找共享分段值类型的维度：

![](../assets/Dimension_Editor.png)

## 步骤6：设置`Metric Filters`、`Perspective`和`Time Interval` {#metric-specific}

对于添加到分析的每个量度，您可以添加过滤器、选择相关数据透视并设置`time interval`选项。 要访问这些功能，请单击位于报告中所包含量度旁边的漏斗(`Filter`)、眼睛(`Perspective`)和时钟(`Time`)图标。

![](../assets/Filters_Perspective_Interval_Report_builder.png)

### `Filters`

`Filters`限制分析中包含的数据集。 例如，在评估各个客户获取渠道和删除离群值时，过滤器非常有用。

除了下拉菜单和文本框之外，您还可以使用特殊的筛选器运算符（如`LIKE`或`IN`）来创建筛选器。

支持将通配符（`%`或`_`）与`LIKE`语句一起使用。 `%`通配符匹配多个字符，而`_`仅匹配任何单个字符。 例如：

- `affiliate's name Like B%`仅允许来自名称以`B`开头的客户的数据。

- `affiliate's name Like _ake`仅允许来自名称类似于`Jake`、`Rake`或`Bake`的客户的数据，但不允许`Drake`或`Blake`的数据。

添加多个筛选器可严格控制图表数据。 默认情况下，对于要包含的数据段，所有过滤条件都必须为true，但您可以通过编辑“过滤规则”文本框来创建OR关系。

![](../assets/edit-filter-rules.png)

### `Perspectives`

`Perspectives`允许您轻松地在不同的数据视图之间切换。 查看可用内容：

- `Standard perspective`：标准透视在x轴上显示匹配日期的结果（例如1月的收入）。 这是您在每个订单的平均收入示例中使用的透视。

![](../assets/Standard.png)

- `Amount`或`Percent Change`与`Previous Period`透视：此透视图显示从一个间隔到下一个间隔的量或百分比变化，可用于测量快速变化的量度中的变化率。 还有一个视角来比较这一间隔与去年同期的情况，以显示年同比的增长。

![](../assets/Amt_or_Percent_Change.png)

- `Cumulative perspective`： `cumulative perspective`显示量度在某个时段内的持续或累积总和。 这通常用于分析总客户并规划未来容量。

![](../assets/Cumulative_Perspective.png)

- `Percent of First Value perspective`：此透视以分析中包含的首次时间间隔的百分比显示数据。 这有助于衡量特定操作相对于第一阶段性能的有效性。

![](../assets/Percent_of_First_Value.png)

- `Rolling averages window perspective`：滚动平均窗口透视显示量度在指定时间范围内的滚动平均值。 间隔必须与报告级别上设置的间隔相同。 例如，如果报表按周显示收入的最后一个完整季度，则可以将滚动平均窗口时间范围设置为四周。 这使得前三个值为空，第四个值表示收入前四周的平均值。 为清楚起见，如果您使用滚动平均值查看同一指标，请确保关闭`Multiple Y-Axes`复选框，如下面的示例所示。

![](../assets/rolling_avg_window.png)

### 特定于量度的时间选项

报表中使用的量度有两个选项：它们可以根据全局时间选项随时间变化趋势，也可以根据全局时间选项随时间变化趋势（否则将作为一个标量数字显示）。

将量度时间间隔更改为`None`将返回`scalar`个数字，在创建涉及将时间趋势量度除以`scalar`个数字的公式时，此数字非常有用。 此外，您还可以将`scalar`量度的时间范围更改为与报表的时间范围无关的时间范围。

例如，假设您想查看2019年的月收入在2019年总收入中所占的百分比。 您可以向全局时间范围为2019年1月1日至2019年12月31日的报表中添加两个`Revenue`量度，按月分段。

>[!NOTE]
>
>如果添加`group by`维度，请选择新的可视化图表，或者调整时间间隔，然后仅保存数字(`scalar`)。 下次从仪表板打开该报表时，不会保留这些调整，而只会保留时间范围。

若要了解有关在报表中使用时间选项的更多信息，请参阅此[教程](../tutorials/time-options-visual-rpt-bldr.md)。

## 步骤7：保存报表

创建图表时，单击`Visual Report Builder`右上角的&#x200B;**[!UICONTROL Save]**&#x200B;可保存该图表。

您可以选择使用`Type`下拉菜单保存图表、表或数字(`scalar`)，也可以使用`Location`下拉菜单保存报告到仪表板。

然后，单击&#x200B;**[!UICONTROL Save to Dashboard]**&#x200B;可保存报告。

![](../assets/save-to-dashboard.png)

## 报表输出

要帮助您决定选择哪个报表输出，请参阅以下内容：

### 图表

![](../assets/RB_Chart.png)

### 表

![](../assets/RB_Table.png)

### 数字(`scalar`)

![](../assets/RB_Scalar.png)

恭喜！你完了。
