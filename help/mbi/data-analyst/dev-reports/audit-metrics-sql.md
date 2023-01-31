---
title: 使用SQLReport Builder
description: 了解如何使用SQLReport Builder审核数据和量度，以便将结果与本地数据库中的数据进行比较。
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# `SQL Report Builder`

的 `SQL Report Builder` 主要用于构建新报表并进行迭代分析，但也可用于有效审核数据和量度。 以下信息说明了如何使用 `SQL Report Builder` 以便将结果与本地数据库的数据进行比较。

## 查询量度

要开始配置，请打开 `SQL Report Builder` 导航至 **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. 您可以使用SQL编辑器中的侧栏，通过将鼠标悬停在量度上并单击，将量度直接插入查询中 **[!UICONTROL Insert]**. 这会将该量度的查询定义添加到编辑器中。 定义将包括以下组件：

- 的 **量度操作** ，如以下示例中的SUM()所示。
- 的 **表** 从中生成量度，如FROM子句所示。
- 任意 **过滤器（和过滤器集）** 量度中已添加的WHERE子句所指示的事件数。
- 组件 **timestamp** （年、月），如以下示例中的ORDER BY子句所示。

如果希望更清晰地查看查询，则可以重新设置查询字段中查询显示格式。 准备就绪后，选择 `Run Query`. 结果将作为表格填充在查询下方的报表面板中。

![](../../assets/run-query-results.gif)

## 限制查询

如果您试图找出特定差异或数据集，则应将查询限制为针对本地数据库检查的特定示例。 为此，您可以编辑查询以符合所需的限制。 在以下示例中，我们将查询限制为仅包含2013年1月1日或更高版本的收入。 更新查询后，选择 **[!UICONTROL Run Query]** 再次更新结果。

![](../../assets/restricting-query.gif)

## 保存和导出

当报表满足您的需求时，通过为报表提供一个不同的名称并单击 **[!UICONTROL Save]**，然后选择要保存的报表类型和功能板。 在审核量度时，我们建议将报表另存为 `Table` 并将其保存到测试仪表板。

保存报表后，通过选择 `Go to Dashboard`. 从此处，您可以通过查找报表并选择 **[!UICONTROL Options gear > Full `.csv`导出]** 或 **[!UICONTROL Full Excel Export]**.

![](../../assets/export-dboard-data.gif)

## 自定义查询

您还可以编写自定义查询并导出要与本地数据库进行比较的结果。 关注 [查询优化准则](../../best-practices/optimizing-your-sql-queries.md)，在SQL编辑器中写入查询。 您可以使用侧栏顶部的按钮，在可用于 `SQL Report Builder` 并将其添加到查询中。 当自定义查询符合您的需求时，您可以保存报表并从功能板导出该数据。

### 还难过？

如果您在审核数据后发现差异，请查看 [联系支持人员：数据差异](https://support.magento.com/hc/en-us/articles/360016505312) 支持文章，以了解有关下一步操作的更多信息。
