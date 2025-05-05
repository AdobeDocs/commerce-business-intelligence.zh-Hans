---
title: 在可视化Report Builder中使用时间选项
description: 了解如何分析报告中特定时间段的数据。
exl-id: a1bb4838-f882-44b1-a29f-84b985032ceb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 0%

---

# 在[!DNL Visual Report Builder]中使用[!DNL Time]选项

[!DNL Visual Report Builder]的功能之一是全局`Time Range`和`Interval`设置。 利用这些设置，可分析特定时间段内的报表数据。

但是，对于某些分析，可能需要在同一报表中考虑不同的时间范围或时间间隔。 这就是`Time`选项的功能。 为了让您更好地了解如何在报表中使用`Time`选项，本教程涵盖以下用例：

* [分析不带时间戳的量度](#notimestamp)
* [指定一个量度独立的时间间隔](#independenttimeinterval)
* [比较不同时间范围内的相同量度](#difftimerange)

如果要与本主题中讨论的一些示例报告一起关注，请打开[[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md)，然后再继续。

## 分析不带时间戳的量度 {#notimestamp}

某些量度根本无法随时间变化趋势，因为未收集数据或这些数据未与关联的时间戳一起存储。 例如，库存表通常每个SKU只包含一行。 在这种情况下，您应在不指定时间戳的情况下[创建量度](../data-user/reports/ess-manage-data-metrics.md)。

在报表中使用此类量度时，您会注意到，将此量度添加到报表会自动设置独立的`Time Interval`（共`None`和`Time Range`）（共`Global`个）：

![](../assets/Metrics_without_timestamps.gif)

## 指定一个量度独立的时间间隔 {#independenttimeinterval}

`Time`选项允许您创建基于时间的100%图表，以识别在特定时间范围内哪天、周、月或年贡献了最大的值。 在此部分中，您将创建一个图表，其中显示一年中每个日历月产生的收入百分比。

如果要比较年同比产生的收入，此类报表会非常有用。 例如，您有一张2015年的图表显示，1月占全年收入的18%，而另一张图表显示，2016年仅占8%。 你可以开始研究可能发生的事。

1. 将您的`Revenue`量度添加到报表中。
1. 单击&#x200B;**[!UICONTROL Duplicate]**&#x200B;以制作该量度的副本。
1. 单击全局&#x200B;**[!UICONTROL Time Range]**&#x200B;选项，然后单击&#x200B;**[!UICONTROL Moving Time Range]**。 将此项设置为`Last Year`。
1. 单击全局&#x200B;**[!UICONTROL Time Interval]**&#x200B;选项并将其设置为`Monthly`。
1. Report Builder会自动为第二个量度添加第二个Y轴。 取消选择`Multiple Y-Axes`框。
1. 接下来，将独立的`Time Interval`应用于第一个量度。 单击`first Revenue metric`右侧的&#x200B;**[!UICONTROL Time Options]** （时钟图标）。
1. 在报表上方显示的展开窗口中单击&#x200B;**[!UICONTROL Time Options]**。
1. 在下拉菜单中，设置以下内容：

   * `Time Interval`：将此项设置为`None`。

   * `Time Range`：通过先单击&#x200B;**[!UICONTROL Custom]**，再单击&#x200B;**[!UICONTROL Moving Range]**，最后选择`Last Year`选项，将此选项设置为`Last Year`。

   * 单击&#x200B;**[!UICONTROL Apply]**&#x200B;保存间隔和范围设置。 这将创建一个量度，用于计算上一年的总收入。 接下来，在公式中将此量度用作分母。

   * 要查看每个月的收入百分比，您必须向报表中添加一个公式。 单击&#x200B;**[!UICONTROL Add Formula]**。

   * 在公式字段中输入`B/A`，然后从文本字段旁边的下拉列表中选择`% Percent`。 此公式将去年特定月份的收入额除以去年的收入总额。

   * 单击&#x200B;**[!UICONTROL Apply Changes]**。

   * 隐藏两个输入量度并重命名公式。

现在，您可以看到去年每个月的影响力有多大：

![](../assets/Independent_Time_Int.png)

## 比较不同时间范围内的相同量度 {#difftimerange}

此示例使用名为`Day number of the month`的自定义维度。 如果要创建此报表，但您的Data Warehouse中还没有此维度，请[联系支持人员](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=zh-Hans)寻求帮助。

此类别中最常见的两个示例是(1)比较增长指标（年收入或月收入）和(2)更好地了解最近的库存或物料销售趋势。

要演示此用例，请查看上个月的每日收入与去年同期相比。 假设您想查看2016年1月的每日收入，然后将其与2015年1月、2014年1月等进行比较，此报表将向我们显示这一点。

1. 将您的`Revenue`量度添加到报表中。
1. 单击&#x200B;**[!UICONTROL Duplicate]**&#x200B;以制作该量度的副本。
1. 将第一个指标重命名为`Items sold last 7 days`，将第二个指标重命名为`Items sold last 28 days`。
1. 单击&#x200B;**[!UICONTROL Time Range]**，然后单击&#x200B;**[!UICONTROL Moving Time Range]**。 将此项设置为`Last Month`。
1. 单击&#x200B;**[!UICONTROL Time Interval]**&#x200B;并将其设置为`None`。
1. 单击第二个`Revenue`量度旁边的&#x200B;**[!UICONTROL Time Options]** （时钟图标）。
1. 在报表上方显示的展开窗口中单击&#x200B;**[!UICONTROL Time Options]**。
1. 在下拉菜单中，设置以下内容：

   * `Time Interval`：将此项设置为`None`。

   * `Time Range`：通过先单击&#x200B;**[!UICONTROL Custom]**，然后单击&#x200B;**[!UICONTROL Moving Range]**&#x200B;将此项设置为`From 14 Months Ago To 13 Months Ago`。 使用菜单顶部的字段和下拉菜单设置范围。 此设置允许我们查看上个月但上一年度的收入。

   如果量度从报表中消失，请不要担心 — 设置独立时间选项会自动从报表中隐藏该量度。 要重新显示它，请单击量度旁边的&#x200B;**[!UICONTROL Show]**。

   ![](../assets/Different_Time_Ranges.gif)

   * 单击&#x200B;**[!UICONTROL Apply]**&#x200B;保存间隔和范围设置。

   * 接下来，通过单击&#x200B;**[!UICONTROL Group By]**&#x200B;并选择维度，添加您的自定义`Day number of the month`维度。 这将返回订单当月的日期编号 — 例如，3月2日下单的订单将返回`2`。

   * 在`Group By`下拉列表中，选择`Show All`并单击&#x200B;**[!UICONTROL Apply]**。 这将为报表创建X轴值：

   ![](../assets/TO4.png)

   * 重命名量度。 在此示例中，第一个量度是`Revenue - 2015`，第二个量度是`Revenue - 2014`。

自定义`Time Options`的另一个常见用途是确定供应周。 特别是在假日季节或特殊促销期间，您可能需要考虑过去一周、一个月和上一个促销期间销售的项目，以便做出明智的购买决策。

切记在自行构建此报表时将时间范围设置为所需的值。

1. 将您的`Items Sold`量度添加到报表中。
1. 单击&#x200B;**[!UICONTROL Duplicate]**&#x200B;以制作该量度的副本。
1. 重命名量度。 您可以使用相同的名称或类似名称：
   1. 将第一个量度重命名为`Items sold last 7 days`。
   1. 将第二个量度重命名为`Items sold last 28 days`。
1. 在`Items sold last 7 days`指标上，单击全局&#x200B;**[!UICONTROL Time Range]**&#x200B;选项，然后单击&#x200B;**[!UICONTROL Moving Time Range]**。 对于此示例，您将其设置为`Last 7 Days`。
1. 单击&#x200B;**[!UICONTROL Time Interval]**&#x200B;并将其设置为`None`。
1. 接下来，您为`Items sold last 28 days`量度定义`Time Options`。 单击`second Items sold`量度右侧的&#x200B;**[!UICONTROL Time Options]** （时钟图标）。
1. 在报表上方显示的展开窗口中单击&#x200B;**[!UICONTROL Time Options]**。
1. 在下拉菜单中，设置以下内容：

   * `Time Interval`：将此项设置为`None`。
   * `Time Range`：通过先单击&#x200B;**[!UICONTROL Custom]**，然后单击&#x200B;**[!UICONTROL Moving Range]**&#x200B;将此项设置为`From 29 days to 1 day ago`。 使用菜单顶部的字段和下拉菜单设置范围。
   * 单击&#x200B;**[!UICONTROL Apply]**&#x200B;保存间隔和范围设置。
   * 复制`Items sold last 28 days`指标并打开新指标的`Time Options`。 将选项设置为以下内容：

      * `Time Interval`：保留为`None`。
      * `Time Range`：通过单击&#x200B;**[!UICONTROL Specific Date Range]**&#x200B;并输入相应的日期，将此项更改为与您感兴趣的促销活动相一致的日期范围。
      * 重命名指标`Items sold during last promotion`或类似内容。
      * 添加您的`Units on hand`量度。
      * 接下来，您必须添加计算，以便根据销售趋势显示您要在报表中包括的时间段（`last 7 days`、`last 28 days`和`last promo`时段）的现有周数。 您必须为每个时间段执行一次此操作。

若要创建公式，请单击&#x200B;**[!UICONTROL Add Formula]**。 输入下面的公式，完成后，单击&#x200B;**[!UICONTROL Apply Changes]**。 对三个时间段中的每一个重复此操作：

* 对于`last 7 days time period`，在`Formula`字段中输入`D / A`。
* 对于`last 28 days time period`，在`Formula`字段中输入`D / (B/4)`。

  >[!NOTE]
  >
  >请务必在此标准化您选择的时间范围。 在此示例中，将28天划分为四周。 您可能需要对公式应用不同的逻辑。

* 对于`last promo period`，在`Formula`字段中输入`D / C`。

  ![](../assets/Different_Time_Ranges_2.png)

* 最后，通过隐藏量度并将`SKU`或类似维度作为`Group By`添加到报表来自定义报表。

此示例表明，当前库存水平非常适合于全产品14天销售。 然而，加上一个类似的促销期，表明该公司需要做出一些改变 — 要么订购更多库存，要么只促销库存量足够的。

由于客户随着时间的推移表现出的行为有所不同，因此，您可能会在执行分析时看到数据差异。 通过设置自定义时间选项，您可以快速创建复杂的分析，从而做出考虑历史趋势的数据驱动型决策。

