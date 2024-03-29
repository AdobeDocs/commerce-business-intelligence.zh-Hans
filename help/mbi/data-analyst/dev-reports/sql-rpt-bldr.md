---
title: 使用SQLReport Builder
description: 了解使用SQLReport Builder的细节。
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---

# 使用 [!DNL SQL Report Builder]

>[!NOTE]
>
>需要 [管理员权限](../../administrator/user-management/user-management.md) 创建和编辑SQL图表。 `Standard` 用户可以在功能板上重新排列这些图表，并且 `Read-only` 用户拥有与传统图表相同的体验。 另外， `Read-only` 用户无权访问查询的文本。

请参阅 [训练视频](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) 了解更多信息。

[!DNL SQL]或结构化查询语言，是一种用于与数据库通信的编程语言。 在 [!DNL Commerce Intelligence]， [!DNL SQL] 用于从Data Warehouse中查询或检索数据。 查看仪表板上的报告 — 在幕后，每个报告都由 [!DNL SQL] 查询。

您可以使用 [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) 要直接查询Data Warehouse，请查看结果，并将其转换为图表。 您可以使用以下内容开始创建报告 [!DNL SQL Report Builder] 通过单击 **[!UICONTROL Report Builder** > **[!DNL SQL Report Builder]]**.

请参阅 [训练视频](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) 了解更多信息。

此 [!DNL SQL Report Builder] 允许您直接查询Data Warehouse、查看结果并快速将其转换为图表。 使用的最佳部分 [!DNL SQL] 要生成报表，您无需等待更新周期即可对创建的列进行迭代。 如果结果不正确，您可以快速编辑并重新运行查询，直到符合您的预期为止。

本主题将指导您使用 [!DNL SQL Report Builder]. 在您了解自己的方式后，查看 [!DNL SQL] 用于可视化教程，或尝试优化您编写的某些查询。

本文涵盖的内容：

