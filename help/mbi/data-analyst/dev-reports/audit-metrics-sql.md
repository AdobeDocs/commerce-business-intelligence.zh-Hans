---
title: 使用SQLReport Builder
description: 了解如何使用SQLReport Builder审核数据和量度，以便将结果与本地数据库中的数据进行比较。
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
role: Admin, Data Architect, Data Engineer, User
feature: Reports, Data Warehouse Manager, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# [!DNL SQL Report Builder]

此 [!DNL SQL Report Builder] 主要用于构建新报告和迭代分析，但也可以用于有效审核数据和量度。 以下信息介绍了如何使用 [!DNL SQL Report Builder] 以便您可以将结果与本地数据库中的数据进行比较。

## 查询量度

要开始配置，请打开 [!DNL SQL Report Builder] 导航到 **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. 您可以使用中的侧栏 [!DNL SQL] 编辑器，通过将鼠标悬停在量度上并单击 **[!UICONTROL Insert]**. 这会将该量度的查询定义添加到编辑器中。 该定义包括以下组成部分：

- 此 **量度操作** 正在执行，指示为 `SUM()` 在以下示例中。
- 此 **表** 其中构建了指标，由 `FROM` 子句。
- 任意 **过滤器（和过滤器集）** 添加到量度的，表示为 `WHERE` 子句。
- 的组件 **时间戳** （年、月）的数据，由 `ORDER BY` 子句。

为了更清楚地查看查询，您可以重新格式化查询在查询字段中的显示方式。 准备就绪后，选择 `Run Query`. 结果将作为表格填充到查询下的报表面板中。

![](../../assets/run-query-results.gif)

## 限制查询

如果您尝试查明特定差异或数据集，则应将查询限制为特定示例以检查您的本地数据库。 为此，您可以编辑查询以符合所需的限制。 在以下示例中，您将查询限制为仅包含来自2013年1月1日或之后日期的收入。 更新查询后，选择 **[!UICONTROL Run Query]** 以更新结果。

![](../../assets/restricting-query.gif)

## 保存和导出

当报表满足您的需求时，请为报表指定不同的名称，然后单击 **[!UICONTROL Save]**，并选择要保存的报表类型和功能板。 在审核指标时，Adobe建议将报表另存为 `Table` 并保存到测试仪表板。

保存报告后，通过选择导航到该仪表板 `Go to Dashboard`. 从那里，您可以通过找到报告并选择 **[!UICONTROL Options gear > Full `.csv`导出]** 或 **[!UICONTROL Full Excel Export]**.

![](../../assets/export-dboard-data.gif)

## 自定义查询

您还可以编写自定义查询并导出结果，以与本地数据库进行比较。 遵循 [查询优化准则](../../best-practices/optimizing-your-sql-queries.md)，在SQL编辑器中编写查询。 您可以使用侧边栏顶部的按钮在表列表和可用于的量度之间进行切换。 [!DNL SQL Report Builder] 并将它们添加到您的查询中。 当您的自定义查询符合您的需要时，您可以保存报告并从功能板导出该数据。

>[!NOTE]
>
>如果审计数据后发现不一致，请查看 [联系支持人员：数据差异](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html) 支持主题，以了解有关后续操作的更多信息。
