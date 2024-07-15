---
title: 使用“显示顶部/底部”功能排序数据
description: 了解如何使用显示顶部/底部功能对数据排序。
exl-id: d47119f4-cdc5-4fa7-a606-d4b8555a8843
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# 使用`Show Top/Bottom`功能对数据排序

在`Visual Report Builder`中，您可以执行更多操作，而不是创建一段时间内该趋势的分析。 例如，您可以构建一个报表来显示客户获取和营销渠道的价值，但也可以构建一个仅显示前五名绩效者的报表。 同样，您可以通过创建显示哪些州产生的收入最多的报告，重新集中营销工作。

这种类型的排序和排序可以在同时使用`Group By`和`Time Interval of None`的报表中完成。 当这两个元素都在报表中时，`Show Top/Bottom`功能会显示在图表预览上方。 此功能允许您根据设置的参数查看顶端（最高到最低）和底部（最低到最高）数据点。

![在可视化Report Builder中显示顶部/底部功能。](../../assets/Show_Top_Bottom.png)

## 如何使用它？ {#how}

单击&#x200B;**[!UICONTROL Show Top/Bottom link]**&#x200B;以设置显示和排序参数。 文本框中的数字可以是整数（如`5`）或`ALL`。 接下来，您可以选择按指标或分组对报表进行排序。

例如，如果要显示带来最多收入的五个反向链接来源，您可以按照以下方式操作：

1. 将`Revenue`量度添加到报表中。

1. 添加`Group By`以按反向链接来源对量度进行分段。

1. 将`Time Interval`设置为`None`。

1. 在`Show Top/Bottom`设置中，将显示设置为`5`，以便报表中只包含具有前五个总收入金额的反向链接来源。

>[!NOTE]
>
>由于报表没有`Time Interval`，因此值（在本例中是前五个反向链接源）可能会随着时间的推移而发生变化。 如果一个反向链接来源在收入方面超过另一个反向链接来源，则其显示顺序会发生更改。

## 使用多个量度怎么样？ {#multiplemetrics}

当报表中有多个量度时，使用此功能会变得复杂，因为每个量度只能按其本身或按分组之一排序。

假设您生成了一个同时具有`Revenue`和`Number of orders`指标（按反向链接来源分组）的报告。 `Revenue`只能按`Revenue`或引用源排序，`Number of orders`只能按`Number of orders`或引用源排序。

这意味着尽管您可以仅显示来自前`5`个创收反向链接来源的`Revenue`，但不能同时显示来自前`5`个创收反向链接来源的订单数。 简而言之：当存在多个量度时，最佳方法是按分组对每个量度进行排序。

以下是按`Revenue`量度本身而不是按分组进行排序的图表示例。 如您所见，如果不按分组对量度进行排序，则会创建一个异常（并且最终毫无帮助）的报告：

![异常且无帮助的报告结果。](../../assets/strange-report-results.png)

如果您已按分组对两个量度进行排序，则图表将如下所示：

![按分组对两个量度进行排序。](../../assets/sort-metrics-by-grouping.png)

## 默认情况下，如何对值进行排序？ {#defaultsorting}

当在具有`Group by`且`Time Interval`为`None`的报表中仅包含一个量度时，`Visual Report Builder`中的默认排序是基于该量度显示最大值。 在此实例中，如果满足您的需求，则可能无需`Show Top/Bottom`功能。

此示例查看了您的销售代表已结束的销售机会数。 此表会根据量度自动从最高排序到最低，在本例中为`Won Opportunities`。

![按指标排序。](../../assets/Ordered_by_metric.png)

但是，在添加第二个量度时，默认设置是根据分组对排名最前的量度进行排序。 添加量度和分组后，默认排序将依次基于第一个分组、第二个分组，依此类推。

![按分组排序。](../../assets/Ordered_by_grouping.png)

## 正在结束 {#wrapup}

虽然这里介绍了一些基本功能，但此功能有许多有趣的用途。

想一想以前的销售代表和销售机会示例。 删除`Time Interval`、应用`Group By`并根据分组对数据排序，使我们能够详细了解每个代表的成功机会数。 此外，使用`Show Top/Bottom`功能可让我们发现谁是表现最好的人。
