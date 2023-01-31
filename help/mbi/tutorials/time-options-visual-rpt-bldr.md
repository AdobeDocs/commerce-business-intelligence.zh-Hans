---
title: 可视化Report Builder中的使用时间选项
description: 了解如何分析报表中特定时间段的数据。
exl-id: a1bb4838-f882-44b1-a29f-84b985032ceb
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 0%

---

# 使用 `Time` 选项 `Visual Report Builder`

的功能之一 `Visual Report Builder` 是全球 `Time Range` 和 `Interval` 设置。 这些设置允许您分析报表中特定时间段的数据。

但是，对于某些分析，您可能需要在同一报表中考虑不同的时间范围或时间间隔。 那就是 `Time` 有选择。 让你更清楚地知道如何使用 `Time` 本教程将介绍您的报表中的选项，其中涵盖以下用例：

* [分析没有时间戳的量度](#notimestamp)
* [为一个量度提供独立的时间间隔](#independenttimeinterval)
* [比较不同时间范围中的相同量度](#difftimerange)

如果要遵循本主题中讨论的一些示例报表，请打开 [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md) 才能继续。

## 分析没有时间戳的量度 {#notimestamp}

某些量度无法随时间呈现趋势，因为数据未收集或存储为关联的时间戳。 例如，库存表通常每个SKU只包含一行。 在这种情况下，您应 [创建量度](../data-user/reports/ess-manage-data-metrics.md) 而不指定时间戳。

在报表中使用此量度时，您会注意到将此量度添加到报表会自动设置独立的 `Time Interval` of `None` 和 `Time Range` of `Global`:

![](../assets/Metrics_without_timestamps.gif)

## 为一个量度提供独立的时间间隔 {#independenttimeinterval}

`Time` 利用选项，可创建基于时间的100%图表，以确定在特定时间范围内，哪天、周、月或年贡献的价值最大。 在此部分中，我们将创建一个图表，显示每年每个日历月产生的收入百分比。

如果要比较年同比产生的收入，此类型的报表会非常有用。 例如，如果2015年的一张图表显示，1月份贡献了该年收入的18%，而2016年的一份图表显示仅贡献了8%，那么你就可以开始研究可能发生的情况。

1. 添加 `Revenue` 量度。
1. 单击 **[!UICONTROL Duplicate]** 以复制量度。
1. 单击全局 **[!UICONTROL Time Range]** 选项，然后 **[!UICONTROL Moving Time Range]**. 将此参数设置为 `Last Year`.
1. 单击全局 **[!UICONTROL Time Interval]** 选项，并将其设置为 `Monthly`.
1. Report Builder会自动为第二个量度添加第二个Y轴。 取消选择 `Multiple Y-Axes` 框中。
1. 接下来，我们申请一个独立 `Time Interval` 到第一个量度。 单击 **[!UICONTROL Time Options]** （时钟图标） `first Revenue metric`.
1. 单击 **[!UICONTROL Time Options]** 在报表上方显示的展开窗口中。
1. 在下拉菜单中，设置以下内容：

   * `Time Interval`:将此设置为 `None`.

   * `Time Range`:将此设置为 `Last Year` 首次单击 **[!UICONTROL Custom]**，则 **[!UICONTROL Moving Range]**，最后选择 `Last Year` 选项。

   * 单击 **[!UICONTROL Apply]** 以保存间隔和范围设置。 这会创建一个用于计算上一年总收入的量度。 接下来，我们将此量度用作公式中的分母。

   * 要查看每月收入百分比，我们需要向报表添加一个公式。 单击 **[!UICONTROL Add Formula]**.

   * 输入 `B/A` 在“公式”字段中，然后选择 `% Percent` 从文本字段旁边的下拉菜单中。 此公式将去年特定月份的收入额除以去年的收入总额。

   * 单击 **[!UICONTROL Apply Changes]**.

   * 隐藏两个输入量度并重命名公式。

现在，我们可以看到，去年每个月的影响力有多大：

![](../assets/Independent_Time_Int.png)

## 比较不同时间范围中的相同量度 {#difftimerange}

此示例使用一个名为的自定义维度 `Day number of the month`. 如果要创建此报表，并且您的Data warehouse中尚未包含此维度， [联系支持](../guide-overview.md) 以寻求帮助。

此类别中最常见的两个示例是(1)比较增长量度（年同比或月同比收入）和(2)更好地了解近期库存或物料销售趋势。

为了演示此用例，我们查看了上个月与上年同期相比的每日收入。 假设我们想看看2016年1月的每一天收入，然后将其与2015年1月、2014年1月等的收入进行比较 — 此报告将向我们展示这一点。

1. 添加 `Revenue` 量度。
1. 单击 **[!UICONTROL Duplicate]** 以复制量度。
1. 将第一个量度重命名为 `Items sold last 7 days` 第二个量度 `Items sold last 28 days`.
1. 单击 **[!UICONTROL Time Range]**，则 **[!UICONTROL Moving Time Range]**. 将此参数设置为 `Last Month`.
1. 单击 **[!UICONTROL Time Interval]** 将其设置为 `None`.
1. 单击 **[!UICONTROL Time Options]** （时钟图标）位于第二个 `Revenue` 量度。
1. 单击 **[!UICONTROL Time Options]** 在报表上方显示的展开窗口中。
1. 在下拉菜单中，设置以下内容：

   * `Time Interval`:将此设置为 `None`.

   * `Time Range`:将此设置为 `From 14 Months Ago To 13 Months Ago` 首次单击 **[!UICONTROL Custom]** then **[!UICONTROL Moving Range]**. 使用菜单顶部的字段和下拉菜单设置范围。 此设置允许我们查看上个月（但是上一年）的收入。
   如果量度从报表中消失，请不要担心 — 设置独立时间选项会自动从报表中隐藏量度。 要重新显示它，请单击 **[!UICONTROL Show]** 量度旁边。

   ![](../assets/Different_Time_Ranges.gif)

   * 单击 **[!UICONTROL Apply]** 以保存间隔和范围设置。

   * 接下来，我们添加自定义 `Day number of the month` 通过单击 **[!UICONTROL Group By]** 和选择维度。 这将返回订单月份的日期编号 — 例如，在3月2日下达的订单将返回 `2`.

   * 在 `Group By` 下拉列表，选择 `Show All` 单击 **[!UICONTROL Apply]**. 这将有效地为报表创建X轴值：

   ![](../assets/TO4.png)

   * 重命名量度。 在本例中，第一个量度是 `Revenue - 2015` 第二个是 `Revenue - 2014`.



自定义的另一个常见用法 `Time Options` 是确定供应周数。 特别是在假日季或特殊促销期间，您可能需要考虑在上周、月和上一促销期间售出的商品，以便做出明智的购买决策。

请记住，将时间范围设置为您自己构建此报表时所需的时间范围。

1. 添加 `Items Sold` 量度。
1. 单击 **[!UICONTROL Duplicate]** 以复制量度。
1. 重命名量度。 您可以使用与我们相同的名称，或使用类似的名称：
   1. 将第一个量度重命名为 `Items sold last 7 days`.
   1. 将第二个量度重命名为 `Items sold last 28 days`.
1. 在 `Items sold last 7 days` 量度，单击全局 **[!UICONTROL Time Range]** 选项，然后 **[!UICONTROL Moving Time Range]**. 在本例中，我们将其设置为 `Last 7 Days`.
1. 单击 **[!UICONTROL Time Interval]** 将其设置为 `None`.
1. 接下来，我们定义 `Time Options` 对于 `Items sold last 28 days` 量度。 单击 **[!UICONTROL Time Options]** （时钟图标） `second Items sold` 量度。
1. 单击 **[!UICONTROL Time Options]** 在报表上方显示的展开窗口中。
1. 在下拉菜单中，设置以下内容：

   * `Time Interval`:将此设置为 `None`.
   * `Time Range`:将此设置为 `From 29 days to 1 day ago` 首次单击 **[!UICONTROL Custom]**，则 **[!UICONTROL Moving Range]**. 使用菜单顶部的字段和下拉菜单设置范围。
   * 单击 **[!UICONTROL Apply]** 以保存间隔和范围设置。
   * 复制 `Items sold last 28 days` 量度并打开新量度 `Time Options`. 将选项设置为：

      * `Time Interval`:将此项保留为 `None`.
      * `Time Range`:通过单击 **[!UICONTROL Specific Date Range]** 然后输入相应的日期。
      * 重命名量度 `Items sold during last promotion` 或者类似的。
      * 添加 `Units on hand` 量度。
      * 接下来，我们需要添加一些计算，以便在考虑销售趋势后，显示当前的周数(`last 7 days`, `last 28 days`和 `last promo` 期)，我们将包括在报告中。 您需要为每个时间段执行一次此操作。

要创建公式，请单击 **[!UICONTROL Add Formula]**. 输入下面的公式并单击 **[!UICONTROL Apply Changes]** 完成。 对以下三个时间段中的每个时间段重复此操作：

* 对于 `last 7 days time period`，输入 `D / A` 在 `Formula` 字段。
* 对于 `last 28 days time period`，输入 `D / (B/4)` 在 `Formula` 字段。

   >[!NOTE]
   >
   >请务必在此处标准化您选择的时间范围。 在本例中，28天应当分为4周。 您可能需要对公式应用不同的逻辑。

* 对于 `last promo period`，输入 `D / C` 在 `Formula` 字段。

   ![](../assets/Different_Time_Ranges_2.png)

* 最后，通过隐藏量度并添加 `SKU` 或与报表类似的维度 `Group By`.

此示例说明，当前库存水平非常适合于在整个产品范围内进行14天的销售。 但是，添加一个类似的促销期意味着公司需要做出一些改变 — 要么订购更多库存，要么只推广库存量足够的商品。

由于客户的行为随时间而有所不同，因此在执行分析时可能会看到数据差异。 通过设置自定义时间选项，您可以快速创建复杂的分析，从而实现数据驱动的决策，从而将历史趋势考虑在内。

查看我们的 [培训视频](https://support.magento.com/hc/en-us/articles/360016730071-Training-Video-Time-Options-in-the-Visual-Report-Builder) 以了解更多。