1. [编写查询](#writing)

1. [运行查询并查看结果](#runquery)

1. [创建可视化图表](#createviz)

1. [保存报告](#save)

## [!DNL SQL Report Builder] 集成

[[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) 是唯一无法与一起使用的集成 [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md). 此功能正在开发中。

开始创建 [!DNL SQL] 报表，单击 **[!UICONTROL Report Builder]** 或 **[!UICONTROL Add Report]** 任何仪表板的顶部。 在 [!DNL Report Picker] 屏幕，单击 **[!UICONTROL SQL Report Builder]** 以打开 [!DNL SQL] 编辑者。

## 开始使用

要编辑报表，请单击齿轮(![](../../assets/gear-icon.png))图标（位于的右上角） [!DNL SQL]基于的图表并单击 **[!UICONTROL Edit]**.

## 编写查询 {#writing}

>[!NOTE]
>
>[!DNL SQL Report Builder] 查询区分大小写。 请确保您在编写查询时使用正确的大小写，否则您可能会收到意外的结果或错误。

遵循 [查询优化准则](../../best-practices/optimizing-your-sql-queries.md)，在中编写查询 [!DNL SQL] 编辑者。

>[!IMPORTANT]
>
>**中的量度 [!DNL SQL] 报表**  — 在SQL报表中插入度量时， `current definition` 的量度。

如果度量在将来更新，则SQL报告 *不会* 反映这些更改。 您必须手动编辑报告以使更改生效。

使用侧边栏顶部的按钮，您可以在表格列表和可用于中的量度之间切换 [!DNL SQL Report Builder]. 如果您在列表中看不到要查找的内容，请尝试使用侧栏顶部的搜索栏进行搜索。

您还可以使用中的侧栏 [!DNL SQL] 编辑器通过将鼠标悬停在量度、表和列上并单击，将其直接插入到查询中 **[!UICONTROL Insert]**：

![将表插入到 [!DNL SQL] 编辑者。](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>任何 [SELECT函数](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST)或SQLReport Builder支持PostgreSQL支持的任何不变量数据的函数。 这包括但不限于AVG、COUNT、COUNT DISTINCT、MIN/MAX和SUM。

此外，任何 `JOIN` 类型受支持，但Adobe建议仅使用INNER JOIN，因为它是开销最低的 `JOIN` 类型。

## 运行查询并查看结果 {#runquery}

编写完查询后，单击 **[!UICONTROL Run Query]**. 结果显示在SQL编辑器下方的表中：

![运行查询并查看结果。](../../assets/SQL_Run_Query.gif)

如果结果中有出错的地方，您可以编辑查询并重新运行它，直到满意为止。

您有时可能会看到 [编辑器中带有EXPLAIN的消息](../../best-practices/optimizing-your-sql-queries.md). 如果您看到其中一个，则表示您的查询尚未运行，需要微调一下。

编辑完查询后，您可以转到创建可视化图表或将您的工作保存到功能板。

## 创建可视化图表 {#createviz}

要创建包含查询结果的可视化图表，请单击 **[!UICONTROL Chart]** 选项卡 `Results` 窗格。 在此选项卡中，选择：

* 此 `Series`或要测量的列，如 **售出商品**.
* 此 `Category`或要用于分段数据的列，例如 **客户获取源**.
* 此 `Labels`或X轴值。

下面是可视化流程的外观：

![](../../assets/SQL_RB_viz_overview.gif)

有关如何创建可视化的详细演练，请参阅 [从SQL查询创建可视化图表教程](../../tutorials/create-visuals-from-sql.md){： target=&quot;_blank&quot;}.

## 保存报告 {#save}

在保存所做的工作之前，必须为报表提供一个名称。 请记住遵循 [命名最佳实践指南](../../best-practices/naming-elements.md){： target=&quot;_blank&quot;}并选择能清楚地传达报告内容的内容！

单击 **[!UICONTROL Save]** 位于的右上角 [!DNL SQL] 编辑器并选择报表 `Type` (`Chart` 或 `Table`)。 要完成这些操作，请选择要将报告保存到的功能板，然后单击 **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### 分析您的数据

#### [!DNL SQL Report Builder]

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) 使您能够直接查询Data Warehouse、查看结果并快速将其转换为报表。 使用 [!DNL SQL] 还允许您 [使用 [!DNL SQL] 不可用的函数](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) 在 `Visual` 或 `Cohort` Report Builder，从而让您能够更好地控制数据。

计算列创建工具 [!DNL SQL] 不依赖于更新周期，这意味着您可以根据需要对其进行迭代并立即查看结果。

>[!NOTE]
>
>这仅适用于列的结构，而不适用于数据的新鲜度。 新数据仍依赖于已成功完成的更新周期。

| **这个很适合……** | **这不太适合……** |
|---|---|
| 中级/高级分析师 | 初学者 — 您需要知道 [!DNL SQL]. |
| 此 [!DNL SQL] 精通 | 简单的分析 — 编写查询可能比简单地使用 [!UICONTROL Visual Report Builder]. |
| 构建一次性使用的计算列 | 与他人共享 — 考虑您的受众：他们是否了解 [!DNL SQL]？ 否则，他们可能会对构建报表的方式感到困惑。 |
| 数据与 `one-to-many` 关系 |  |
| 测试新列或分析 |  |

#### 数据库与SQL编辑器结果

大多数情况下，结果的差异可归因于更新周期。 如果 [!DNL Commerce Intelligence] 正在将数据从数据库复制到Data Warehouse中，即使使用相同的查询，您也可能会看到不同的结果。

连接问题也会导致不一致。 导航至 `Connections` 通过单击显示的页面 **[!DNL Manage Data** > **Connections]** 签出 — 有问题的数据库集成是否存在错误？ 如果是这样的话，您可能需要 [重新验证集成](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html) 让一切恢复运转。

如果所有集成都连接成功，并且您未处于更新周期中，则可能有其他错误。

#### 删除 [!DNL SQL] 是否还会从我的Data Warehouse中删除基础列？

不需要，无论如何构建Data Warehouse，您都不会丢失任何列。

使用创建的列 `Data Warehouse Manager` 如果删除使用它们的报表或查询，则不会受到影响。

使用创建的列 [!DNL SQL Report Builder] 不会保存到您的Data Warehouse。


#### `Report Builder` 对比 `SQL Report Builder`

此 [!DNL SQL Report Builder] 在创建和构建图表时为您提供了更大的灵活性 — 例如，您可以选择应该在 `X` 和 `Y` 坐标轴。 有关在中创建图表的详细信息 [!DNL SQL Report Builder]，查看 [创建可视化图表 [!DNL SQL] 查询](../../tutorials/create-visuals-from-sql.md) 教程。

#### `Cohort Report Builder` {#cohortrb}

不像 [!DNL Visual Report Builder]， [[!DNL Cohort Report Builder]](../dev-reports/cohort-rpt-bldr.md) 旨在用于一个目的 — 分析和识别一段时间内类似用户群组的行为趋势。 使用 [!DNL Cohort Report Builder] 不需要任何 [!DNL SQL] 精明，所以如果你刚开始的话，可以毫不犹豫地直接跳进去。

| **这个很适合……** | **这不太适合……** |
|---|---|
| 中级/高级分析师 | 初学者 — 您需要定义练习的同类群组。 |
| 确定一段时间内的行为趋势 | 定性分析 — 可以是 [完成](../dev-reports/create-qual-cohort-analysis.md)，但需要Adobe帮助。 |

## 在更新周期后重建查询

您不必重新生成查询。 使用创建的报告 [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) 保存方式与在中创建的相同 `Report Builder`. 的更新过程 [!DNL SQL] 图表是相同的 — 更新数据后，图表中的值将重新计算并重新显示。

>[!NOTE]
>
>删除 [!DNL SQL] 不会从Data Warehouse中删除基础列。 无论如何构建列，都不会丢失任何列。

* 如果删除使用使用Data Warehouse管理器创建的报表或查询，则这些列不会受到影响。

* 使用SQLReport Builder创建的列不会保存到Data Warehouse中。

## 正在结束 {#wrapup}

如果您希望尝试一些更具挑战性的东西，为什么不尝试编写针对可视化进行了优化的查询？ 查看 [创建可视化图表 [!DNL SQL] 查询教程](../../tutorials/create-visuals-from-sql.md){： target=&quot;_blank&quot;}以开始使用。
