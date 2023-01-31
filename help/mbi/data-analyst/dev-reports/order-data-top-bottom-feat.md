---
title: 使用显示顶部/底部功能对数据排序
description: 了解如何使用显示顶部/底部功能对数据进行排序。
exl-id: d47119f4-cdc5-4fa7-a606-d4b8555a8843
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# 使用对数据排序 `Show Top/Bottom` 功能

您可以在 `Visual Report Builder` 而不是创建随时间推移的趋势分析。 例如，您可以构建一个报表以显示您的客户获取和营销渠道的价值，但您也可以构建一个报表，仅显示前五位执行者。 同样，您也可以通过创建一个报表来重新调整营销工作，该报表显示哪些州产生的收入最多。

此类数据的排序和排序可以在同时使用 `Group By` 和 `Time Interval of None`. 当这两个元素都在报表中时， `Show Top/Bottom` 功能将在图表预览上方显示。 此功能允许您根据您设置的参数查看顶部（最高到最低）和底部（最低到最高）数据点。

![在可视化Report Builder中显示顶部/底部功能。](../../assets/Show_Top_Bottom.png)

## 如何使用它？ {#how}

单击 **[!UICONTROL Show Top/Bottom link]**，将显示一个窗口，您可以在其中设置显示和排序参数。 文本框中的数字可以是整数(如 `5`)或 `ALL`. 接下来，您可以选择按量度或按分组对报表进行排序。

例如，如果我们想要显示贡献最大收入的五个反向链接来源，我们就是这样做的：

1. 添加 `Revenue` 量度。

1. 添加 `Group By` 按引荐源对量度进行分段。

1. 已设置 `Time Interval` to `None`.

1. 在 `Show Top/Bottom` 设置，将显示内容设置为 `5` 因此，报表中只包含具有前五个总收入额的推荐来源。

>[!NOTE]
>
>因为报表没有 `Time Interval`，则值（在本例中为前五个反向链接源）会随时间而改变。 如果一个反向链接来源在收入方面超过另一个来源，则来源显示的顺序将发生更改。

## 使用多个量度呢？ {#multiplemetrics}

当报表中有多个量度时，使用此功能会变得复杂，因为每个量度只能按自身或按其中一个分组进行排序。

假设我们使用 `Revenue` 和 `Number of orders` 量度，按引荐来源分组。 `Revenue` 只能按 `Revenue` 或反向链接来源和 `Number of orders` 只能按 `Number of orders` 或反向链接来源。

这意味着，当我们 `Revenue` 仅从顶部 `5` 产生反向链接来源的收入，我们无法同时按排名最前的 `5` 产生转荐来源的收入。 简言之：当存在多个量度时，最好按分组对每个量度进行排序。

下面是一个图表示例，我们在其中对 `Revenue` 量度，而不是按分组。 如您所见，不按分组对量度进行排序，会创建一个奇怪（而且最终无助）的报表：

![奇怪而无益的报告结果。](../../assets/strange-report-results.png)

如果我们按分组对两个量度进行排序，则图表将如下所示：

![按分组对两个量度进行排序。](../../assets/sort-metrics-by-grouping.png)

## 默认情况下，值是如何排序的？ {#defaultsorting}

当报表中只包含一个量度，且 `Group by` 和 `Time Interval` of `None`，在 `Visual Report Builder` 是显示基于量度的排名最前的值。 在本例中， `Show Top/Bottom` 如果此功能符合您的需求，则可能不是必需的功能。

在本例中，我们将查看我们的销售代表已关闭的机会数。 此表会根据量度自动从最高到最低进行排序，在此例中为 `Won Opportunities`.

![按量度排序。](../../assets/Ordered_by_metric.png)

但是，添加第二个量度时，默认设置是根据分组对顶部量度进行排序。 添加量度和分组后，默认排序将依据第一个分组，然后是第二个分组，依此类推。

![按分组排序。](../../assets/Ordered_by_grouping.png)

## 包装 {#wrapup}

我们在文章的开头提到了这一点，但我们再次说：虽然我们介绍了一些基本示例，但此功能有许多有趣的用途。

想想我们以前的销售代表和销售机会示例。 删除 `Time Interval`，应用 `Group By`，并根据分组对数据进行排序，以便我们详细了解每个代表赢得的机会数量。 此外，使用 `Show Top/Bottom` 通过功能，我们可以发现哪些表现最佳。
